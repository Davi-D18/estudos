![[Pasted image 20240702075138.png]]

# Callbacks

## fs()
fs() é uma biblioteca para ler arquivos
![[Pasted image 20240702080007.png]]

```jsx
const fs = require('fs')
// importando a biblioteca

fs.readline("aula-13/arquivo.json", (erro, conteudo) => {
	if (erro) {
		console.log('Ocorreu um erro ao ler o arquivo', erro);
	} else {
		console.log(String(conteudo));
	}
});
// detalhe, ao ler o conteúdo ele será carregado em buffer, por isso precisa
// converter em string ou outro tipo de dado
```

## setTimeout()
espera um tempo antes de executar algo
```jsx
setTimeout(() => {
	console.log('Isso aqui será executado')
}, 2000);
// uma estrutura básica dessa função assíncrona
```


# Promises
![[Pasted image 20240702082112.png]]
## then()
then() será executado quando ocorrer tudo certo com a promise
```jsx
const promessa = new Promise((resolve, reject) => {
	fs.readline("aula-13/arquivo.json", (erro, conteudo) => {
	if (erro) {
		reject('Ocorreu um erro ao ler o arquivo', erro);
	} else {
		resolve(String(conteudo));
	}
});
});

promessa.then((retornoDaPromise) => {
	console.log('A promise deu certo:', retornoDaPromise);
});

```
Dificilmente você irá criar uma **promise**, porém aí mostra uma forma de lidar usando o método 
**then** e usando uma variável de parâmetro caso ocorra tudo bem

## catch()
Caso dê erro, o método usado será o **catch** depois do fechamento do ultimo parenteses, basicamente a estrutura do catch é a mesma do then
```jsx
// considerando o bloco de código anterior
.catch((erro) => {
	console.log('Deu ruim:', erro);
});

```

## finally()
Será executado independente do resultado ocorrer bem ou dá erro 
```jsx
.catch(() => {
	console.log('Será executado dando certo ou não');
}); 

```


# async / await
`await`: aguarde 
`async`: assíncrona (transforma uma função em assíncrona)
detalhe: você deve criar uma função e usar o `async` para em seguida colocar dentro dessa função outra função e utilizar o `await` para funcionar
```jsx
function lerArquivos () {
	return promessa = new Promise((resolve, reject) => {
	fs.readline("aula-13/arquivo.json", (erro, conteudo) => {
	if (erro) {
		reject('Ocorreu um erro ao ler o arquivo', erro);
	} else {
		resolve(String(conteudo));
	}
});
});
}

async function leituraDeDados () {
	console.log('Isso é executado')
	try {
		const retornoDaPromessa = await lerArquivos();
		console.log(retornoDaPromessa);
		console.log('Isso aqui será executado depois da função anterior')
	} catch (erro) {
		console.log('Caso dê erro, será executado isso')
	}
}
```

`try` executará o código se ocorrer tudo bem, caso dê erro, aí ele entra no `catch`  para fazer algo quando der erro