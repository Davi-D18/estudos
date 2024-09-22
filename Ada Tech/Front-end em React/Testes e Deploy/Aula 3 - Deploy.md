![[Pasted image 20240909140811.png]]

- *Build*: Transformar todos os códigos HTML, CSS e JS em um único arquivo

![[Pasted image 20240909141328.png]]

Na [Vercel](https://vercel.com), é possível fazer deploy de aplicações React de Graça
Tem a CLI da Vercel para fazer esse deploy de aplicações React que não estão no GIthub, basta instalar utilizando 
```zsh
yarn global add vercel 
```

## Fazendo Deploy sem GitHub
No terminal do projeto na raiz, digite `vercel` e vá respondnedo as perguntas de configurações do projeto

Caso queira fazer uma modificação no projeto depois do deploy e jogar lá novamente, basta digitar `vercel`

Depois de fazer o primeiro deploy, o projeto irá de primeira para o ambiente de produção e testes, a partir da 2° vez que fizer o deploy novamente ele vai apenas para o ambiente de testes
para fazer ir para o de produção, use o `vercel --prod`