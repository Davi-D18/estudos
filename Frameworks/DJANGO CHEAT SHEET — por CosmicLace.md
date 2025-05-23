#### **MODELS (MODELOS)**  

#### **O que são Models?**  
Models (Modelos) são classes em Python que definem a estrutura do seu banco de dados. Cada classe de modelo representa uma tabela no banco de dados, e cada atributo representa um campo nessa tabela. O **ORM** (*Object-Relational Mapper*) do Django faz a tradução entre objetos Python e registros do banco de dados.  

---

#### **Normalização de Banco de Dados & Chaves Estrangeiras**  
A normalização de banco de dados é o processo de organizar um banco relacional para **reduzir redundância** e **melhorar a integridade dos dados**. Envolve dividir tabelas grandes em tabelas menores e relacionadas, definindo relações entre elas.  

**Principais benefícios:**  
- Elimina duplicação de dados  
- Evita anomalias em atualizações  
- Garante consistência dos dados  
- Melhora desempenho em consultas (na maioria dos casos)  

**Formas de normalização:**  
- **1NF**: Elimina grupos repetidos, criando tabelas separadas para dados relacionados.  
- **2NF**: Remove dependências parciais (atributos que dependem apenas de parte da chave primária).  
- **3NF**: Remove dependências transitivas (atributos que dependem de outros não-chave).  

**Chaves estrangeiras** são o mecanismo que implementa essas relações:  
- Uma chave estrangeira é um campo (ou conjunto de campos) em uma tabela que referencia a chave primária de outra tabela.  
- Elas garantem **integridade referencial** (evitam registros "órfãos").  

No Django, os campos `ForeignKey`, `ManyToManyField` e `OneToOneField` criam essas relações:  

---

### **1. Exemplo de `ForeignKey` (Muitos-para-Um)**  
```python
# models.py
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)
    bio = models.TextField()
    def __str__(self):
        return self.name

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')
    published_date = models.DateField()
    def __str__(self):
        return self.title

# Uso:
# Criar um autor e vários livros
author = Author.objects.create(name="J.K. Rowling")
Book.objects.create(title="Harry Potter 1", author=author, published_date="1997-06-26")
Book.objects.create(title="Harry Potter 2", author=author, published_date="1998-07-02")

# Consultar objetos relacionados
author = Author.objects.get(name="J.K. Rowling")
author_books = author.books.all()  # Acessa livros via related_name
```

---

### **2. Exemplo de `ManyToManyField` (Muitos-para-Muitos)**  
```python
# models.py
class Tag(models.Model):
    name = models.CharField(max_length=50)
    def __str__(self):
        return self.name

class Article(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    tags = models.ManyToManyField(Tag, related_name='articles')
    def __str__(self):
        return self.title

# Uso:
# Criar tags e artigos
python_tag = Tag.objects.create(name="Python")
django_tag = Tag.objects.create(name="Django")
article = Article.objects.create(title="Django ORM Tips")

# Adicionar relações
article.tags.add(python_tag, django_tag)

# Consultar
django_articles = django_tag.articles.all()
article_tags = article.tags.all()
```

---

### **3. Exemplo de `OneToOneField` (Um-para-Um)**  
```python
# models.py
class User(models.Model):
    username = models.CharField(max_length=100)
    email = models.EmailField()
    def __str__(self):
        return self.username

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name='profile')
    bio = models.TextField(blank=True)
    birth_date = models.DateField(null=True, blank=True)
    avatar = models.ImageField(upload_to='avatars/', null=True, blank=True)
    def __str__(self):
        return f"Perfil de {self.user.username}"

# Uso:
# Criar usuário e perfil
user = User.objects.create(username="johndoe", email="john@example.com")
Profile.objects.create(user=user, bio="Desenvolvedor Python e blogueiro")

# Acessar objetos relacionados
user = User.objects.get(username="johndoe")
user_bio = user.profile.bio  # Acessa perfil via related_name
profile = Profile.objects.get(user__username="johndoe")
username = profile.user.username  # Acessa usuário a partir do perfil
```

---

