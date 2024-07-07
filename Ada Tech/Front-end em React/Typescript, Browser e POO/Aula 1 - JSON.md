![[Pasted image 20240703091824.png]]
Quando for instalar bibliotecas e caso uma biblioteca seja útil apenas na hora do desenvolvimento como o caso do eslint, seria interessante retirar essa biblioteca ao publicar o software, usando o `--save-dev` 
```bash
npm install eslint --save-dev
// ou -D 
```

![[Pasted image 20240703100004.png]]


## Lendo um arquivo Json com Javascript
usando uma biblioteca para ler arquivos, procure o arquivo JSON que você quer ler os dados e converta-os 
```jsx
const fs = require('fs')

fs.readline('eslintrc.json', (erro, dados) => {
	if (erro) {
		console.log('Erro:', erro);
	} else {
		const dados_obtidos = JSON.parse(dados);
	}
});

// nesse caso irá ler as informações do JSON e converter em um object do javascript 
```
`JSON.parse()` converte arquivos JSON para objetos
`JSON.stringify()` converte objetos do js para formatos JSON


