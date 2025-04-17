# Guia Prático: Serializers no Django REST Framework

## 1. O que são Serializers?
Serializers convertem objetos Python (como modelos do Django) em formatos como JSON (serialização) e vice-versa (desserialização). Eles também validam dados recebidos, similar a formulários do Django.

---

## 2. Passo a Passo: Criando um Serializer Básico

### Passo 1: Definir um Serializer Manualmente
```python
# serializers.py
from rest_framework import serializers

class ProdutoSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    nome = serializers.CharField(max_length=100)
    preco = serializers.DecimalField(max_digits=10, decimal_places=2)
    estoque = serializers.IntegerField(min_value=0)

    def create(self, validated_data):
        """Cria um novo produto no banco de dados"""
        return Produto.objects.create(**validated_data)

    def update(self, instance, validated_data):
        """Atualiza um produto existente"""
        instance.nome = validated_data.get('nome', instance.nome)
        instance.preco = validated_data.get('preco', instance.preco)
        instance.estoque = validated_data.get('estoque', instance.estoque)
        instance.save()
        return instance
```

### Passo 2: Usar o Serializer em uma View
```python
# views.py
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Produto
from .serializers import ProdutoSerializer

@api_view(['POST'])
def criar_produto(request):
    serializer = ProdutoSerializer(data=request.data)
    if serializer.is_valid():
        serializer.save()
        return Response(serializer.data, status=201)
    return Response(serializer.errors, status=400)
```

---

## 3. Validações: Garantindo Dados Corretos

### Validação de Campo Simples (Exemplo: Preço Positivo)
```python
class ProdutoSerializer(serializers.Serializer):
    # ...
    def validate_preco(self, value):
        if value <= 0:
            raise serializers.ValidationError("Preço deve ser maior que zero!")
        return value
```

### Validação entre Campos (Exemplo: Estoque e Preço)
```python
class ProdutoSerializer(serializers.Serializer):
    # ...
    def validate(self, data):
        if data['estoque'] > 0 and data['preco'] == 0:
            raise serializers.ValidationError("Produtos em estoque não podem ter preço zero!")
        return data
```

---

## 4. ModelSerializer: Simplificando a Vida

### Passo 1: Criar um ModelSerializer
```python
# serializers.py
from rest_framework import serializers
from .models import Produto

class ProdutoModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = Produto
        fields = ['id', 'nome', 'preco', 'estoque']
```

### Benefícios:
- Gera automaticamente campos baseados no modelo.
- Implementa `create()` e `update()` automaticamente.
- Reduz código repetitivo em 80%.

---

## 5. Campos Customizados e Transformações

### Exemplo 1: Adicionar Campo Calculado
```python
class ProdutoModelSerializer(serializers.ModelSerializer):
    preco_com_taxa = serializers.SerializerMethodField()

    class Meta:
        model = Produto
        fields = ['id', 'nome', 'preco', 'estoque', 'preco_com_taxa']

    def get_preco_com_taxa(self, obj):
        return obj.preco * 1.1  # Adiciona 10% de taxa
```

### Exemplo 2: Formatar Data
```python
class PedidoSerializer(serializers.ModelSerializer):
    data_pedido = serializers.DateTimeField(format='%d/%m/%Y %H:%M')

    class Meta:
        model = Pedido
        fields = '__all__'
```

---

## 6. Relacionamentos entre Modelos

### Caso 1: Relação Many-to-Many (Exemplo: Tags)
```python
class TagSerializer(serializers.ModelSerializer):
    class Meta:
        model = Tag
        fields = ['id', 'nome']

class ProdutoSerializer(serializers.ModelSerializer):
    tags = TagSerializer(many=True, read_only=True)

    class Meta:
        model = Produto
        fields = ['id', 'nome', 'preco', 'tags']
```

### Caso 2: Aninhamento Completo (Criação/Atualização)
```python
class ProdutoSerializer(serializers.ModelSerializer):
    tags = TagSerializer(many=True)

    class Meta:
        model = Produto
        fields = '__all__'

    def create(self, validated_data):
        tags_data = validated_data.pop('tags')
        produto = Produto.objects.create(**validated_data)
        for tag_data in tags_data:
            tag, _ = Tag.objects.get_or_create(**tag_data)
            produto.tags.add(tag)
        return produto
```

---

## 7. Validações Avançadas

### Validação com Banco de Dados (Exemplo: Nome Único)
```python
class ProdutoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Produto
        fields = '__all__'

    def validate_nome(self, value):
        if Produto.objects.filter(nome__iexact=value).exists():
            raise serializers.ValidationError("Já existe um produto com este nome!")
        return value
```