### **Definindo Models (Campos Comuns)**  
```python
from django.db import models
from django.utils import timezone

class Book(models.Model):
    # Campos básicos
    title = models.CharField(max_length=200)
    subtitle = models.CharField(max_length=200, blank=True, null=True)
    description = models.TextField(help_text="Descrição completa do livro")
    page_count = models.IntegerField(default=0)
    price = models.DecimalField(max_digits=6, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)  # Definido na criação
    updated_at = models.DateTimeField(auto_now=True)  # Atualizado a cada save()

    # Relacionamentos
    author = models.ForeignKey('Author', on_delete=models.CASCADE, related_name='books')
    co_authors = models.ManyToManyField('Author', related_name='co_authored_books')

    # Campos de escolha (choices)
    GENRE_CHOICES = [
        ('FIC', 'Ficção'),
        ('NON', 'Não-Ficção'),
        ('SCI', 'Ficção Científica'),
        ('MYS', 'Mistério'),
    ]
    genre = models.CharField(max_length=3, choices=GENRE_CHOICES, default='FIC')

    # Outros campos úteis
    isbn = models.CharField(max_length=13, unique=True)
    cover_image = models.ImageField(upload_to='covers/', blank=True)

    class Meta:
        ordering = ['-published_date']  # Ordenação padrão
        
	constraints = [
	    models.UniqueConstraint(fields=['title', 'author'],                              name='unique_book_per_author')
	]
	
	verbose_name = 'Livro'  # Nome singular no admin
	verbose_name_plural = 'Livros'  # Nome plural no admin
	
	def __str__(self):
	    return self.title  # Representação em string do objeto
	
	def save(self, **kwargs):
	    # Comportamento personalizado no save()
	    if not self.slug:
	        self.slug = slugify(self.title)
	    super().save(**kwargs)
	
	def get_absolute_url(self):
	    from django.urls import reverse
	    return reverse('book-detail', args=[str(self.id)])  # URL para detalhes do livro
	
	def is_recent(self):
	    # Verifica se o livro foi publicado nos últimos 30 dias
	    return self.published_date >= timezone.now().date() -                            timezone.timedelta(days=30)
```

---

### **TIPOS DE CAMPOS (FIELD TYPES)**

#### **Campos de Texto**
- `CharField`: String com tamanho máximo.
- `TextField`: Texto sem limite de tamanho.
- `SlugField`: String amigável para URLs.
- `EmailField`: Valida formato de e-mail.
- `URLField`: Valida formato de URL.
- `FilePathField`: Seleciona arquivos de um diretório.

#### **Campos Numéricos**
- `IntegerField`: Números inteiros.
- `PositiveIntegerField`: Inteiros positivos.
- `FloatField`: Números decimais.
- `DecimalField`: Decimais com precisão fixa.

#### **Campos Booleanos**
- `BooleanField`: `True`/`False`.
- `NullBooleanField`: `True`/`False`/`None`.

#### **Campos de Data/Hora**
- `DateField`: Data.
- `DateTimeField`: Data e hora.
- `DurationField`: Períodos de tempo.

#### **Campos Especiais**
- `BinaryField`: Dados binários.
- `FileField`: Upload de arquivo.
- `ImageField`: Upload de imagem (com validação).
- `UUIDField`: Armazena UUIDs.
- `JSONField`: Armazena dados JSON.

---

### **RELACIONAMENTOS EM DETALHE**

#### **1. `ForeignKey` (Muitos-para-Um)**
- **Uso básico**:
  ```python
  author = models.ForeignKey('Author', on_delete=models.CASCADE)
  ```
- **`on_delete` options**:
  - `CASCADE`: Apaga o livro se o autor for apagado.
  - `PROTECT`: Impede a exclusão do autor se houver livros.
  - `SET_NULL`: Define como `NULL` (requer `null=True`).

- **Auto-relacionamento**:
  ```python
  parent_chapter = models.ForeignKey('self', on_delete=models.CASCADE, null=True)
  ```

#### **2. `ManyToManyField` (Muitos-para-Muitos)**
- **Uso básico**:
  ```python
  tags = models.ManyToManyField('Tag', related_name='books')
  ```
- **Com modelo intermediário** (para campos extras):
  ```python
  class BookAuthor(models.Model):
      book = models.ForeignKey('Book', on_delete=models.CASCADE)
      author = models.ForeignKey('Author', on_delete=models.CASCADE)
      contribution_percentage = models.IntegerField(default=100)
  ```

