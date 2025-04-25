
# Visão Geral Aprimorada do Django REST Framework

## Tabela de Métodos e Hooks (Explicação Expandida)

### dispatch()
**O que faz:** Primeiro método chamado em qualquer requisição. Responsável por:
1. Identificar o método HTTP (GET, POST, etc.)
2. Aplicar middlewares (autenticação, permissões)
3. Chamar o método correspondente (get, post, etc.)

**Quando sobrescrever:** 
- Exemplo: Adicionar headers personalizados em todas as respostas
- Cuidado: Alterações aqui afetam todas as requisições

```python
class CustomViewSet(viewsets.ModelViewSet):
    def dispatch(self, request, *args, **kwargs):
        response = super().dispatch(request, *args, **kwargs)
        response['X-Custom-Header'] = 'MyValue'
        return response
```

### initial()
**O que faz:** Executado após o dispatch, antes do método handler. Ordem de operações:
1. Formatação da entrada (parsers)
2. Autenticação
3. Permissões
4. Throttling

**Quando sobrescrever:**
- Exemplo: Registrar métricas antes das verificações de segurança
```python
def initial(self, request, *args, **kwargs):
    start_time = time.time()
    super().initial(request, *args, **kwargs)
    log_request_time(request.method, time.time() - start_time)
```

### perform_create() vs create()
**Diferença crucial:**
- `create()`: Gerencia todo o fluxo (validação, resposta)
- `perform_create()`: Hook focado na lógica pré-save

**Boas práticas:**
```python
def create(self, request, *args, **kwargs):
    # Não sobrescreva a menos que precise mudar o fluxo COMPLETO
    return super().create(request, *args, **kwargs)

def perform_create(self, serializer):
    # Local ideal para adicionar dados ao objeto antes do save
    user = self.request.user
    serializer.save(created_by=user, updated_by=user)
```

## Arquitetura em Camadas - Explicação Detalhada

### 1. Models (Entidades de Dados)
```python
# apps/books/models/book.py
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100, unique=True)  # Garante nomes únicos

    def __str__(self):
        return self.name

class Book(models.Model):
    title = models.CharField(max_length=255)
    author = models.CharField(max_length=255)
    category = models.ForeignKey(
        Category,
        on_delete=models.PROTECT,  # Impede exclusão de categoria com livros
        related_name="books"
    )
    published_date = models.DateField(null=True, blank=True)

    class Meta:
        unique_together = ('title', 'author')  # Combinação única título-autor

    def __str__(self):
        return f"{self.title} by {self.author}"
```

### 2. Repositories (Acesso a Dados)
```python
# apps/books/repositories/book_repository.py
from apps.books.models.book import Book

def get_book_by_title_and_author(title: str, author: str) -> Book | None:
    """Consulta case-insensitive com otimização para evitar duplicatas"""
    return Book.objects.filter(
        title__iexact=title.strip(),  # Remove espaços e ignora caixa
        author__iexact=author.strip()
    ).first()

# apps/books/repositories/category_repository.py
from apps.books.models.book import Category

def get_category_by_name(name: str) -> Category | None:
    """Busca categoria com pré-carregamento de relacionamentos"""
    return Category.objects.filter(
        name__iexact=name.strip()
    ).prefetch_related('books').first()
```

### 3. Services (Lógica de Negócio)
```python
# apps/books/services/book_service.py
from rest_framework.exceptions import ValidationError
from rest_framework import status

def validate_unique_book(title: str, author: str) -> None:
    """Validação reutilizável que pode ser usada em múltiplos endpoints"""
    existing = get_book_by_title_and_author(title, author)
    if existing:
        raise ValidationError(
            {
                "error": "DUPLICATE_BOOK",
                "message": f"Book '{title}' by {author} already exists."
            },
            code=status.HTTP_400_BAD_REQUEST
        )

def get_or_create_category(name: str) -> Category:
    """Padrão comum para evitar duplicatas acidentais em categorias"""
    name = name.strip().title()  # Normaliza o nome
    category, created = Category.objects.get_or_create(
        name=name,
        defaults={'name': name}
    )
    return category
```

### 4. Serializers (Validação e Transformação de Dados)
```python
# apps/books/serializers/book_serializer.py
from rest_framework import serializers

class BookSerializer(serializers.ModelSerializer):
    category = serializers.SlugRelatedField(
        slug_field='name',
        queryset=Category.objects.all(),
        help_text="Nome da categoria (ex: 'Ficção Científica')"
    )

    class Meta:
        model = Book
        fields = '__all__'
        extra_kwargs = {
            'published_date': {'required': False}
        }

    def validate_title(self, value):
        """Validação customizada no nível do serializer"""
        if len(value) < 2:
            raise serializers.ValidationError("Title must be at least 2 characters long.")
        return value.strip()
```

### 5. Views (Camada de Apresentação)
```python
# apps/books/views/books_controller.py
class BookViewSet(ModelViewSet):
    serializer_class = BookSerializer
    pagination_class = PageNumberPagination
    
    def get_queryset(self):
        """Filtragem básica para otimização de queries"""
        return Book.objects.select_related('category').order_by('-id')

    def perform_create(self, serializer):
        """Fluxo completo de criação com validação de negócio"""
        data = serializer.validated_data
        validate_unique_book(data['title'], data['author'])
        
        category = get_or_create_category(data['category'].name)
        serializer.save(category=category)

    @action(detail=True, methods=['post'])
    def publish(self, request, pk=None):
        """Exemplo de ação customizada"""
        book = self.get_object()
        book.publish()
        return Response({'status': 'published'})
```

### 6. Rotas (Configuração de URLs)
```python
# apps/books/urls.py
from rest_framework.routers import DefaultRouter

router = DefaultRouter(trailing_slash=False)  # URLs sem / no final
router.register(r'books', BookViewSet)

urlpatterns = [
    path('api/v1/', include(router.urls)),
]
```

## Diagrama de Fluxo de Requisição

```
Requisição HTTP → Dispatch → Initial → Método HTTP (GET/POST/etc.)
    → get_queryset() → filter_queryset() → paginate_queryset()
    → get_serializer() → Validação → perform_create/update()
    → Resposta HTTP
```

## Boas Práticas Explicadas

1. **Separação de Responsabilidades:**
   - **Models:** Apenas estrutura de dados
   - **Views:** Orquestração do fluxo
   - **Serializers:** Validação e transformação de dados
   - **Services:** Regras de negócio complexas
   - **Repositories:** Acesso a dados complexo

2. **Vantagens da Arquitetura:**
   - Testes unitários isolados
   - Reúso de código entre diferentes endpoints
   - Facilidade de manutenção
   - Menor acoplamento entre componentes

3. **Performance:**
   - Use `select_related` e `prefetch_related` em `get_queryset()`
   - Cache de queries frequentes nos repositories
   - Paginação para listagens grandes

4. **Segurança:**
   - Sempre use `validated_data` ao invés de `request.data`
   - Permissões específicas em cada ViewSet
   - Validação em múltiplas camadas (serializer + service)

## Erros Comuns e Soluções

**Problema:** Dados duplicados mesmo com unique_together
**Solução:** Usar `iexact` nas consultas e normalizar dados antes da validação

**Problema:** Queries complexas em views
**Solução:** Movar para repositories com métodos especializados

**Problema:** Serializers muito grandes
**Solução:** Usar serializers diferentes para criação/atualização
```python
def get_serializer_class(self):
    if self.action == 'create':
        return CreateBookSerializer
    return BookSerializer
```