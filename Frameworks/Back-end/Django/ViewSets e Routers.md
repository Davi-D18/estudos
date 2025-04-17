# Guia Prático: ViewSets e Routers no Django REST Framework

## 1. O que são ViewSets e Routers?

**ViewSets** são classes que agrupam todas as operações CRUD (Create, Retrieve, Update, Delete) de um recurso em um único local. Em vez de criar views separadas para cada ação (como `UserList` e `UserDetail`), você define métodos como `list()`, `retrieve()`, `create()`, etc., em uma única classe.

**Routers** automatizam a criação de URLs para seus ViewSets, gerando rotas padrão como `/users/` (GET/POST) e `/users/1/` (GET/PUT/DELETE), seguindo convenções REST.

---

## 2. Passo a Passo: Implementando um ModelViewSet

### Passo 1: Criar um ModelViewSet Básico
```python
# views.py
from rest_framework import viewsets
from .models import Produto
from .serializers import ProdutoSerializer

class ProdutoViewSet(viewsets.ModelViewSet):
    queryset = Produto.objects.all()
    serializer_class = ProdutoSerializer
```

### Passo 2: Registrar no Router
```python
# urls.py
from rest_framework.routers import DefaultRouter
from .views import ProdutoViewSet

router = DefaultRouter()
router.register(r'produtos', ProdutoViewSet, basename='produto')

urlpatterns = router.urls
```

**Endpoints Gerados Automaticamente:**
- `GET /produtos/`: Lista todos os produtos
- `POST /produtos/`: Cria um novo produto
- `GET /produtos/1/`: Detalhes de um produto
- `PUT /produtos/1/`: Atualiza totalmente um produto
- `PATCH /produtos/1/`: Atualiza parcialmente um produto
- `DELETE /produtos/1/`: Exclui um produto

---

## 3. Restringindo Métodos HTTP

Para permitir apenas métodos específicos (ex: apenas GET e POST):

### Opção 1: Usar `http_method_names`
```python
class ProdutoViewSet(viewsets.ModelViewSet):
    queryset = Produto.objects.all()
    serializer_class = ProdutoSerializer
    http_method_names = ['get', 'post']  # Bloqueia PUT, PATCH, DELETE
```

### Opção 2: Sobrescrever Métodos
```python
class ProdutoViewSet(viewsets.ModelViewSet):
    queryset = Produto.objects.all()
    serializer_class = ProdutoSerializer

    def update(self, request, *args, **kwargs):
        return Response(status=405)  # Retorna erro 405 para PUT/PATCH

    def destroy(self, request, *args, **kwargs):
        return Response(status=405)  # Retorna erro 405 para DELETE
```

---

## 4. Adicionando Validações Customizadas

### Validação no Serializer
```python
# serializers.py
from rest_framework import serializers

class ProdutoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Produto
        fields = '__all__'

    def validate_preco(self, value):
        if value < 0:
            raise serializers.ValidationError("Preço não pode ser negativo!")
        return value
```

### Validação na ViewSet (Exemplo: Criar Produto)
```python
class ProdutoViewSet(viewsets.ModelViewSet):
    # ...

    def perform_create(self, serializer):
        # Verifica se o usuário tem permissão para criar
        if not self.request.user.is_staff:
            raise PermissionDenied("Apenas administradores podem criar produtos.")
        serializer.save()
```

---

## 5. Ações Customizadas com `@action`

Crie endpoints extras além do CRUD padrão:

### Exemplo: Ativar/Desativar Produto
```python
from rest_framework.decorators import action
from rest_framework.response import Response

class ProdutoViewSet(viewsets.ModelViewSet):
    # ...

    @action(detail=True, methods=['post'])
    def ativar(self, request, pk=None):
        produto = self.get_object()
        produto.ativo = True
        produto.save()
        return Response({'status': 'Produto ativado'})

    @action(detail=True, methods=['post'])
    def desativar(self, request, pk=None):
        produto = self.get_object()
        produto.ativo = False
        produto.save()
        return Response({'status': 'Produto desativado'})
```

**Endpoints Gerados:**
- `POST /produtos/1/ativar/`
- `POST /produtos/1/desativar/`

---

## 6. Controlando Permissões

Defina quem pode acessar cada ação:

```python
from rest_framework import permissions

class ProdutoViewSet(viewsets.ModelViewSet):
    queryset = Produto.objects.all()
    serializer_class = ProdutoSerializer

    # Permissão global para a ViewSet
    permission_classes = [permissions.IsAuthenticated]

    # Permissão específica para uma ação
    def get_permissions(self):
        if self.action == 'list':
            return [permissions.AllowAny()]  # Todos podem listar
        return [permissions.IsAdminUser()]   # Apenas admins para outras ações
```

---

## 7. Exemplo Completo: ViewSet Personalizado

```python
from rest_framework import viewsets, status
from rest_framework.response import Response

class ProdutoViewSet(viewsets.ModelViewSet):
    queryset = Produto.objects.all()
    serializer_class = ProdutoSerializer
    http_method_names = ['get', 'post', 'delete']  # Bloqueia PUT e PATCH

    @action(detail=False, methods=['get'])
    def baratos(self, request):
        produtos = Produto.objects.filter(preco__lt=100)
        serializer = self.get_serializer(produtos, many=True)
        return Response(serializer.data)

    def perform_destroy(self, instance):
        if instance.quantidade_estoque > 0:
            return Response(
                {"erro": "Produto com estoque não pode ser excluído."},
                status=status.HTTP_400_BAD_REQUEST
            )
        instance.delete()
```

---

## 8. Configurando Rotas Customizadas

Para ações que não seguem o padrão `/produtos/{pk}/action/`:

```python
# urls.py
from django.urls import path
from rest_framework.routers import DefaultRouter
from .views import ProdutoViewSet

router = DefaultRouter()
router.register(r'produtos', ProdutoViewSet)

urlpatterns = [
    path('produtos/em-falta/', ProdutoViewSet.as_view({'get': 'list_em_falta'})),
] + router.urls
```

---

## 9. Quando Não Usar ViewSets?

- **APIs não-CRUD:** Se seu endpoint não segue operações padrão (ex: processamento complexo).
- **Controle total sobre URLs:** Quando você precisa de rotas fora do padrão REST.
- **Projetos pequenos:** Se a abstração de ViewSets/Routers complica mais do que ajuda.

---

## 10. Melhores Práticas

1. **Use `ModelViewSet` para CRUD completo.**
2. **Prefira `ReadOnlyModelViewSet` para dados somente leitura.**
3. **Documente ações customizadas** com `@action(detail=True/False, methods=[...])`.
4. **Teste todas as ações** usando a ferramenta de teste do DRF ou Postman.

---

## Conclusão

ViewSets e Routers simplificam drasticamente o desenvolvimento de APIs RESTful no Django, reduzindo código repetitivo e garantindo consistência. Comece com as classes base (`ModelViewSet`, `ReadOnlyModelViewSet`) e personalize conforme necessidade usando métodos sobrescritos, decoradores `@action` e controle de permissões.