#### **3. `OneToOneField` (Um-para-Um)**
- **Extendendo um modelo**:
  ```python
  class BookDetail(models.Model):
      book = models.OneToOneField('Book', on_delete=models.CASCADE, primary_key=True)
      first_published = models.DateField(null=True)
  ```

---

### **HERANÇA DE MODELOS**

#### **1. Classes Abstratas**
- **Não cria tabela no banco**:
  ```python
  class BaseItem(models.Model):
      title = models.CharField(max_length=100)
      class Meta:
          abstract = True
  ```

#### **2. Herança Multi-tabela**
- **Cria tabelas separadas**:
  ```python
  class Book(Product):  # Herda campos de Product
      author = models.CharField(max_length=100)
  ```

#### **3. Proxy Models**
- **Altera comportamento sem alterar o banco**:
  ```python
  class RecentBook(Book):
      class Meta:
          proxy = True
      def is_recent(self):
          return self.published_date >= timezone.now() - timedelta(days=30)
  ```

#### **Método `get_recent` (Personalizado)**
```python
@classmethod
def get_recent(cls):
    # Retorna livros publicados nos últimos 30 dias
    return cls.objects.filter(
        published_date__gte=timezone.now().date() - timezone.timedelta(days=30)
    )
```

#### **Classe `Meta` (Configurações Avançadas)**
```python
class Book(models.Model):
    # Campos do modelo...
    class Meta:
        db_table = 'bookstore_books'  # Nome personalizado da tabela no banco
        ordering = ['-published_date', 'title']  # Ordenação padrão
        constraints = [
            # Garante combinação única de título e autor
            models.UniqueConstraint(fields=['title', 'author'],                              name='unique_book_author'),
            # Valida preço positivo
            models.CheckConstraint(check=models.Q(price__gt=0),                              name='positive_price')
        ]
        indexes = [
            models.Index(fields=['title']),  # Índice no campo 'title'
            models.Index(fields=['author', 'genre'], name='author_genre_idx')  # Índice composto
        ]
        permissions = [
            ('publish_book', 'Pode publicar livro'),
            ('feature_book', 'Pode destacar livro')
        ]
        verbose_name = 'Livro'  # Nome singular no admin
        verbose_name_plural = 'Livros'  # Nome plural
```

---

### **MÉTODOS COMUNS EM MODELOS**
```python
class Book(models.Model):
    # Campos do modelo...

    # Representação em string
    def __str__(self):
        return self.title

    # Gera URL para detalhes do livro
    def get_absolute_url(self):
        from django.urls import reverse
        return reverse('book-detail', args=[str(self.id)])

    # Comportamento personalizado ao salvar
    def save(self, **kwargs):
        if not self.slug:
            self.slug = slugify(self.title)
        super().save(**kwargs)

    # Lógica de negócio
    def is_on_sale(self):
        return self.discount_percent > 0

    def get_discount_price(self):
        return self.price * (1 - self.discount_percent / 100) 
        if self.is_on_sale() else self.price
```

---

### **MANAGERS PERSONALIZADOS**
```python
class BookManager(models.Manager):
    # QuerySet padrão com otimização
    def get_queryset(self):
        return super().get_queryset().select_related('author')

    # Filtra livros publicados
    def published(self):
        return self.filter(published=True)

    # Filtra best-sellers
    def bestsellers(self):
        return self.filter(is_bestseller=True)

class Book(models.Model):
    # Campos do modelo...
    objects = BookManager()  # Substitui o manager padrão
    published_books = BookManager().published()  # Manager adicional
```

**Uso:**
```python
Book.objects.published()  # Todos os livros publicados
Book.bestsellers.all()  # Todos os best-sellers
```

---

### **QUERYSETS: CONSULTAS AO BANCO**

#### **Criação de QuerySets**
```python
all_books = Book.objects.all()  # Query não executada ainda
first_book = Book.objects.first()  # Executa a query
book_count = Book.objects.count()  # Executa a query
```