### Validação Assíncrona (Exemplo: Consulta Externa)
```python
def validate_cep(self, value):
    import requests
    response = requests.get(f'https://viacep.com.br/ws/{value}/json/')
    if response.status_code != 200:
        raise serializers.ValidationError("CEP inválido!")
    return value
```

---

## 8. Sobrescrevendo Comportamentos Padrão

### Customizando a Criação:
```python
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['email', 'password']

    def create(self, validated_data):
        user = User.objects.create_user(
            email=validated_data['email'],
            password=validated_data['password']
        )
        return user
```

### Modificando a Resposta:
```python
class ProdutoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Produto
        fields = '__all__'

    def to_representation(self, instance):
        data = super().to_representation(instance)
        data['categoria'] = instance.get_categoria_display()  # Pega o nome da escolha
        return data
```

---

## 9. Boas Práticas e Dicas

1. **Use `ModelSerializer` por padrão:** Só crie Serializers manuais para casos muito específicos.
2. **Validações em camadas:** 
   - Validações simples → use parâmetros de campo (`max_length`, `required`)
   - Validações complexas → use métodos `validate_<campo>` ou `validate()`
3. **Mantenha os serializers focados:** 
   - Crie serializers diferentes para criação/leitura se necessário.
4. **Teste todas as validações:** 
   ```python
   def test_serializer_valida_preco_negativo(self):
       serializer = ProdutoSerializer(data={'nome': 'Teste', 'preco': -10})
       self.assertFalse(serializer.is_valid())
       self.assertIn('preco', serializer.errors)
   ```

---

## 10. Fluxo de Trabalho Típico

1. Definir Modelo no Django
2. Criar ModelSerializer baseado no modelo
3. Adicionar validações customizadas se necessário
4. Usar o serializer em uma View ou ViewSet
5. Testar todas as operações via Postman ou testes unitários

```python
# Exemplo de ViewSet Completo
class ProdutoViewSet(viewsets.ModelViewSet):
    queryset = Produto.objects.all()
    serializer_class = ProdutoSerializer

    def get_serializer_class(self):
        if self.action == 'create':
            return ProdutoCreateSerializer  # Serializer diferente para criação
        return ProdutoSerializer
```

---

## Conclusão

Serializers são o coração de APIs no DRF, atuando como guardiões dos dados. Dominar:
- Validações granularas
- Relacionamentos complexos
- Customizações de resposta
- Boas práticas de estrutura

Garante APIs robustas e fáceis de manter. Comece simples com `ModelSerializer`, evolua para customizações conforme necessidade, e sempre teste exaustivamente cada validação.

---

Vamos desvendar os **Serializers** no Django REST Framework (DRF) de forma detalhada, entendendo cada componente e suas configurações. 

---

## 1. **Campos do Serializer: O Básico**
Cada campo em um serializer define como um atributo do modelo (ou dado) é convertido para JSON (serialização) e vice-versa (desserialização).  
Existem **dois tipos principais de serializers**: `Serializer` (manual) e `ModelSerializer` (automático).

### Campos Comuns e Seus Parâmetros:
```python
from rest_framework import serializers

class ProdutoSerializer(serializers.Serializer):
    # Exemplo de campos básicos:
    id = serializers.IntegerField(
        read_only=True,  # Só aparece na saída (não é aceito em POST/PUT)
        help_text="ID único do produto"  # Descrição na documentação da API
    )
    nome = serializers.CharField(
        max_length=100,
        required=True,  # Campo obrigatório na desserialização (POST/PUT)
        allow_blank=False,  # Proíbe strings vazias
        trim_whitespace=True  # Remove espaços extras no início/fim
    )
    preco = serializers.DecimalField(
        max_digits=10,
        decimal_places=2,
        min_value=0,  # Valor mínimo permitido
        error_messages={
            'min_value': 'O preço não pode ser negativo!'  # Mensagem customizada
        }
    )
    ativo = serializers.BooleanField(
        default=True  # Valor padrão se o campo não for enviado
    )
    data_criacao = serializers.DateTimeField(
        format="%d/%m/%Y %H:%M",  # Formato de saída
        read_only=True  # Não é modificável via API
    )
```

