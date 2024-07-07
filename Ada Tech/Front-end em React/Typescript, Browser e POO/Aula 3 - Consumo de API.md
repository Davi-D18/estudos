# Fetch API
É uma API do Browser, ela faz requisições em APIs

Utilizando o método `.then` e `.catch`:
```jsx
fetch('viacep.com.br/ws/01001000/json/')
	.then((response) => {
		response.json().then((dados) => console.log(dados));
	}).catch((erro) => {
		console.log(erro)
	});
```
Após fazer uma requisição, os dados ficará em um formato parecido com html, use o método `.json`para converte-los em json, porém esse método é uma promise, sendo assim irá levar um tempo para converter, por isso o outro `.then` 

Utilizando o `async` e `await`:
```jsx
// async vem de assíncrona e await vem de aguarde, algo assim
async function obterDadosDoCep() {
	try {
		const dados = await fetch('viacep.com.br/ws/01001000/json/')
		const dadosConvertidosEmJson = await dados.json();
		console.log(dadosConvertidosEmJson);
	} catch(erro) {
		console.log('Deu erro', erro);
	} finally {
		console.log('Terminou a requisição');
	}
}

obterDadosDoCep();

```

> [Importante]
> Quando for usar APIs lembre-se de sempre olhar a documentação daquela API

## Fazendo requisições

```js
// obtendo informação de vários usuários
async function getUsers() {
	const reposta = fetch('https://dummyapi.io/data/v1/user', {
		headers: {
			"app-id": "id aqui"
		},
	});

	const users = await resposta.json();
	console.log(users.data);
}
// depois do link no fetch, pode passar outro parâmetro contendo o body, heraders e etc porém é entre chaves { } em seguida passe sua chave id dentro do headers

// obtendo informações de um usuário em especifico
async function getUser() {
	const reposta = fetch('https://dummyapi.io/data/v1/user/id_do_usuario', {
		headers: {
			"app-id": "id aqui"
		},
	});

	const users = await resposta.json();
	console.log(users);
}

// criando um usuário
async function createUser() {
	const userData = {
		firstname: "Davi",
		lastname: "Araújo",
		email: "luizdavi@gmail.com",
	};

	await fetch('https://dummyapi.io/data/v1/user/create', {
		// aqui informará o tipo de requisição, no caso POST
		method: "POST",
		headers: {
			"app-id": "api-key",
			"Content-Type": "application/json",
			// o content-type é obrigatório caso queira usar o POST
		},
		body: json.strigify(userData),
	});
}
```


> [Importante] Métodos de Requisição
> Você sempre deve se atentar a informar o método que irá usar, caso use o Get, ele é padrão então não precisa informar, mas outros como POST é necessário 