#### **Filtros**
```python
# Filtros básicos
fiction_books = Book.objects.filter(genre='fiction')
recent_books = Book.objects.filter(published_date__gte='2023-01-01')

# Lookups avançados
from django.db.models import Q
books = Book.objects.filter(
    Q(genre='fiction') | Q(genre='non-fiction'),  # OR
    ~Q(price__gt=50),  # NOT
    Q(published_date__year=2023)
)

# Filtros por relacionamento
rowling_books = Book.objects.filter(author__name='J.K. Rowling')
```

#### **Lookups Comuns**
| Lookup | Exemplo | Descrição |
|--------|---------|-----------|
| `__exact` | `title__exact='Harry'` | Match exato (case-sensitive) |
| `__iexact` | `title__iexact='harry'` | Match exato (case-insensitive) |
| `__contains` | `title__contains='Potter'` | Contém substring |
| `__gt`/`__lt` | `price__gt=20` | Maior/menor que |
| `__in` | `genre__in=['fiction', 'fantasy']` | Está em uma lista |
| `__isnull` | `author__isnull=True` | É nulo |

#### **Ordenação e Paginação**
```python
# Ordenação
books = Book.objects.order_by('-price', 'title')  # Preço decrescente, título crescente

# Paginação
page_number = 3
page_size = 10
page = Book.objects.all()[(page_number-1)*page_size : page_number*page_size]
```

---

### **AGRAGAÇÃO E ANOTAÇÃO**
```python
from django.db.models import Count, Avg, F

# Estatísticas agregadas
stats = Book.objects.aggregate(
    avg_price=Avg('price'),
    total_stock=Sum('stock')
)

# Anotação (campos calculados)
books = Book.objects.annotate(
    discounted_price=F('price') * 0.9
)

# Agrupamento
genre_counts = Book.objects.values('genre').annotate(count=Count('id'))
# Resultado: [{'genre': 'fiction', 'count': 12}, ...]
```

---

### **OTIMIZAÇÃO DE QUERIES**
```python
# select_related (ForeignKey/OneToOne)
books = Book.objects.select_related('author')  # Evita N+1 queries

# prefetch_related (ManyToMany)
books = Book.objects.prefetch_related('tags')

# Campos adiados/deferidos
books = Book.objects.only('title', 'price')  # Busca apenas campos essenciais
```

---

### **EXPRESSÕES AVANÇADAS**
```python
from django.db.models import Subquery, OuterRef

# Subconsultas
long_books = Book.objects.filter(
    page_count__gt=Subquery(
        Book.objects.filter(id=OuterRef('id'))
        .values('page_count')
        .annotate(avg=Avg('page_count'))
        .values('avg')
    )
)
```

### **OPERAÇÕES EM MASSA (BULK OPERATIONS)**

#### **1. `bulk_create` (Criação em massa)**
```python
# Cria múltiplos livros de uma vez (mais eficiente que create() individual)
books_to_create = [
    Book(title="Livro 1", price=19.99, author_id=1),
    Book(title="Livro 2", price=24.99, author_id=1),
]
created_books = Book.objects.bulk_create(books_to_create)  # Retorna lista de objetos criados
```

#### **2. `bulk_update` (Atualização em massa)**
```python
# Atualiza preços de livros com desconto
books = Book.objects.filter(price__lt=20)
for book in books:
    book.price *= 1.1  # Aumento de 10%
Book.objects.bulk_update(books, ['price'])  # Campos a atualizar
```

#### **3. Atualização condicional com `Case`/`When`**
```python
from django.db.models import Case, When, Value

# Marca livros como "destaque" se forem best-sellers ou tiverem rating alto
Book.objects.update(
    featured=Case(
        When(bestseller=True, then=Value(True)),
        When(rating__gte=4.5, then=Value(True)),
        default=Value(False)
    )
)
```

---

### **SQL DIRETO (QUANDO NECESSÁRIO)**

#### **1. `raw()` (Consultas SQL brutas)**
```python
# Para queries complexas não suportadas pelo ORM
books = Book.objects.raw("""
    SELECT b.*, COUNT(r.id) as review_count
    FROM books_book b
    LEFT JOIN reviews_review r ON b.id = r.book_id
    GROUP BY b.id
    HAVING COUNT(r.id) > 5
""")
```

#### **2. Conexão direta com o banco**
```python
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute("UPDATE books_book SET featured = %s WHERE bestseller = %s", [True, True])
    cursor.execute("SELECT title FROM books_book WHERE price > %s", [20])
    expensive_books = [row[0] for row in cursor.fetchall()]
```