#### Parâmetros Universais dos Campos:
| Parâmetro         | Descrição                                                                 |
|-------------------|---------------------------------------------------------------------------|
| `required`        | Se o campo é obrigatório (padrão: `True`).                                |
| `read_only`       | Campo só aparece na saída (ex: IDs gerados automaticamente).              |
| `write_only`      | Campo só é aceito na entrada (ex: senhas).                                |
| `default`         | Valor padrão se o campo não for fornecido.                                |
| `allow_null`      | Permite `None` como valor (útil para campos opcionais).                    |
| `source`          | Mapeia para um atributo diferente do modelo (ex: `source='get_full_name'`). |
| `validators`      | Lista de validadores customizados (ex: `[validador1, validador2]`).       |

---

## 2. **Classe `Meta` no ModelSerializer**
Usada para configurar o `ModelSerializer` de forma declarativa. Define qual modelo e campos serão serializados.

### Exemplo Completo:
```python
from rest_framework import serializers
from .models import Produto

class ProdutoSerializer(serializers.ModelSerializer):
    # Campos customizados (não presentes no modelo) podem ser adicionados aqui
    desconto = serializers.SerializerMethodField()

    class Meta:
        model = Produto  # Modelo associado ao serializer
        fields = ['id', 'nome', 'preco', 'desconto', 'categoria']  # Campos incluídos
        # fields = '__all__'  # Inclui todos os campos do modelo (não recomendado por segurança)
        exclude = ['data_criacao']  # Exclui campos específicos (alternativa ao fields)
        read_only_fields = ['id', 'data_modificacao']  # Campos somente leitura
        extra_kwargs = {
            'preco': {'min_value': 0},  # Parâmetros extras para campos específicos
            'categoria': {'write_only': True}  # Exemplo: categoria só na entrada
        }
        depth = 1  # Serializa relacionamentos até 1 nível de profundidade (ex: FK)

    def get_desconto(self, obj):
        """Método para campos customizados (SerializerMethodField)"""
        return obj.preco * 0.1
```

### Parâmetros da Classe `Meta`:
| Parâmetro           | Descrição                                                                 |
|---------------------|---------------------------------------------------------------------------|
| `model`             | Modelo Django associado ao serializer.                                    |
| `fields`            | Lista de campos do modelo a serem serializados (ou `'__all__'`).          |
| `exclude`           | Lista de campos do modelo a serem **excluídos** (alternativa ao `fields`).|
| `read_only_fields`  | Campos que serão **somente leitura** (não aceitos em POST/PUT).           |
| `extra_kwargs`      | Dicionário para configurar parâmetros específicos dos campos.             |
| `depth`             | Profundidade de serialização de relacionamentos (ex: ForeignKey).         |

---

## 3. **Validações: Garantindo Dados Corretos**

### 3.1 Validação de Campo Individual:
```python
class ProdutoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Produto
        fields = ['nome', 'preco']

    def validate_preco(self, value):
        """Validação customizada para o campo 'preco'."""
        if value < 10:
            raise serializers.ValidationError("Preço mínimo é R$ 10,00.")
        return value
```

### 3.2 Validação entre Múltiplos Campos:
```python
def validate(self, data):
    """Validação que envolve múltiplos campos."""
    nome = data.get('nome')
    preco = data.get('preco')

    if 'promocao' in nome.lower() and preco >= 100:
        raise serializers.ValidationError(
            "Produtos em promoção não podem custar mais que R$ 100,00."
        )
    return data
```

### 3.3 Validadores Externos:
```python
from rest_framework.validators import UniqueValidator

class ProdutoSerializer(serializers.ModelSerializer):
    nome = serializers.CharField(
        validators=[
            UniqueValidator(
                queryset=Produto.objects.all(),
                message="Já existe um produto com este nome!"
            )
        ]
    )
    # ...
```

---

## 4. **Relacionamentos entre Modelos**
Como serializar campos que se relacionam com outros modelos (ex: ForeignKey, ManyToMany).

### Exemplo com ForeignKey:
```python
class CategoriaSerializer(serializers.ModelSerializer):
    class Meta:
        model = Categoria
        fields = ['id', 'nome']

class ProdutoSerializer(serializers.ModelSerializer):
    categoria = CategoriaSerializer()  # Serializa o objeto inteiro (aninhado)

    # Ou, para apenas o ID:
    # categoria = serializers.PrimaryKeyRelatedField(queryset=Categoria.objects.all())

    # Ou, para um atributo específico:
    # categoria = serializers.SlugRelatedField(slug_field='nome', queryset=Categoria.objects.all())

    class Meta:
        model = Produto
        fields = ['id', 'nome', 'categoria']
```

