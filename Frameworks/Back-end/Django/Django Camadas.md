## 1. Configuração do Admin (`admin.py`)

```python
from django.contrib import admin
from cars.models import Brand, Car

class BrandAdmin(admin.ModelAdmin):
    list_display = ('id', 'name', 'created_at',)  # Colunas exibidas na lista
    search_fields = ('name',)  # Campos habilitados para busca

class CarAdmin(admin.ModelAdmin):
    list_display = ('id', 'model', 'brand__name', 'color', 'factory_year', 'model_year', 'created_at',)
    search_fields = ('model',)  # Busca por modelo
    list_filter = ('brand',)  # Filtros laterais por marca

admin.site.register(Brand, BrandAdmin)  # Registra modelo + configurações customizadas
admin.site.register(Car, CarAdmin)
```

**Explicação Detalhada:**
- **`list_display`**: Define quais campos serão exibidos na listagem
  - `brand__name` está incorreto. Para relacionamentos, use:
    ```python
    def brand_name(self, obj):
        return obj.brand.name
    brand_name.short_description = 'Marca'
    list_display = (..., 'brand_name')
    ```
- **`search_fields`**: Habilita a barra de busca usando campos específicos
- **`list_filter`**: Cria filtros laterais para navegação rápida
- **`admin.site.register()`**: Vincula o modelo à interface admin com configurações customizadas

---

## 2. Configuração de URLs

### `cars/urls.py` (App-level)
```python
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from cars.views import BrandModelViewSet, CarModelViewSet

router = DefaultRouter()  # Cria roteador DRF
router.register('brands', BrandModelViewSet)  # Registra ViewSet com base URL /brands/
router.register('cars', CarModelViewSet)      # Registra ViewSet com base URL /cars/

urlpatterns = [
    path('', include(router.urls)),  # Inclui todas URLs geradas pelo router
]
```

**Rotas Geradas Automaticamente:**
```
/brands/    → GET(list), POST(create)
/brands/1/  → GET(retrieve), PUT(update), PATCH(partial_update), DELETE(destroy)
/cars/      → Mesmas operações para Car
```

### `core/urls.py` (Project-level)
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),          # URL padrão do admin Django
    path('api/v1/', include('cars.urls')),    # Namespace para versionamento da API
]
```

**Estrutura Final de URLs:**
```
/admin/         → Painel admin Django
/api/v1/brands/ → Endpoint para marcas
/api/v1/cars/   → Endpoint para carros
```

---

## 3. Views (Controllers)

### `cars/views.py`
```python
from rest_framework import viewsets
from cars.models import Brand, Car
from cars.serializers import BrandModelSerializer, CarModelSerializer

class BrandModelViewSet(viewsets.ModelViewSet):
    queryset = Brand.objects.all()  # Define o conjunto de dados
    serializer_class = BrandModelSerializer  # Serializador usado

class CarModelViewSet(viewsets.ModelViewSet):
    queryset = Car.objects.all()
    serializer_class = CarModelSerializer
```

**Funcionamento do `ModelViewSet`:**

| Método HTTP | Ação          | URL Example       | Descrição               |
|-------------|---------------|-------------------|-------------------------|
| GET         | list          | /api/v1/cars/     | Lista todos             |
| POST        | create        | /api/v1/cars/     | Cria novo               |
| GET         | retrieve      | /api/v1/cars/1/   | Detalhe de um registro  |
| PUT         | update        | /api/v1/cars/1/   | Atualização completa    |
| PATCH       | partial_update| /api/v1/cars/1/   | Atualização parcial     |
| DELETE      | destroy       | /api/v1/cars/1/   | Remove registro         |

---

## 4. Serializers (Camada de Transformação de Dados)

### `cars/serializers.py`
```python
from rest_framework import serializers
from cars.models import Brand, Car

class BrandModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = Brand  # Modelo associado
        fields = '__all__'  # Todos campos do modelo

class CarModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = Car
        fields = '__all__'  # Inclui todos campos, incluindo FK
```

**Funcionalidades dos Serializers:**
1. **Validação de Dados**: Checa se os dados recebidos são válidos
2. **Conversão**: Transforma objetos Python ↔ JSON
3. **Controle de Campos**: Define quais campos são lidos/escritos
4. **Relacionamentos**: Gerencia FK, nested objects ou hyperlinks

**Melhor Prática:** Evite `fields = '__all__'` por segurança. Liste explicitamente:
```python
fields = ('id', 'model', 'brand', 'factory_year')
```

---

## 5. Arquitetura em Camadas do Django/DRF

### Fluxo de Requisição:
1. **URLs** → Mapeia requisição para View correta
2. **View** → Processa requisição, coordena operações
3. **Serializer** → Valida dados, converte formatos
4. **Model** → Interage com banco via ORM
5. **Response** → Retorna dados serializados

![Fluxo Django](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Z9mGkNGrZ7Hsw1ZxHyITCQ.png)

### Camadas Principais:
1. **Model (ORM)**: 
   - Define estrutura do banco
   - Gerencia operações de CRUD
   - Ex: `Car.objects.filter(brand__name='Fiat')`

2. **View (Controller)**: 
   - Lógica de negócio
   - Processa requisições/respostas
   - Ex: `CarModelViewSet`

3. **Template (UI)**: 
   - Não usado em APIs REST
   - Substituído por serializers no DRF

4. **Serializer**: 
   - Camada de apresentação
   - Validação e transformação de dados
   - Controle de versão de API

---

## 6. Dicas

### No Admin:
```python
class CarAdmin(admin.ModelAdmin):
    list_display = ('id', 'model', 'brand_name', 'color', 'factory_year')
    
    def brand_name(self, obj):
        return obj.brand.name
    brand_name.short_description = 'Marca'
```

### Nos Serializers (para relacionamentos):
```python
class CarModelSerializer(serializers.ModelSerializer):
    brand = serializers.StringRelatedField()  # Mostra o __str__ da marca
    
    class Meta:
        model = Car
        fields = ('id', 'model', 'brand', 'factory_year')
```

### Nas Views (otimização):
```python
class CarModelViewSet(viewsets.ModelViewSet):
    queryset = Car.objects.select_related('brand')  # Evita N+1 queries
    serializer_class = CarModelSerializer
```

### Versionamento de API:
```python
# core/urls.py
urlpatterns = [
    path('api/v1/', include('cars.urls')),
    path('api/v2/', include('cars.v2.urls')),  # Nova versão
]
```