---

### **DICAS DE PERFORMANCE**

1. **Filtre no banco, não em Python**:
   ```python
   # Ruim (carrega todos os objetos):
   expensive_books = [b for b in Book.objects.all() if b.price > 20]
   
   # Bom (filtro no banco):
   expensive_books = Book.objects.filter(price__gt=20)
   ```

2. **Conte de forma eficiente**:
   ```python
   # Ruim:
   book_count = len(Book.objects.all())  # Carrega todos os objetos
   
   # Bom:
   book_count = Book.objects.count()  # Contagem no banco
   ```

3. **Use `values()` ou `values_list()` para campos específicos**:
   ```python
   # Ruim:
   titles = [book.title for book in Book.objects.all()]
   
   # Bom:
   titles = Book.objects.values_list('title', flat=True)
   ```

4. **Use `django-debug-toolbar` para otimizar queries**.

---

### **VIEWS (VISUALIZAÇÕES)**

#### **1. Function-Based Views (FBVs)**
```python
from django.shortcuts import render

def book_list(request):
    books = Book.objects.all()
    return render(request, 'books/list.html', {'books': books})
```

#### **2. Class-Based Views (CBVs)**
```python
from django.views.generic import ListView

class BookListView(ListView):
    model = Book
    template_name = 'books/list.html'
    context_object_name = 'books'
```

**Quando usar**:
- **FBVs**: Lógica customizada e simples.
- **CBVs**: Operações CRUD padrão (herdam de `CreateView`, `UpdateView`, etc.).

---

### **URLS (ROTEAMENTO)**

#### **1. Mapeamento básico**
```python
from django.urls import path
from .views import BookListView

urlpatterns = [
    path('', BookListView.as_view(), name='book-list'),
    path('books/<int:pk>/', BookDetailView.as_view(), name='book-detail'),
]
```

#### **2. Conversores de URL**
```python
path('books/<int:pk>/', views.book_detail),  # Inteiro
path('genre/<str:genre>/', views.genre_books),  # String
path('posts/<slug:slug>/', views.post_detail),  # Slug (amigável para URLs)
```

#### **3. URLs nomeadas**
```python
# Em views:
from django.urls import reverse
url = reverse('book-detail', args=[1])  # → '/books/1/'

# Em templates:
<a href="{% url 'book-detail' book.pk %}">Ver livro</a>
```

#### **4. Inclusão de URLs de apps**
```python
path('books/', include('books.urls', namespace='books'))
# Uso: {% url 'books:book-detail' pk=1 %}
```

### **TEMPLATES (TEMPLATES)**

#### **Linguagem de Templates**
Os templates do Django são projetados para serem **não Turing-completos** (seguros para editores não confiáveis), focando em exibição com lógica mínima.

```django
{% for book in books %}
  <h2>{{ book.title }}</h2>
{% endfor %}
```

#### **Principais Funcionalidades**
| Sintaxe | Descrição | Exemplo |
|---------|-----------|---------|
| `{{ var }}` | Exibe variável | `{{ book.title }}` |
| `{% if %}` | Condicional | `{% if book.price > 20 %}Caro{% endif %}` |
| `{% for %}` | Loop | `{% for book in books %}{{ book.title }}{% endfor %}` |
| `{% include %}` | Inclui outro template | `{% include "header.html" %}` |
| `{% extends %}` | Herança de template | `{% extends "base.html" %}` |
| `{{ var|filter }}` | Filtros | `{{ date|date:"d/m/Y" }}` |

#### **Herança de Templates**
```django
<!-- base.html -->
<html>
  <body>
    {% block content %}{% endblock %}
  </body>
</html>

<!-- child.html -->
{% extends "base.html" %}
{% block content %}
  <h1>Meu Conteúdo</h1>
{% endblock %}
```

---

### **FORMS (FORMULÁRIOS)**

#### **O que são?**
Classes Python que:
1. Renderizam HTML
2. Validam dados
3. Vinculam-se a modelos (ModelForms)

#### **Tipos de Formulários**
1. **`forms.Form`** (Formulário manual):
```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
```

2. **`forms.ModelForm`** (Vinculado a um modelo):
```python
from .models import Book

class BookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = ['title', 'author']  # Ou '__all__'
```

