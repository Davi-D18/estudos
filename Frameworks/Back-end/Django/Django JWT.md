Para usar autenticação por JWT no Django e django-rest-framework, basta instalar a seguinte lib:
```bash
pip install djangorestframework-simplejwt
```

Após isso, vá nas configurações do projeto e em `INSTALLED_APPS` adicione o `djangorestframework-simplejwt`:
```python
INSTALLED_APPS = {
	'rest_framework_simplejwt',
}
```

## Outras configurações
```python
from datetime import timedelta

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
    ),
}

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=5),
    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),
}

```

Em `rest_framework_simplejwt.authentication.JWTAuthentication`, `JWTAuthentication` é uma classe de autenticação que será usado por default em todas as rotas

`rest_framework.permissions.**IsAuthenticated**` indica que apenas os usuários logados terão acesso as rotas da API

## Configurando rotas
No arquivo `urls.py` em `core` , basta criar rotas e redirecionar elas para as classes já prontas da lib `djangorestframework-simplejwt`:
```python
from django.contrib import admin
from django.urls import path, include
from rest_framework_simplejwt import views as jwt_views

urlpatterns = [
    path('api/v1/token/', jwt_views.TokenObtainPairView.as_view(),
				name='token_obtain_pair'),
    path('api/v1/token/refresh/', jwt_views.TokenRefreshView.as_view(),
			    name='token_refresh'),
]

```

Quando o usuário for acessar a rota `api/v1/token` com o método POST e fornecendo o seguinte arquivo no corpo da requisição:
```json
{
	"username": "usuario",
	"password": "senha"
}
```

a API retornará 2 tokens, um com o **refresh** e o outro com o **token** 
	- **Refresh**: Esse token serve para dar refresh no token gerado, permitindo ficar mais tempo fazendo requisições, após o tempo de expirar, não será mais possível dar refresh, precisa gerar um novo token
		- Detalhe: Para dar certo o **refresh**, você precisa acessar a rota `api/v1/token/refresh/` usando o método POST e passando o token de refresh no corpo da requisição
	- **Token**: Aqui é o token gerado uado para se autenticar a API

Existe uma 3° rota que pode ser adicionada onde verifica se o Token gerado ainda está válido:
```python
from django.contrib import admin
from django.urls import path, include
from rest_framework_simplejwt import views as jwt_views

urlpatterns = [
    path('api/v1/verify/', jwt_views.TokenVerifyView.as_view(),
				name='token_verify'),
]
```

## Permissões
As classes de permissões prontas do DRF são:

- AllowAny

- IsAuthenticated

- IsAdminUser

- IsAuthenticatedOrReadOnly

- DjangoModelPermissions

- DjangoModelPermissionsOrAnonReadOnly

- DjangoObjectPermissions

Podemos usar DjangoModelPermissions como default

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
        'rest_framework.permissions.DjangoModelPermissions', # adicionar isso
    ),
}

```

Após configurado isso, basta entrar no painel de admin do Django e definir as permissões para cada usuário


> [!NOTE] Importante
> As permissões configuradas no **core** elas serão aplicadas globalmente

### Aplicando permissões diferentes para cada rota
Você pode definir uma rota com permissão personalizada, analise o exemplo:
```python
from rest_framework import viewsets, permissions # basta importar o permissions do rest_framework

class Brand(models.Model):
    name = models.CharField(max_length=100, verbose_name="Nome")
    description = models.TextField(null=True, blank=True, verbose_name="Descrição")
    created_at = models.DateTimeField(auto_now_add=True, verbose_name="Criado em")
    updated_at = models.DateTimeField(auto_now=True, verbose_name="Atualizado em")
    permission_classes = [permissions.AllowAny] # Usar como propriedade na classe
```


## Permissões Personalizadas
Caso não queira usar as permissões prontas do DRF ou adicionar permissões personalizadas, basta criar um arquivo `permissions.py` e nele usar uma estrutura como essa:

```python
from rest_framework import permissions # importa as permissions do DRF


class CarOwnerPermission(permissions.BasePermission): # Usa a classe base

	# Aqui se refere a rota em si, ao acessar a rota, essa função será chamada
	# Onde retorna apenas os carros que estão no nome do usuário
    def has_permission(self, request, view): 
        if view.action == 'list':
            view.queryset = view.queryset.filter(owner=request.user)
            return True
        return super().has_permission(request, view)

	# Se o usuário tentar modificar ou apagar um carro que está registrado no usuário dele, vai ser permitido, do contrário, não é permitido
    def has_object_permission(self, request, view, obj):
        return obj.owner == request.user

```

Depois, basta ir no controller/view e adicionar a Classe:
```python
from cars.permissions import CarOwnerPermission


class CarModelViewSet(viewsets.ModelViewSet):
    queryset = Car.objects.all()
    serializer_class = CarModelSerializer
    filter_backends = [RQLFilterBackend]
    rql_filter_class = CarFilterClass
    permission_classes = [permissions.DjangoModelPermissions, CarOwnerPermission,] 

```


> [!NOTE] Ordem das permissões
> Ao definir permissões em alguma rota seja personalizada ou não, a ordem é respeitada, exemplo:
> Aqui **permissions.DjangoModelPermissions** ele irá verificar primeiro as permissões padrão do Django, caso ele tenha permissão, ele vai verificar o  **CarOwnerPermission** se tiver acesso, ele é liberado

## Paginação
O DRF tem algumas classes de paginação prontas para utilizar:

- `PageNumberPagination`
    
    - O estilo **PageNumberPagination** aceita um único número de página nos parâmetros de consulta da solicitação
    - É fixo
- `LimitOffsetPagination`
    
    - No estilo LimitOffsetPagination, o cliente inclui um parâmetro de consulta “limite” e “deslocamento”
    - Dinâmico
- `CursorPagination`
    
    - O **CursorPagination** fornece um indicador de cursor para percorrer o conjunto de resultados. Ele fornece apenas controles de avanço ou reverso e não permite que o cliente navegue para posições arbitrárias. O estilo **CursorPagination** assume que deve haver um campo de carimbo de data / hora criado na instância do modelo e ordena os resultados por '-created’

Nas configurações do projeto, adicione:
```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}

REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.LimitOffsetPagination',
    'PAGE_SIZE': 10
}

REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.CursorPagination',
    'PAGE_SIZE': 10
}
```

No `LimitOffsetPagination` ele inclui alguns parâmetros na URL, como:
- `limit`
	- No **limit** é o limite de registros por página
- `offset`
	- No **offset** é a partir de qual registro começa, se colocar 10, ele começa do registro 10 a paginar