### Tipos de Campos para Relacionamentos:
| Campo                          | Descrição                                                                 |
|--------------------------------|---------------------------------------------------------------------------|
| `PrimaryKeyRelatedField`       | Mostra o ID do objeto relacionado.                                        |
| `SlugRelatedField`             | Mostra um atributo específico (ex: `slug_field='nome'`).                  |
| `HyperlinkedRelatedField`      | Mostra um link para o objeto (ex: `view_name='categoria-detail'`).        |
| Serializer aninhado            | Inclui todos os dados do objeto relacionado (ex: `CategoriaSerializer()`).|

---

## 5. **Métodos Especiais: create() e update()**
Sobrescreva esses métodos para controlar como objetos são criados ou atualizados.

### Exemplo de `create()` com Relacionamento ManyToMany:
```python
class ProdutoSerializer(serializers.ModelSerializer):
    tags = serializers.PrimaryKeyRelatedField(many=True, queryset=Tag.objects.all())

    class Meta:
        model = Produto
        fields = ['id', 'nome', 'tags']

    def create(self, validated_data):
        tags_data = validated_data.pop('tags')  # Remove as tags dos dados
        produto = Produto.objects.create(**validated_data)  # Cria o produto
        produto.tags.set(tags_data)  # Associa as tags ao produto
        return produto
```

### Exemplo de `update()`:
```python
def update(self, instance, validated_data):
    # Atualiza campos simples
    instance.nome = validated_data.get('nome', instance.nome)
    instance.preco = validated_data.get('preco', instance.preco)
    
    # Atualiza relacionamento ManyToMany
    if 'tags' in validated_data:
        instance.tags.set(validated_data['tags'])
    
    instance.save()
    return instance
```

---

## 6. **Campos Dinâmicos e Customizados**

### SerializerMethodField:
```python
class ProdutoSerializer(serializers.ModelSerializer):
    status_estoque = serializers.SerializerMethodField()

    class Meta:
        model = Produto
        fields = ['id', 'nome', 'estoque', 'status_estoque']

    def get_status_estoque(self, obj):
        """Retorna 'Disponível' ou 'Esgotado' baseado no estoque."""
        return "Disponível" if obj.estoque > 0 else "Esgotado"
```

### Customizando a Representação (to_representation):
```python
def to_representation(self, instance):
    """Modifica a saída do serializer."""
    data = super().to_representation(instance)
    data['preco'] = f"R$ {data['preco']}"  # Formata o preço como string
    return data
```

---

## 7. **Exemplo Completo: Serializer para um E-commerce**
```python
from rest_framework import serializers
from .models import Produto, Categoria, Tag

class TagSerializer(serializers.ModelSerializer):
    class Meta:
        model = Tag
        fields = ['id', 'nome']

class CategoriaSerializer(serializers.ModelSerializer):
    class Meta:
        model = Categoria
        fields = ['id', 'nome']

class ProdutoSerializer(serializers.ModelSerializer):
    categoria = CategoriaSerializer()
    tags = TagSerializer(many=True)
    preco_promocional = serializers.SerializerMethodField()

    class Meta:
        model = Produto
        fields = [
            'id', 
            'nome', 
            'preco', 
            'preco_promocional', 
            'categoria', 
            'tags', 
            'estoque'
        ]
        read_only_fields = ['preco_promocional']
        extra_kwargs = {
            'estoque': {'min_value': 0}
        }

    def get_preco_promocional(self, obj):
        return obj.preco * 0.9  # 10% de desconto

    def validate_preco(self, value):
        if value < 10:
            raise serializers.ValidationError("Preço mínimo: R$ 10,00.")
        return value

    def validate(self, data):
        if data['estoque'] == 0 and not data.get('disponivel', True):
            raise serializers.ValidationError("Produto esgotado deve estar marcado como indisponível.")
        return data
```

---

## 8. **Dicas Finais**

1. **Use `ModelSerializer` para CRUD simples:** Economiza tempo e reduz código repetitivo.
2. **Campos customizados:** Use `SerializerMethodField` para dados calculados ou lógica complexa.
3. **Valide sempre:** Combine validações de campo, objeto e validadores externos.
4. **Relacionamentos:** Escolha entre IDs, slugs ou serializers aninhados conforme a necessidade da API.
5. **Teste seus serializers:** Garanta que todas as validações e transformações funcionem como esperado.

Com esse conhecimento, você está pronto para dominar os serializers no DRF e construir APIs robustas e seguras! 🚀