---

#### **Campos de Formulário Comuns**

| Campo | Descrição | Exemplo |
|-------|-----------|---------|
| `CharField` | Texto | `forms.CharField(max_length=100)` |
| `EmailField` | E-mail validado | `forms.EmailField()` |
| `DateField` | Data | `forms.DateField(widget=forms.DateInput(attrs={'type': 'date'}))` |
| `ChoiceField` | Seleção única | `forms.ChoiceField(choices=[('F', 'Ficção'), ('N', 'Não-Ficção')])` |
| `ModelChoiceField` | Seleção de QuerySet | `forms.ModelChoiceField(queryset=Author.objects.all())` |
| `FileField` | Upload de arquivo | `forms.FileField()` |

---

#### **Widgets (Controle de Renderização HTML)**
```python
title = forms.CharField(
    widget=forms.TextInput(attrs={
        'class': 'form-control',
        'placeholder': 'Título do livro'
    })
)
```

**Widgets Comuns:**
- `TextInput`: Campo de texto padrão.
- `Textarea`: Área de texto multilinha.
- `Select`: Dropdown.
- `CheckboxSelectMultiple`: Múltiplos checkboxes.

---

#### **Validação**
1. **Validação Automática** (por tipo de campo):
```python
if form.is_valid():  # Verifica todas as validações
    data = form.cleaned_data  # Dados sanitizados
```

2. **Validação Personalizada**:
```python
# Validação por campo
def clean_title(self):
    title = self.cleaned_data.get('title')
    if title.lower() == "untitled":
        raise forms.ValidationError("Escolha um título melhor!")
    return title

# Validação global
def clean(self):
    cleaned_data = super().clean()
    if cleaned_data.get('start_date') > cleaned_data.get('end_date'):
        raise forms.ValidationError("Data inicial não pode ser depois da final!")
```

---

#### **Validadores Incorporados**
```python
from django.core.validators import MinLengthValidator, EmailValidator

username = forms.CharField(
    validators=[MinLengthValidator(5, message="Mínimo 5 caracteres!")]
)
email = forms.EmailField(
    validators=[EmailValidator(message="E-mail inválido!")]
)
```

---

### **EXEMPLO COMPLETO (ModelForm)**
```python
class BookForm(forms.ModelForm):
    GENRE_CHOICES = [
        ('FIC', 'Ficção'),
        ('NON', 'Não-Ficção')
    ]
    
    genre = forms.ChoiceField(choices=GENRE_CHOICES)
    cover = forms.ImageField(required=False)

    class Meta:
        model = Book
        fields = ['title', 'author', 'genre', 'price', 'cover']
        widgets = {
            'title': forms.TextInput(attrs={'class': 'form-control'}),
            'price': forms.NumberInput(attrs={'step': '0.01'})
        }

    def clean_price(self):
        price = self.cleaned_data.get('price')
        if price <= 0:
            raise forms.ValidationError("Preço deve ser positivo!")
        return price
```

### **ADMIN (INTERFACE ADMINISTRATIVA)**

#### **Configuração Básica**
```python
from django.contrib import admin
from .models import Book

@admin.register(Book)
class BookAdmin(admin.ModelAdmin):
    list_display = ('title', 'author', 'published_date')  # Campos exibidos na lista
    search_fields = ('title', 'author__name')  # Campos pesquisáveis
    list_filter = ('genre', 'is_bestseller')  # Filtros laterais
```

#### **Boas Práticas**
- **Nunca** use para usuários finais (apenas equipe interna).
- Proteja com **autenticação de dois fatores (2FA)** e logs de auditoria.
- Restrinja acesso com permissões granulares.

---

### **SETTINGS (CONFIGURAÇÕES)**

#### **Configurações Essenciais**
```python
# settings.py
import os

DEBUG = False  # Sempre False em produção!
SECRET_KEY = os.environ.get('SECRET_KEY')  # Chave em variável de ambiente
ALLOWED_HOSTS = ['seusite.com']  # Domínios permitidos

# Banco de dados
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME'),
    }
}

# Arquivos estáticos e mídia
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')  # Para produção
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

#### **Segurança**
- Armazene segredos em `.env` ou ferramentas como **Vault**.
- Use `python-decouple` ou `django-environ` para gerenciar variáveis.

---

### **MIDDLEWARE**

#### **Funcionamento**
São camadas que processam **requests/responses** (ex: autenticação, CORS).

```python
# Exemplo de middleware customizado
class CustomHeaderMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        response = self.get_response(request)
        response['X-Custom-Header'] = 'Hello'
        return response
