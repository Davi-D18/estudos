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