Crie um arquivo permissions.py:
```python
from django.core.exceptions import PermissionDenied


class UserIsOwnerMixin:

	# Sobrescrevendo o método dispatch usando polimorfismo(POO)
	def dispatch(self, request, *args, **kwargs):
		obj = self.get_object()
		if obj.user != self.request.user:
			raise PermissionDenied
			# caso o objeto criado por usuário for acessado por outro usuário                diferente, ele receberá um "permissão negada"
		return super().dispatch()
```

Nas views/controllers:
```python
class ProductListView(LoginRequiredMixin, ListView):
	model = Product
	template_name = 'product_list.html'
	context_object_name = 'products'

	def get_queryset(self):
		return Product.objects.filter(
			user=self.request.user
		)

# O UserIsOwnerMixin é herdado nas outras classes com os métodos POST, DELETE, PUT / PATCH 
# Quando um usuário acessa essas rotas sem a devida permissão, ele não consegue acessar

class ProductCreateView(LoginRequiredMixin, UserIsOwnerMixin, CreateView):
	model = Product
	template_name = 'product_create.html'
	form_class = forms.ProductForm
	sucess_url = reverse_lazy('product_list')

	def form_valid(self, form):
		form.instance.user = self.request.user
		return super().form_valid(form)


class ProductDetailView(LoginRequiredMixin, UserIsOwnerMixin, DetailView):
	model = Product
	template_name = 'product_detail.html'


class ProductUpdateView(LoginRequiredMixin, UserIsOwnerMixin, UpdateView):
	model = Product
	template_name = 'product_update.html'
	form_class = forms.ProductForm
	success_url = reverse_lazy('product_list.html')


class ProductDeleteView(LoginRequiredMixin, UserIsOwnerMixin, DeleteView):
	model = Product
	template_name = 'product_delete.html'
	success_url = reverse_lazy('product_list')
```

Ao criar um arquivo de permissões personalizadas como por exemplo, apenas os usuários que criaram / cadastraram um produto podem visualizar esse produto, outros usuários recebem um "acesso negado", em seguida importar e usar nas classes das views herdando, naquela rota ele passa a aplicar as permissões personalizadas. Nas rotas não precisa configurar nada

No exemplo acima está usando apenas o Django

## Métodos
`dispatch()`:
É o "controlador central" das *class-based views*. Ele define para qual método da classe (como `get`, `post`, etc.) a requisição HTTP será enviada, baseando-se no tipo de requisição (GET, POST, etc.).

**Como funciona passo a passo:**  
1. Quando uma requisição chega (ex: um acesso à página), o Django cria uma instância da view e chama o método `dispatch`.  
2. O `dispatch` verifica qual é o método HTTP usado na requisição (GET, POST, PUT, etc.).  
3. Ele **redireciona** a requisição para o método correspondente na classe:  
   - Se for GET → chama o método `get()` da view.  
   - Se for POST → chama o método `post()`.  
4. Se o método não existir (ex: alguém fez uma requisição PUT, mas a view não tem `put()`), retorna um erro (HTTP 405 - Método não permitido).

**Exemplo Prático:**  
Se você tem uma view com `get()` e `post()`, o `dispatch` garante que:  
- Acessar a página (GET) executa `get()`.  
- Enviar um formulário (POST) executa `post()`.

**Pontos importantes:**  
- O `dispatch` é chamado automaticamente pelo Django (você raramente precisa mexer nele).  
- Requisições **HEAD** (usadas para verificar recursos) são tratadas como GET por padrão, mas você pode customizar isso.  
- Se quiser adicionar lógica que aconteça **antes de qualquer método** (ex: validar um usuário), você pode sobrescrever o `dispatch` na sua view.

**Resumo:**  
O `dispatch` é como um "guia" que direciona cada tipo de requisição HTTP para o método correto dentro da sua view, automatizando o fluxo básico.

Material: [Pylive](https://pickle-reading-bd9.notion.site/pylive-009-cec874edd164498b9139c10ce51aae8c)