```

#### **Middlewares Comuns**
- `SecurityMiddleware`: Proteção contra ataques (ex: HTTPS).
- `SessionMiddleware`: Gerenciamento de sessões.
- `AuthenticationMiddleware`: Vincula usuários a requests.

---

### **AUTH (AUTENTICAÇÃO)**

#### **Sistema Padrão**
```python
from django.contrib.auth import authenticate, login, logout

# Login
user = authenticate(request, username='foo', password='bar')
if user:
    login(request, user)

# Custom User Model (recomendado!)
class User(AbstractUser):
    bio = models.TextField()
```

#### **Views Úteis**
- `LoginView`, `LogoutView`, `PasswordResetView` (já inclusas no Django).

---

### **SIGNALS (SINAIS)**

#### **Para que Servem?**
Notificam partes do sistema quando eventos ocorrem (ex: pós-salvamento de modelo).

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)
```

#### **Sinais Comuns**
| Sinal | Disparado Quando |
|-------|------------------|
| `pre_save` / `post_save` | Antes/depois de salvar um modelo |
| `pre_delete` / `post_delete` | Antes/depois de deletar um modelo |
| `m2m_changed` | Relação ManyToMany alterada |

---

### **TESTING (TESTES)**

#### **Exemplo Básico**
```python
from django.test import TestCase

class BookTests(TestCase):
    def test_book_creation(self):
        book = Book.objects.create(title="Django for Beginners")
        self.assertEqual(book.title, "Django for Beginners")

    def test_view_status_code(self):
        response = self.client.get('/books/')
        self.assertEqual(response.status_code, 200)
```

#### **Ferramentas**
- `TestCase`: Base para testes.
- `Client`: Simula requests HTTP.
- `factory_boy` ou `model_bakery`: Criam dados de teste.

---

### **MIGRATIONS (MIGRAÇÕES)**

#### **Comandos Chave**
| Comando | Uso |
|---------|-----|
| `makemigrations` | Cria migrações a partir de mudanças nos modelos |
| `migrate` | Aplica migrações pendentes |
| `showmigrations` | Lista migrações e status |
| `sqlmigrate` | Mostra SQL que será executado |

#### **Migrações de Dados**
```python
# 0002_populate_data.py
from django.db import migrations

def add_initial_books(apps, schema_editor):
    Book = apps.get_model('books', 'Book')
    Book.objects.create(title="Dom Quixote")

class Migration(migrations.Migration):
    dependencies = [('books', '0001_initial')]
    operations = [migrations.RunPython(add_initial_books)]
```

#### **Boas Práticas**
- **Sempre** teste migrações em ambiente de desenvolvimento.
- Para **zero-downtime**, garanta compatibilidade reversa.
- Use `--plan` para verificar o que será aplicado antes de migrar em produção.

### **DESAFIOS COMUNS (COMMON CHALLENGES)**

#### **1. Alterações em Tabelas Grandes**
- **Problema**: Migrações podem travar tabelas por muito tempo.
- **Solução**: Use `RunSQL` com comandos específicos do banco (ex: `ALTER TABLE` otimizado).

```python
# migrations/0002_large_table.py
from django.db import migrations

class Migration(migrations.Migration):
    dependencies = [('app', '0001_initial')]
    operations = [
        migrations.RunSQL(
            sql='ALTER TABLE app_large_table ADD COLUMN new_column INT DEFAULT 0;',
            reverse_sql='ALTER TABLE app_large_table DROP COLUMN new_column;'
        )
    ]
```

#### **2. Modificando Dados em Migrações**
- **Erro comum**: Importar o modelo diretamente (pode quebrar em migrações futuras).
- **Correto**: Use `apps.get_model()` para obter a versão histórica.

```python
def update_data(apps, schema_editor):
    Book = apps.get_model('app', 'Book')  # ✅ Versão histórica
    Book.objects.filter(price__lt=10).update(discount=True)
```

