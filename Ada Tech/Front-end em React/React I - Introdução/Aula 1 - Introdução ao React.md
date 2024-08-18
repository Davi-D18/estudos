![[Pasted image 20240815100139.png]]Um exemplo: ![[Pasted image 20240815100502.png]]
## Compilers e Builders
- **Babel**: Um compilador que vai converter um código "recente" para uma versão antiga que o browser entenda
- **[WebPack](https://webpack.js.org)**: Pega vários códigos JavaScript e outros tipos de arquivos e junta em um único arquivo

### Importando e exportando arquivos
#### Exportando
```ts
export function saudacao () {
	console.log("Olá");
}

export const PI = 3.1415
```

#### Importando

> [Importações]
> **EsModules** se dá a esse tipo de importação, a forma antiga se chama **CommonJs**

```ts
import {saudacao, PI} from './caminho/do/arquivo.ts'
// A partir daqui pode usar normalmente funções ou váriaveis do arquivo anterior
```
Pode dar um erro no navegador se tentar compilar do TS para JS por causa que ele compila em uma versão antiga do JS que a forma de importação é a CommonJs e os navegadores não entendem essa forma, para resolver:
- Vá no arquivo de configuração do TS
- Procure a chave **Modules** e altere para **ES6**

### StrictMode
Uma ferramenta para checar possíveis más praticas no React e emitir *Warnings* no ambiente de desenvolvimento