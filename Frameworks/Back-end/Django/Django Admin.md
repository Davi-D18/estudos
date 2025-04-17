## O que é o Django Admin?

Django Admin é um Painel Administrativo, uma interface pré-construída que permite aos administradores do sistema gerenciar e visualizar facilmente os dados da aplicação, sem que você precise escrever código adicional para criar painéis de controle personalizados.

## Por que Usar o Django Admin?

- Produtividade
- Interface amigável e pronta para uso
- Customização completa
- Segurança e estrutura de autenticação e permissões

## Quando utilizar Django Admin?

- Administração interna
- Prototipagem rápida
- Sistemas de suporte
- Sistemas de backoffice e gestão em geral
- Gestão de conteúdos de sites e blogs


## Vamos praticar

Criaremos um projeto Django para cadastro de produtos utilizando apenas os recursos do Django Admin, e também personalizar a interface com algumas bibliotecas de UI.

Repositótio do projeto: [https://github.com/pycodebr/sgp](https://github.com/pycodebr/sgp)

admin.py:
```python
from django.contrib import admin
from .models import Brand, Category, Product


@admin.register(Brand)
class BrandAdmin(admin.ModelAdmin):
    list_display = ('name', 'is_active', 'description', 'created_at', 'updated_at')
    search_fields = ('name',)
    list_filter = ('is_active',)


@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display = ('name', 'is_active', 'description', 'created_at', 'updated_at')
    search_fields = ('name',)
    list_filter = ('is_active',)


@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ('title', 'brand', 'category', 'price',
                    'is_active', 'created_at', 'updated_at')
    search_fields = ('title', 'brand__name', 'category__name')
    list_filter = ('is_active', 'brand', 'category')

```

- `@admin.register(Tabela)`:  Registra uma tabela nova no painel admin
- `list_display`: Exibe os campos informados no painel admin
- `search_fields`: Permite fazer buscas pelos campos especificados na tupla
- `list_filter`: Filtra os dados com base em uma coluna que colocar

Em tabelas que tem relações com outras, para fazer um filtro basta colocar o nome da tabela `__` e o nome da coluna que quer acessar, exemplo:

```python
class ProductAdmin(admin.ModelAdmin):
    list_display = ('title', 'brand', 'category', 'price',
                    'is_active', 'created_at', 'updated_at')
    search_fields = ('title', 'brand__name', 'category__name')
    # brand => tabela
    # name => campo da tabela name
    list_filter = ('is_active', 'brand', 'category')
```

## Criando actions
```python
import csv
from django.http import HttpResponse
from django.contrib import admin
from .models import Brand, Category, Product


@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ('title', 'brand', 'category', 'price',
                    'is_active', 'created_at', 'updated_at')
    search_fields = ('title', 'brand__name', 'category__name')
    list_filter = ('is_active', 'brand', 'category')

    def export_to_csv(self, request, queryset):
        response = HttpResponse(content_type='text/csv')
        response['Content-Disposition'] = 'attachment; filename="products.csv"'
        writer = csv.writer(response)
        writer.writerow(['título', 'marca', 'categoria', 'preço',
                         'ativo', 'descrição', 'criado em', 'atualizado em'])
        for product in queryset:
            writer.writerow([product.title, product.brand.name,                                             product.category.name,
                             product.price, product.is_active,                                              product.description,
                             product.created_at, product.updated_at])
        return response

    export_to_csv.short_description = 'Exportar para CSV'
    actions = [export_to_csv]

```

Adicione uma função dentro da classe e em seguida crie uma ação. Após isso, use o `export_to_csv.short_description` para adicionar uma descrição para a função (que será exibida no painel de admin em ações) e registre a ação em `actions = []`

## Site com ferramentas para Django
consulte em: [Django](https://djangopackages.org)

### Django Jazzmin
[Link]([https://django-jazzmin.readthedocs.io/](https://django-jazzmin.readthedocs.io/))

Instalação

```bash
pip install django-jazzmin
```

_core/settings.py_

```python
INSTALLED_APPS = [
    'jazzmin',

    'django.contrib.admin',
    ...
]
```

Algumas personalizações

```python
JAZZMIN_SETTINGS = {
    # title of the window (Will default to current_admin_site.site_title if absent or None)
    'site_title': 'SGP',

    # Title on the login screen (19 chars max) (defaults to current_admin_site.site_header if absent or None)
    'site_header': 'SGP',

    # Title on the brand (19 chars max) (defaults to current_admin_site.site_header if absent or None)
    'site_brand': 'SGP',

    'icons': {
        'auth': 'fas fa-users-cog',
        'auth.user': 'fas fa-user',
        'auth.Group': 'fas fa-users',
        'products.Brand': 'fas fa-copyright',
        'products.Category': 'fas fa-object-group',
        'products.Product': 'fas fa-box',
    },

    # Welcome text on the login screen
    'welcome_sign': 'Bem-vindo(a) ao SGP',

    # Copyright on the footer
    'copyright': 'PycodeBR LTDA',

    # List of model admins to search from the search bar, search bar omitted if excluded
    # If you want to use a single search field you dont need to use a list, you can use a simple string 
    'search_model': ['products.Product',],

    # Whether to show the UI customizer on the sidebar
    'show_ui_builder': True,
}
```

Biblioteca de ícones em [https://fontawesome.com/icons](https://fontawesome.com/icons)

Mais personalizações usando o UI Builder

```python
JAZZMIN_UI_TWEAKS = {
    'navbar_small_text': False,
    'footer_small_text': False,
    'body_small_text': False,
    'brand_small_text': False,
    'brand_colour': False,
    'accent': 'accent-primary',
    'navbar': 'navbar-white navbar-light',
    'no_navbar_border': False,
    'navbar_fixed': False,
    'layout_boxed': False,
    'footer_fixed': False,
    'sidebar_fixed': False,
    'sidebar': 'sidebar-dark-primary',
    'sidebar_nav_small_text': False,
    'sidebar_disable_expand': False,
    'sidebar_nav_child_indent': False,
    'sidebar_nav_compact_style': False,
    'sidebar_nav_legacy_style': False,
    'sidebar_nav_flat_style': False,
    'theme': 'minty',
    'dark_mode_theme': None,
    'button_classes': {
        'primary': 'btn-outline-primary',
        'secondary': 'btn-outline-secondary',
        'info': 'btn-info',
        'warning': 'btn-warning',
        'danger': 'btn-danger',
        'success': 'btn-success'
    }
}
```

### Dica extra

Pode-se alterar as urls do admin para se tornarem as urls principais do sistema

_core/urls.py_

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('', admin.site.urls),
]

```

Link para o notion: [Notion](https://pickle-reading-bd9.notion.site/py_live-013-03bf8be134a64551b76d9410c0ddadfb)