#### **3. Conflitos de Migração**
- **Causa**: Múltiplos desenvolvedores criam migrações simultaneamente.
- **Solução**: 
  - Comunique-se com a equipe.
  - Use `squashmigrations` para consolidar migrações.

```bash
python manage.py squashmigrations app_name 0001 0004
```

---

### **COMANDOS DE GERENCIAMENTO (MANAGEMENT COMMANDS)**

#### **Comandos Úteis**
| Comando | Descrição |
|---------|-----------|
| `runserver 0.0.0.0:8000` | Inicia servidor em todos os IPs |
| `createsuperuser` | Cria um usuário admin |
| `makemigrations` | Gera migrações para mudanças nos modelos |
| `migrate` | Aplica migrações pendentes |
| `shell_plus` | Shell interativo com modelos pré-carregados |
| `test` | Roda testes |
| `collectstatic` | Coleta arquivos estáticos para produção |

#### **Criando Comandos Customizados**
```python
# app/management/commands/hello.py
from django.core.management.base import BaseCommand

class Command(BaseCommand):
    help = 'Diz olá'

    def handle(self, *args, **options):
        self.stdout.write(self.style.SUCCESS('Olá, Django!'))
```
**Uso**:
```bash
python manage.py hello
```

---

### **PAGINAÇÃO (PAGINATION)**

#### **Implementação Básica**
```python
# views.py
from django.core.paginator import Paginator, EmptyPage, PageNotAnInteger

def book_list(request):
    queryset = Book.objects.all()
    paginator = Paginator(queryset, 10)  # 10 itens por página
    
    page = request.GET.get('page')
    try:
        books = paginator.page(page)
    except PageNotAnInteger:
        books = paginator.page(1)
    except EmptyPage:
        books = paginator.page(paginator.num_pages)
    
    return render(request, 'books/list.html', {'books': books})
```

#### **Template (HTML)**
```django
<!-- list.html -->
{% for book in books %}
  <h3>{{ book.title }}</h3>
{% endfor %}

<div class="pagination">
  {% if books.has_previous %}
    <a href="?page={{ books.previous_page_number }}">Anterior</a>
  {% endif %}
  
  <span>Página {{ books.number }} de {{ books.paginator.num_pages }}</span>
  
  {% if books.has_next %}
    <a href="?page={{ books.next_page_number }}">Próxima</a>
  {% endif %}
</div>
```

#### **Performance em Tabelas Grandes**
- **Problema**: `OFFSET` em queries grandes é lento.
- **Solução alternativa**: Paginação por cursor (usando IDs ou timestamps):
```python
# Paginação eficiente para +1M registros
last_id = request.GET.get('last_id')
books = Book.objects.filter(id__gt=last_id)[:10]
```

---

### **ESTRUTURA DE ARQUIVOS (PROJECT FILE STRUCTURE)**
```
projeto/
├── app/
│   ├── management/
│   │   └── commands/       # Comandos customizados
│   ├── migrations/         # Migrações do banco
│   ├── templates/          # Templates HTML
│   │   └── app/
│   │       └── list.html
│   ├── __init__.py
│   ├── admin.py            # Config do admin
│   ├── models.py           # Modelos do banco
│   ├── tests.py            # Testes
│   ├── urls.py             # URLs da app
│   └── views.py            # Lógica das views
├── projeto/
│   ├── settings.py         # Configurações
│   ├── urls.py             # URLs globais
│   └── wsgi.py             # Config WSGI
└── manage.py               # Script de gerenciamento
```

---

### **MELHORES PRÁTICAS**
1. **Migrações**:
   - Sempre teste migrações em staging antes de produção.
   - Para rollbacks, planeje migrações reversíveis.

2. **Paginação**:
   - Evite `SELECT *` em tabelas grandes. Use `.only()` para campos necessários.
   ```python
   Book.objects.only('title', 'price')[:10]
   ```

3. **Segurança**:
   - Nunca exponha `DEBUG=True` em produção.
   - Use variáveis de ambiente para segredos:
   ```python
   # settings.py
   SECRET_KEY = os.getenv('DJANGO_SECRET_KEY')
   ```

4. **Performance**:
   - Para APIs, considere Django REST Framework com `CursorPagination`.