Link para o site oficial: [typescript](https://typescriptlang.org)
![[Pasted image 20240706100210.png]]
# Instalando TS
Vá no terminal e use o comando `npm install typescript` também é possível usar alguns parâmetros, exemplo: 
- `-D`: Essa biblioteca será usada apenas no desenvolvimento
- `-g`: O pacote será instalado globalmente na máquina

# Rodando um projeto TS(convertendo em JS)
Na linha de comando, use o `npx tsc nomeDoArquivoPara_Conversao` 
Para evitar rodar esse script para executar e compilar toda vez, depois do nome do arquivo, adicione o parâmetro `--watch` ele irá observar as mudanças e compilar toda vez que tiver uma nova mudança
- `npx tsc --init` esse comando cria um arquivo de configuração TS
- Depois de inicializar o projeto em TS e instalar o TS, não é necessário passar o nome do arquivo para compilar, basta usar apenas o `npx tsc` 

## Configurando o `tsconfig.json` 
- `target`: é a versão do javascript que vai ser compilada
- `strict: true`: faz verificações de tipagens no código, por padrão vem como true
- `noEmitOnError: true`: se encontrar um erro no código ts, ele não vai compilar, por padrão vem comentada essa regra
- `outDir`: diretório onde será armazenado o arquivo .js depois de compilar do .ts