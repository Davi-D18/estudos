Instalando o Django e o Django-Rest-Framework
```bash
pip install django djangorestframework
```

---

## 2. ORM Django: Fundamentos

### 2.1 Tipos de Campos
| Campo                 | Descrição                                      | Exemplo de Uso                     |
|-----------------------|-----------------------------------------------|------------------------------------|
| **CharField**         | Strings curtas (ex: nomes)                    | `nome = CharField(max_length=100)` |
| **TextField**         | Textos longos                                 | `descricao = TextField()`          |
| **IntegerField**      | Inteiros padrão (-2¹³¹ a 2¹³¹-1)              | `idade = IntegerField()`           |
| **DateTimeField**     | Data e hora com suporte a timezone            | `criado_em = DateTimeField(auto_now_add=True)` |
| **ForeignKey**        | Relacionamento 1-N com outro modelo           | `autor = ForeignKey(User, on_delete=models.CASCADE)` |
| **EmailField**        | Valida formato de e-mail                      | `email = EmailField(max_length=254)` |

**Campos Especiais:**
- `UUIDField`: Identificador único universal
- `JSONField`: Armazena estruturas JSON nativas
- `DurationField`: Períodos temporais (ex: 2 dias, 5 horas)

---

### 2.2 Opções de Campos
| Opção           | Descrição                                      | Exemplo                          |
|-----------------|-----------------------------------------------|----------------------------------|
| **null**        | Permite NULL no banco (padrão: False)         | `null=True`                      |
| **blank**       | Permite valor vazio em formulários            | `blank=True`                     |
| **default**     | Valor padrão quando não informado             | `default=0`                      |
| **choices**     | Lista de valores permitidos                   | `choices=[('S', 'Small'), ('L', 'Large')]` |
| **unique**      | Garante unicidade do valor                    | `unique=True`                    |
| **db_index**    | Cria índice no banco para otimização          | `db_index=True`                  |

**Diferença Crucial:**
```python
# Banco de Dados vs Formulários
models.CharField(
    null=True,    # BD aceita NULL
    blank=True    # Formulário aceita campo vazio
)
```

---

## 3. Classe Meta: Configurações Avançadas
```python
class Meta:
    db_table = 'custom_table_name'  # Nome da tabela no BD
    ordering = ['-data_criacao']    # Ordenação padrão
    indexes = [                     # Índices customizados
        models.Index(fields=['nome'], name='idx_nome')
    ]
    constraints = [                 # Restrições de BD
        models.UniqueConstraint(
            fields=['email', 'pais'], 
            name='unique_email_por_pais'
        )
    ]
    verbose_name = 'Artigo'         # Nome amigável
```

**Opções Principais:**
- `abstract = True`: Cria modelo base para herança
- `get_latest_by = 'data_publicacao'`: Define campo para latest()
- `default_related_name = 'posts'`: Nome padrão para relações reversas

---

## 4. Modelos Exemplo

### 4.1 Modelo Brand (Marca)
```python
class Brand(models.Model):
    name = models.CharField(max_length=100, verbose_name="Nome")
    description = models.TextField(null=True, blank=True, verbose_name="Descrição")
    created_at = models.DateTimeField(auto_now_add=True, verbose_name="Criado em")
    updated_at = models.DateTimeField(auto_now=True, verbose_name="Atualizado em")

    class Meta:
        ordering = ['name']
        verbose_name = "Marca"
        verbose_name_plural = "Marcas"

    def __str__(self):
        return self.name
```

### 4.2 Modelo Car (Carro)
```python
class Car(models.Model):
    model = models.CharField(max_length=100, verbose_name='Modelo')
    brand = models.ForeignKey(
        Brand, 
        on_delete=models.PROTECT, 
        verbose_name='Marca',
        related_name='cars'
    )
    factory_year = models.PositiveIntegerField(verbose_name='Ano de fabricação')
    model_year = models.PositiveIntegerField(verbose_name='Ano do modelo')
    owner = models.ForeignKey(
        'auth.User',
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        verbose_name='Proprietário'
    )

    class Meta:
        indexes = [
            models.Index(fields=['model', 'brand'], name='idx_model_brand')
        ]
```

---

## 5. Métodos Especiais em Modelos

### 5.1 Métodos Básicos
```python
def __str__(self):
    return f"{self.model} ({self.brand})"  # Representação legível

def save(self, *args, **kwargs):
    # Pré-processamento antes do save
    if not self.model_year:
        self.model_year = self.factory_year
    super().save(*args, **kwargs)  # Chamada obrigatória

def get_absolute_url(self):
    from django.urls import reverse
    return reverse('car-detail', kwargs={'pk': self.pk})
```

### 5.2 Validação Customizada
```python
def clean(self):
    if self.factory_year > date.today().year:
        raise ValidationError({'factory_year': 'Ano futuro inválido'})
    if self.model_year < self.factory_year:
        raise ValidationError('Ano modelo não pode ser anterior ao de fabricação')
```

---

## 6. Relacionamentos e ForeignKey

### 6.1 Tipos de on_delete
| Opção         | Comportamento                               | Caso de Uso Típico               |
|---------------|--------------------------------------------|-----------------------------------|
| **CASCADE**   | Apaga registros dependentes                | Comentários de um post           |
| **PROTECT**   | Bloqueia exclusão se houver dependentes    | Marcas com carros associados     |
| **SET_NULL**  | Define campo como NULL                     | Autor opcional de conteúdo       |
| **SET_DEFAULT**| Usa valor padrão                          | Categoria genérica padrão        |

### 6.2 Boas Práticas
```python
# Evitar referência direta ao User
from django.conf import settings

owner = models.ForeignKey(
    settings.AUTH_USER_MODEL,
    on_delete=models.CASCADE
)

# Nomeando relações reversas
class Car(models.Model):
    brand = models.ForeignKey(
        Brand,
        related_name='veiculos',
        related_query_name='veiculo'
    )
# Uso: brand.veiculos.all()
```

---

## 7. Consultas com ORM (QuerySet API)

### 7.1 Métodos Básicos
```python
# Criação
Car.objects.create(model='Fusca', brand=vw)

# Consulta
Car.objects.filter(brand__name='Volkswagen')
           .exclude(factory_year__lt=2000)
           .order_by('-model_year')

# Agregação
from django.db.models import Count
Brand.objects.annotate(total_carros=Count('cars'))

# Seleção relacionada (OTIMIZAÇÃO)
Car.objects.select_related('brand').prefetch_related('owner')
```

### 7.2 Métodos Avançados
```python
# Bulk Update
Car.objects.filter(factory_year=2020).update(model_year=2021)

# Valores específicos
Car.objects.values_list('model', flat=True).distinct()

# Raw SQL (uso cauteloso)
Car.objects.raw('SELECT * FROM app_car WHERE model LIKE "%a%"')
```

---

## 8. Integração com DRF (Exemplo Básico)

### 8.1 Serializer
```python
from rest_framework import serializers

class CarSerializer(serializers.ModelSerializer):
    brand_name = serializers.CharField(source='brand.name', read_only=True)
    
    class Meta:
        model = Car
        fields = ['id', 'model', 'brand', 'brand_name', 'factory_year']
        extra_kwargs = {
            'brand': {'write_only': True}
        }
```

### 8.2 ViewSet
```python
from rest_framework.viewsets import ModelViewSet

class CarViewSet(ModelViewSet):
    queryset = Car.objects.select_related('brand')
    serializer_class = CarSerializer
    filterset_fields = ['brand', 'model_year']
    search_fields = ['model', 'brand__name']
```

---

## 9. Melhores Práticas e Dicas

1. **Nomenclatura de Relações:**  
   Use `related_name` explícito para evitar conflitos:
   ```python
   user = models.ForeignKey(
       User,
       related_name='cars_owned'
   )
   ```

2. **Índices Compostos:**  
   Otimize consultas frequentes:
   ```python
   class Meta:
       indexes = [
           models.Index(fields=['model', 'factory_year'])
       ]
   ```

3. **Validação em Dois Níveis:**  
   Combine validação de modelo e serializer:
   ```python
   # Serializer
   def validate_factory_year(self, value):
       if value < 1900:
           raise serializers.ValidationError("Ano inválido")
       return value
   ```

4. **Versionamento de Esquema:**  
   Planeje evolução dos modelos com migrações reversíveis.

5. **Monitoramento de Desempenho:**  
   Use `django-debug-toolbar` para analisar consultas SQL.