# guia-node-js

# Introdução

Olá, muito obrigado por ter acessado esse guia, ele foi pensado e desenvolvido com muito carinho com o objetivo de ajudar você que está começando na programação.

Não esquece de me seguir no Instagram [**@umporcentoprog](https://www.instagram.com/umporcentoprog/)** que lá eu trago conteúdo educacional de programação todos os dias, e é por lá que eu solto esses guias gratuitos, como esse que você está lendo!

**IMPORTANTE:**

Para melhor proveito desse guia, recomendo fortemente que você tenha uma base sólida com a linguagem JavaScript, caso não tenha, recomendo ler o meu guia gratuito de JavaScript:

[**Guia JavaScript**](https://www.notion.so/guia-javascript-90241f2f64f140d1a77fbaaca4da32ce?pvs=21)

---

# 1- Introdução ao Node

## **1.1 - O que é Node.js?**

Node.js é um runtime de JavaScript construído no motor V8 do Google Chrome. Diferente dos navegadores, que executam JavaScript no lado do cliente, o Node.js permite que o JavaScript seja executado no lado do servidor. Isso significa que você pode usar a mesma linguagem tanto para a lógica de frontend quanto para a lógica de backend da sua aplicação.

Node.js é conhecido por seu modelo de I/O não bloqueante e orientado a eventos, que o torna uma escolha popular para construir aplicações de rede escaláveis, como servidores web, APIs e aplicações em tempo real.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f7feecbd-7058-4805-b782-5c71283c99cc/d4618b97-f2a0-4c87-a97a-d40aea5d311d/Untitled.png)

## **1.2 - História e evolução do Node.js**

Node.js foi criado por Ryan Dahl em 2009. A motivação por trás do Node.js foi a necessidade de construir aplicações de alta performance que pudessem lidar com um grande número de conexões simultâneas. Antes do Node.js, as soluções de servidores tradicionais, como Apache e IIS, utilizavam um modelo de thread, que não era tão eficiente em termos de performance e escalabilidade.

## **1.3 - Vantagens e desvantagens do uso de Node.js**

**Vantagens**

1. **Performance Alta**: O Node.js é construído sobre o motor V8 do Google, que é extremamente rápido na execução de JavaScript.
2. **Escalabilidade**: Devido ao seu modelo de I/O não bloqueante, o Node.js pode lidar com um grande número de conexões simultâneas de forma eficiente.
3. **Unificação do Stack**: Com o Node.js, é possível usar JavaScript tanto no frontend quanto no backend, facilitando o desenvolvimento full-stack.
4. **Grande Comunidade**: O Node.js possui uma comunidade ativa e um vasto ecossistema de pacotes disponíveis através do npm.
5. **Real-time**: Perfeito para aplicações em tempo real, como chats e jogos online.

**Desvantagens**

1. **Modelo Assíncrono**: O modelo de programação assíncrona pode ser desafiador para desenvolvedores que não estão familiarizados com ele.
2. **Single-threaded**: Embora o Node.js possa lidar com muitas conexões simultâneas, ele ainda é single-threaded, o que pode ser uma limitação para algumas tarefas computacionais pesadas.
3. **Callback Hell**: Sem um gerenciamento adequado, o uso extensivo de callbacks pode tornar o código difícil de manter e ler, embora o uso de Promises e async/await tenha mitigado esse problema.

---

# **2- Instalação e Configuração do Ambiente🛠️**

Preparar seu ambiente de desenvolvimento é o primeiro passo prático para começar a criar aplicações backend incríveis. Vamos lá! 🚀

## **Escolhendo uma Versão do Node.js**

O Node.js possui várias versões disponíveis, cada uma com suas próprias características e funcionalidades. Duas versões principais são amplamente utilizadas:

- **LTS (Long-Term Support)**: Esta versão é recomendada para a maioria dos projetos de produção, pois recebe suporte a longo prazo e atualizações de segurança regulares.
- **Current**: Esta versão contém as funcionalidades mais recentes, mas não é recomendada para produção, pois pode não ser tão estável quanto a versão LTS.

## **Instalação do Node.js**

Para instalar o Node.js, siga os passos relevantes para o seu sistema operacional:

- **Windows**: Baixe o instalador do Node.js no site oficial e siga o assistente de instalação.
- **macOS**: Use o Homebrew ou baixe o instalador do Node.js no site oficial.
- **Linux**: Use o gerenciador de pacotes apropriado para sua distribuição, como o **`apt-get`** no Ubuntu.

## **Verificação da Instalação**

Após a instalação, você pode verificar se o Node.js e o npm (Node Package Manager) foram instalados corretamente. Abra o terminal e digite os seguintes comandos:

```
node -v
npm -v
```

Esses comandos retornarão as versões instaladas do Node.js e npm, respectivamente.

## **Gerenciadores de Pacotes (npm e Yarn)**

Os gerenciadores de pacotes são essenciais para instalar e gerenciar bibliotecas e módulos em seus projetos Node.js. Os dois gerenciadores mais comuns são:

- **npm**: É o gerenciador de pacotes padrão que vem com o Node.js. Ele é amplamente utilizado e oferece um vasto ecossistema de pacotes.
- y**arn**: Uma alternativa ao npm, Yarn é conhecido por sua velocidade e eficiência. Você pode escolher entre npm e Yarn com base em suas preferências.

## **Inicializando um Projeto Node.js com npm ou Yarn**

Agora que você tem o Node.js e um gerenciador de pacotes instalados, pode criar um novo projeto Node.js. Para isso, você pode usar os seguintes comandos:

- Com npm:

```
npm init
```

- Com Yarn:

```
yarn init
```

Isso iniciará um assistente para criar um arquivo **`package.json`**, que é o arquivo de configuração do seu projeto.

## **Estrutura de Pastas Típica de um Projeto Node.js**

Um projeto Node.js típico consiste em uma estrutura de pastas que organiza seus arquivos e recursos de forma eficiente. Aqui está uma estrutura comum:

```scss
meu-projeto/
  |- node_modules/   (pasta para módulos e pacotes de terceiros)
  |- src/            (pasta para seus arquivos JavaScript)
  |- package.json    (arquivo de configuração do projeto)
  |- README.md       (documentação do projeto)
```

Agora que você configurou o ambiente, está pronto para começar a escrever código em Node.js e construir aplicativos poderosos. Este é o primeiro passo para se tornar um desenvolvedor Node.js competente. Certifique-se de acompanhar os próximos tópicos para expandir seu conhecimento e habilidades.

## **Primeiros Passos com Node.js**

Node.js permite executar JavaScript fora do navegador. Isso abre um novo mundo de possibilidades, como criar servidores web, interagir com sistemas de arquivos, e muito mais.

### **Criando Seu Primeiro Script**

1. **Crie um Arquivo JavaScript**: No seu projeto Node.js, crie um arquivo chamado **`index.js`**.
2. **Escreva Algum Código JavaScript**: Por exemplo, um simples **`console.log`**.

```jsx
// index.js
console.log("Olá, mundo Node.js!");
```

Este código, embora simples, é poderoso. Ele mostra o básico da execução de um script Node.js.

### **Executando o Programa**

Para rodar seu programa, você precisa de um terminal ou linha de comando, por isso, recomendo usar o Visual Studio Code, pois ele tem um terminal incluso, na barra superior é só clicar em terminal.

1. **Abra o Terminal.**
2. **Execute o Script**: Digite **`node index.js`** e pressione Enter.
3. **Veja o Resultado**: Se tudo estiver correto, você verá "Olá, mundo Node.js!" impresso no terminal.

### **O Que Acontece Aqui?**

- **`node`**: É o comando para executar o Node.js.
- **`index.js`**: Indica ao Node.js qual arquivo executar.
- **Resultado**: O Node.js lê o arquivo **`index.js`**, executa o código JavaScript nele e imprime o resultado no terminal.

## **Entendendo o Processo**

- **Node.js como Runtime**: Ao contrário do JavaScript no navegador, onde seu código é executado dentro do contexto de uma página web, Node.js executa seu código como um processo independente em seu computador.
- **Uso do Console**: O **`console.log`** é uma maneira de imprimir informações no terminal, útil para depuração e exibição de dados.

### **Exemplo Prático Adicional**

Vamos ir um pouco além e adicionar uma função.

```jsx
// index.js
function saudacao(nome) {
  return `Olá, ${nome}! Bem-vindo ao Node.js!`;
}

console.log(saudacao("João"));
```

Aqui, definimos uma função **`saudacao`** que recebe um nome e retorna uma mensagem de boas-vindas. Em seguida, chamamos essa função com um nome e imprimimos o resultado.

## Materiais complementares:

- [Node.JS: Como BAIXAR E INSTALAR no Windows](https://www.youtube.com/watch?v=-cLzUD0TQY0&pp=ygUTaW5zdGFsYcOnw6NvIG5vZGVqcw%3D%3D)
- [Como instalar Node.js no Linux de maneira simples e fácil](https://www.youtube.com/watch?v=LU1TYsyPim0&pp=ygUMbm9kZWpzIGxpbnV4)
- [How to install Nodejs on Mac [Any version & Easy method]](https://www.youtube.com/watch?v=SwUKKCS3r3c&pp=ygUMbm9kZWpzIG1hY29z)

---

# 3. Fundamentos do Node.js

## 3.1 O que é o V8 Engine?

O V8 é um motor de execução de JavaScript open-source desenvolvido pelo Google. Ele foi projetado para o navegador Google Chrome, mas também é usado no Node.js para executar JavaScript no lado do servidor. O V8 compila o JavaScript diretamente para código de máquina nativo antes de executá-lo, o que resulta em uma performance extremamente rápida.

### Características do V8

- **JIT Compilation (Just-In-Time)**: O V8 utiliza compilação Just-In-Time para converter o JavaScript em código nativo durante a execução, otimizando a performance.
- **Garbage Collection**: O V8 possui um sistema de coleta de lixo eficiente que gerencia a alocação e desalocação de memória automaticamente.
- **Suporte a ECMAScript**: O V8 é frequentemente atualizado para suportar as últimas versões do padrão ECMAScript, garantindo que os desenvolvedores possam usar os recursos mais modernos do JavaScript.

## 3.2 Event Loop e Assíncronismo

O Event Loop é o coração do Node.js e a chave para seu comportamento assíncrono. Diferente de linguagens de programação tradicionais que utilizam threads para lidar com múltiplas tarefas simultâneas, o Node.js usa um único thread, mas com um modelo de I/O não bloqueante e orientado a eventos.

### Como Funciona o Event Loop

1. **Call Stack**: Onde as funções são executadas. Quando uma função é chamada, ela é empilhada na call stack.
2. **Node APIs**: Quando uma operação assíncrona, como leitura de arquivo ou requisição de rede, é iniciada, ela é delegada para as Node APIs, permitindo que a call stack continue a processar outras tarefas.
3. **Callback Queue**: Uma vez que a operação assíncrona é concluída, a callback associada é empilhada na callback queue.
4. **Event Loop**: O Event Loop monitora a call stack e a callback queue. Quando a call stack está vazia, o Event Loop move as callbacks da callback queue para a call stack para serem executadas.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f7feecbd-7058-4805-b782-5c71283c99cc/c249126e-7ae9-47e4-bd6e-19572f3fa0b9/Untitled.png)

### Exemplos de Assíncronismo no Node.js

- **I/O não bloqueante**: Operações de leitura e escrita de arquivos, requisições de rede e manipulação de banco de dados são realizadas de forma assíncrona.
- **Timers**: Funções como `setTimeout` e `setInterval` permitem a execução de código de forma assíncrona após um determinado período de tempo.

## 3.3 Callbacks, Promises e Async/Await

Node.js oferece várias maneiras de lidar com operações assíncronas. As três abordagens principais são callbacks, promises e async/await.

### Callbacks

Callbacks são funções passadas como argumento para outras funções e são chamadas quando a operação assíncrona é concluída.

```jsx
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});

```

### Problema do Callback Hell

O uso extensivo de callbacks pode levar ao "callback hell", onde o código fica aninhado em vários níveis, tornando-se difícil de ler e manter.

```jsx
doSomething(param1, (err, result) => {
  if (err) {
    // handle error
  } else {
    doSomethingElse(result, (err, result2) => {
      if (err) {
        // handle error
      } else {
        // continue...
      }
    });
  }
});

```

### Promises

Promises são uma forma mais moderna e legível de lidar com operações assíncronas. Elas representam um valor que pode estar disponível agora, no futuro ou nunca.

```jsx
const fs = require('fs').promises;

fs.readFile('example.txt', 'utf8')
  .then(data => {
    console.log(data);
  })
  .catch(err => {
    console.error(err);
  });

```

### Async/Await

Async/await é uma sintaxe que torna o uso de promises mais simples e legível, permitindo escrever código assíncrono de forma semelhante ao código síncrono.

```jsx
const fs = require('fs').promises;

async function readFile() {
  try {
    const data = await fs.readFile('example.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}

readFile();

```

### Comparação

- **Callbacks**: Simples e direto, mas pode levar ao callback hell.
- **Promises**: Mais legíveis e gerenciáveis, especialmente com encadeamento.
- **Async/Await**: Sintaxe mais limpa e fácil de entender, lidando de forma natural com código assíncrono.

---

# 4. Módulos e Pacotes

## 4.1 Sistema de Módulos do Node.js

O Node.js utiliza um sistema de módulos para organizar e estruturar o código. Módulos são arquivos JavaScript que exportam funcionalidades para serem utilizadas em outros arquivos. Existem dois tipos principais de módulos no Node.js:

- **Módulos Internos**: Incluídos no núcleo do Node.js, como `fs` (sistema de arquivos), `http` (servidor HTTP), e `path` (manipulação de caminhos de arquivos).
- **Módulos Externos**: Instalados via npm (Node Package Manager) e gerenciados como dependências do projeto.

### Importação e Exportação de Módulos

Para utilizar um módulo, você deve importá-lo usando a função `require()`. Para tornar funções ou variáveis disponíveis para outros arquivos, você deve exportá-las.

**Exemplo de Módulo Interno:**

```jsx
const fs = require('fs');
```

**Criando e Utilizando um Módulo Externo:**

1. Crie um arquivo chamado `math.js` com o seguinte conteúdo:
    
    ```jsx
    function add(a, b) {
      return a + b;
    }
    
    function subtract(a, b) {
      return a - b;
    }
    
    module.exports = { add, subtract };
    ```
    
2. Importe e utilize o módulo em outro arquivo:
    
    ```jsx
    const math = require('./math');
    
    console.log(math.add(2, 3)); // 5
    console.log(math.subtract(5, 3)); // 2
    ```
    

## 4.2 Gerenciamento de Pacotes com npm

O npm (Node Package Manager) é o gerenciador de pacotes padrão do Node.js. Ele permite instalar, atualizar e remover pacotes de software.

### Instalando Pacotes com npm

- **Instalar um Pacote**: Para instalar um pacote e adicioná-lo ao `package.json`, use o comando `npm install <package_name>`.
    
    ```
    npm install express
    ```
    
- **Instalar Dependências de Desenvolvimento**: Use a flag `-save-dev` para instalar pacotes que só são necessários em desenvolvimento.
    
    ```
    npm install jest --save-dev
    ```
    
- **Atualizar Pacotes**: Use `npm update` para atualizar os pacotes para suas versões mais recentes compatíveis.
    
    ```
    npm update
    ```
    
- **Remover Pacotes**: Use `npm uninstall <package_name>` para remover um pacote e suas dependências do `package.json`.
    
    ```
    npm uninstall express
    ```
    

## 4.3 Trabalhando com Módulos Internos

Os módulos internos do Node.js são bibliotecas padrão incluídas na instalação do Node.js. Eles oferecem funcionalidades essenciais para várias tarefas. Aqui vai uma pequena introdução ao fs, mas não se preocupe que no próximo tópico iremos se aprofundar nele:

### Módulo `fs`

O módulo `fs` (file system) permite interagir com o sistema de arquivos do seu computador.

**Leitura de Arquivos:**

```jsx
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```

**Escrita de Arquivos:**

```jsx
const fs = require('fs');

const content = 'Some content!';

fs.writeFile('example.txt', content, err => {
  if (err) {
    console.error(err);
    return;
  }
  console.log('File has been written');
});

```

### Exercícios Práticos

1. **Criar um Módulo Personalizado**: Crie um módulo chamado `utils.js` que exporta funções para operações matemáticas básicas (adição, subtração, multiplicação e divisão). Importe e use este módulo em um arquivo separado.
2. **Gerenciamento de Pacotes com npm**: Instale um pacote de sua escolha usando npm e crie um pequeno projeto que utilize esse pacote. Por exemplo, use `axios` para fazer uma requisição HTTP e exibir a resposta.
3. **Explorar o Módulo `os`**: Use o módulo interno `os` para exibir informações sobre o sistema operacional, como a plataforma, arquitetura, e a quantidade de memória livre.

---

# 5. Trabalhando com o Sistema de Arquivos (fs)

O módulo `fs` (file system) do Node.js permite interagir com o sistema de arquivos do seu computador. Ele oferece uma ampla gama de funcionalidades para ler, escrever, atualizar e excluir arquivos, bem como para manipular diretórios.

## 5.1 Leitura de Arquivos

A leitura de arquivos pode ser feita de forma síncrona ou assíncrona. No Node.js, é recomendado usar operações assíncronas para evitar o bloqueio do Event Loop.

### Leitura Assíncrona

```jsx
const fs = require('fs');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});

```

### Leitura Síncrona

```jsx
const fs = require('fs');

try {
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error(err);
}

```

## 5.2 Escrita de Arquivos

Assim como na leitura, a escrita de arquivos pode ser realizada de forma síncrona ou assíncrona.

### Escrita Assíncrona

```jsx
const fs = require('fs');

const content = 'Some content!';

fs.writeFile('example.txt', content, err => {
  if (err) {
    console.error(err);
    return;
  }
  console.log('File has been written');
});

```

### Escrita Síncrona

```jsx
const fs = require('fs');

const content = 'Some content!';

try {
  fs.writeFileSync('example.txt', content);
  console.log('File has been written');
} catch (err) {
  console.error(err);
}

```

## 5.3 Manipulação de Diretórios

### Criação de Diretórios

Você pode criar novos diretórios usando `fs.mkdir`.

```jsx
const fs = require('fs');

fs.mkdir('new-directory', { recursive: true }, err => {
  if (err) {
    console.error(err);
    return;
  }
  console.log('Directory created');
});

```

### Leitura de Diretórios

Para ler o conteúdo de um diretório, use `fs.readdir`.

```jsx
const fs = require('fs');

fs.readdir('.', (err, files) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(files);
});

```

## 5.4 Streams e Buffers

### Leitura de Arquivos com Streams

Streams são uma forma eficiente de ler e escrever grandes quantidades de dados. Em vez de carregar o arquivo inteiro na memória, você pode processá-lo em partes.

```jsx
const fs = require('fs');

const readStream = fs.createReadStream('large-file.txt', 'utf8');

readStream.on('data', chunk => {
  console.log(chunk);
});

readStream.on('end', () => {
  console.log('Finished reading');
});

readStream.on('error', err => {
  console.error(err);
});

```

### Escrita de Arquivos com Streams

```jsx
const fs = require('fs');

const writeStream = fs.createWriteStream('large-file.txt');

writeStream.write('Some data');
writeStream.write('Some more data');

writeStream.end();

writeStream.on('finish', () => {
  console.log('Finished writing');
});

writeStream.on('error', err => {
  console.error(err);
});

```

## Exercícios Práticos

1. **Leitura de Arquivos**: Crie um script que leia o conteúdo de um arquivo chamado `data.txt` e exiba no console.
2. **Escrita de Arquivos**: Crie um script que escreva um texto fornecido pelo usuário em um arquivo chamado `output.txt`.
3. **Manipulação de Diretórios**: Crie um script que crie um novo diretório chamado `test-directory`, leia o conteúdo desse diretório e exiba os nomes dos arquivos e subdiretórios contidos nele.
4. **Streams**: Crie um script que leia um arquivo grande (`large-file.txt`) usando streams e exiba seu conteúdo no console em partes.
5. **Copiar Arquivo**: Crie um script que copie o conteúdo de um arquivo `source.txt` para um novo arquivo `destination.txt` usando streams.

---

# 6. Trabalhando com HTTP

O Node.js possui um módulo interno chamado `http` que permite criar servidores web e lidar com requisições e respostas HTTP. Este módulo fornece a base para a construção de aplicações web e APIs.

**6.1 Introdução ao HTTP**

HTTP (HyperText Transfer Protocol) é o protocolo fundamental usado na web para a comunicação entre clientes (geralmente navegadores web) e servidores. Ele define como as mensagens são formatadas e transmitidas, e quais ações os servidores e navegadores devem tomar em resposta a diferentes comandos.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f7feecbd-7058-4805-b782-5c71283c99cc/e12521b6-316f-479b-beb5-e7601a67e54f/Untitled.png)

**Componentes de uma Requisição HTTP**

1. **Método HTTP**: Define a ação a ser realizada. Os métodos mais comuns incluem:
    - GET: Solicita dados de um servidor.
    - POST: Envia dados para um servidor para criar ou atualizar recursos.
    - PUT: Atualiza um recurso existente no servidor.
    - DELETE: Remove um recurso do servidor.
2. **URL (Uniform Resource Locator)**: Especifica o endereço do recurso a ser acessado.
3. **Headers**: Contêm informações adicionais sobre a requisição, como tipo de conteúdo, autenticação, etc.
4. **Body**: Usado para enviar dados ao servidor (geralmente em requisições POST e PUT).

**Componentes de uma Resposta HTTP**

1. **Status Code**: Indica o resultado da requisição. Alguns códigos comuns são:
    - 200 OK: A requisição foi bem-sucedida.
    - 404 Not Found: O recurso solicitado não foi encontrado.
    - 500 Internal Server Error: Ocorreu um erro no servidor.
2. **Headers**: Contêm informações sobre a resposta, como tipo de conteúdo, tamanho, etc.
3. **Body**: Contém os dados retornados pelo servidor, como HTML, JSON, etc.

## 6.2 Criando um Servidor HTTP Básico

Para criar um servidor HTTP básico, você precisa utilizar o módulo `http` e definir como o servidor deve responder às requisições.

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\\\\n');
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server running at <http://localhost>:${PORT}/`);
});

```

Executando o servidor:

```bash
node index.js
```

Depois de executar este comando, você pode abrir seu navegador e acessar `http://localhost:3000` para ver a mensagem "Hello, World!" exibida.

## 6.3 Tratamento de Requisições e Respostas

### Requisições (Requests)

As requisições HTTP possuem várias propriedades que podem ser acessadas para obter informações sobre a solicitação.

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
  console.log(`Request method: ${req.method}`);
  console.log(`Request URL: ${req.url}`);
  console.log(`Request headers: ${JSON.stringify(req.headers)}`);

  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Request received\\\\n');
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server running at <http://localhost>:${PORT}/`);
});

```

### Respostas (Responses)

Para enviar uma resposta ao cliente, você pode definir o status, os headers e o corpo da resposta.

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/plain') {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello, plain text!\\\\n');
  } else if (req.url === '/json') {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'application/json');
    res.end(JSON.stringify({ message: 'Hello, JSON!' }));
  } else {
    res.statusCode = 404;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Not Found\\\\n');
  }
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server running at <http://localhost>:${PORT}/`);
});

```

## 6.4 Middleware e Roteamento

Para projetos maiores, é comum usar bibliotecas como `express` para facilitar o gerenciamento de rotas e middlewares.

### Roteamento Básico com `http`

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.method === 'GET' && req.url === '/') {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello, GET request!\\\\n');
  } else if (req.method === 'POST' && req.url === '/data') {
    let body = '';
    req.on('data', chunk => {
      body += chunk.toString();
    });
    req.on('end', () => {
      res.statusCode = 200;
      res.setHeader('Content-Type', 'application/json');
      res.end(JSON.stringify({ receivedData: body }));
    });
  } else {
    res.statusCode = 404;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Not Found\\\\n');
  }
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server running at <http://localhost>:${PORT}/`);
});

```

## Exercícios Práticos

1. **Servidor HTTP Básico**: Crie um servidor HTTP que responde com "Hello, World!" para qualquer requisição.
2. **Requisições e Respostas**: Crie um servidor HTTP que exibe o método, URL e cabeçalhos da requisição no console, e responde com "Request received".
3. **Roteamento**: Implemente um servidor HTTP que responda de maneira diferente para as URLs `/plain` (texto simples) e `/json` (JSON).
4. **Recebendo Dados**: Crie um servidor HTTP que aceite requisições POST para a URL `/data`, receba o corpo da requisição e responda com os dados recebidos em formato JSON.
5. **Gerenciamento de Erros**: Implemente um servidor HTTP que responda com "Not Found" para qualquer rota não definida e com "Method Not Allowed" para métodos HTTP não suportados.

---

# 7. Express

## 7.1 Introdução ao Express

Express é um framework web para Node.js que simplifica o desenvolvimento de aplicações web e APIs. Ele fornece uma série de recursos robustos para criar servidores e gerenciar rotas, middlewares, e muito mais.

### Instalação do Express

Para começar a usar o Express, você precisa instalá-lo em seu projeto Node.js. Use o npm para instalar o pacote:

```
npm install express
```

## 7.2 Configuração e Primeiros Passos

### Criando um Servidor Express

**Configuração Básica**: Crie um arquivo chamado `app.js` e adicione o seguinte código para configurar um servidor básico:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hello, Express!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

**Executando o Servidor**: Para iniciar o servidor, execute o comando:

```
node app.js
```

**Acessando o Servidor**: Abra seu navegador e acesse `http://localhost:3000`. Você deverá ver a mensagem "Hello, Express!".

## 7.3 Roteamento Avançado

O roteamento no Express é uma forma de determinar como uma aplicação responde a uma requisição de um cliente em um endpoint específico.

### Definindo Rotas

Você pode definir rotas para diferentes métodos HTTP (`GET`, `POST`, `PUT`, `DELETE`, etc.) e caminhos.

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('GET request to the homepage');
});

app.post('/submit', (req, res) => {
  res.send('POST request to /submit');
});

app.put('/update', (req, res) => {
  res.send('PUT request to /update');
});

app.delete('/delete', (req, res) => {
  res.send('DELETE request to /delete');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});
```

## 7.4 Middleware Customizados

Middlewares são funções que têm acesso ao objeto de requisição (`req`), ao objeto de resposta (`res`) e à próxima função middleware no ciclo de requisição-resposta da aplicação.

### Criando um Middleware

Você pode criar middlewares para várias finalidades, como fazer logging, verificar autenticação, etc.

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware de Logging
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
};

app.use(logger);

app.get('/', (req, res) => {
  res.send('Hello, Middleware!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

## 7.5 Tratamento de Erros

O tratamento de erros no Express é feito através de middlewares de erro. Um middleware de erro tem quatro argumentos: `err`, `req`, `res`, e `next`.

### Exemplo de Middleware de Erro

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware de Tratamento de Erros
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
};

app.get('/', (req, res) => {
  throw new Error('BROKEN');
});

app.use(errorHandler);

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

## Exercícios Práticos

1. **Servidor Express Básico**: Crie um servidor Express que responda com "Hello, Express!" para uma requisição GET na rota raiz (`/`).
2. **Definição de Rotas**: Implemente um servidor Express com rotas para métodos `GET`, `POST`, `PUT`, e `DELETE`. Cada rota deve responder com uma mensagem diferente.
3. **Middleware de Logging**: Crie um middleware de logging que registre o método e a URL de cada requisição recebida.
4. **Middleware de Autenticação**: Implemente um middleware de autenticação simples que verifique a presença de um cabeçalho específico (`Authorization`) e permita ou bloqueie o acesso a uma rota.
5. **Tratamento de Erros**: Crie um middleware de tratamento de erros que capture quaisquer erros gerados durante o processamento das requisições e responda com um status 500 e uma mensagem de erro.

---

# 8. Bases de Dados

Conectar o Node.js a bancos de dados é uma tarefa comum no desenvolvimento de aplicações web. Neste tópico, abordaremos a conexão com bancos de dados SQL usando ORM (Object-Relational Mapping) e a configuração de um banco de dados utilizando Docker.

## 8.1 Conectando Node.js a Bancos de Dados SQL

Para se conectar a bancos de dados SQL como MySQL ou PostgreSQL, utilizaremos o Sequelize, um ORM popular para Node.js que facilita a interação com bancos de dados.

### Instalando o Sequelize e o Driver do Banco de Dados

**Instalar o Sequelize**:

```
npm install sequelize
```

**Instalar o Driver do Banco de Dados** (exemplo com PostgreSQL):

```
npm install pg pg-hstore
```

### Configurando o Sequelize

**Configuração Básica**: Crie um arquivo `config/database.js` para configurar a conexão com o banco de dados.

```jsx
const { Sequelize } = require('sequelize');

const sequelize = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: 'postgres', // ou 'mysql', 'sqlite', etc.
});

module.exports = sequelize;
```

**Testando a Conexão**: Crie um arquivo `test-connection.js` para testar a conexão com o banco de dados.

```jsx
const sequelize = require('./config/database');

async function testConnection() {
  try {
    await sequelize.authenticate();
    console.log('Connection has been established successfully.');
  } catch (error) {
    console.error('Unable to connect to the database:', error);
  }
}

testConnection();
```

## 8.2 Definindo Modelos e Executando Operações

Os modelos no Sequelize representam tabelas no banco de dados. Você pode definir modelos para criar, ler, atualizar e excluir dados.

### Definindo um Modelo

**Criar um Modelo**: Crie um arquivo `models/user.js` para definir um modelo de usuário.

```jsx
const { DataTypes } = require('sequelize');
const sequelize = require('../config/database');

const User = sequelize.define('User', {
  username: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  email: {
    type: DataTypes.STRING,
    allowNull: false,
  },
});

module.exports = User;
```

**Sincronizar o Modelo**: Crie um arquivo `sync.js` para sincronizar o modelo com o banco de dados.

```jsx
const sequelize = require('./config/database');
const User = require('./models/user');

async function syncDatabase() {
  try {
    await sequelize.sync({ force: true }); // 'force: true' recria as tabelas a cada execução
    console.log('Database & tables created!');
  } catch (error) {
    console.error('Error syncing database:', error);
  }
}

syncDatabase();
```

## 8.3 Realizando Operações CRUD

### Criando Registros

```jsx
const User = require('./models/user');

async function createUser() {
  try {
    const user = await User.create({ username: 'john_doe', email: 'john@example.com' });
    console.log('User created:', user);
  } catch (error) {
    console.error('Error creating user:', error);
  }
}

createUser();
```

### Lendo Registros

```jsx
const User = require('./models/user');

async function getUsers() {
  try {
    const users = await User.findAll();
    console.log('Users:', users);
  } catch (error) {
    console.error('Error fetching users:', error);
  }
}

getUsers();
```

### Atualizando Registros

```jsx
const User = require('./models/user');

async function updateUser() {
  try {
    const user = await User.findOne({ where: { username: 'john_doe' } });
    if (user) {
      user.email = 'new_email@example.com';
      await user.save();
      console.log('User updated:', user);
    }
  } catch (error) {
    console.error('Error updating user:', error);
  }
}

updateUser();
```

### Excluindo Registros

```jsx
const User = require('./models/user');

async function deleteUser() {
  try {
    const user = await User.findOne({ where: { username: 'john_doe' } });
    if (user) {
      await user.destroy();
      console.log('User deleted');
    }
  } catch (error) {
    console.error('Error deleting user:', error);
  }
}

deleteUser();
```

## 8.4 Rodando um Banco de Dados Usando Docker

Docker é uma plataforma que permite criar, gerenciar e executar contêineres que podem conter tudo o que você precisa para executar uma aplicação, incluindo o sistema operacional, bibliotecas e dependências.

### Configurando o Docker para PostgreSQL

1. **Instalar o Docker**: Baixe e instale o Docker a partir do [site oficial](https://www.docker.com/).
2. **Rodar o Banco de Dados**: Use o seguinte comando para rodar um contêiner PostgreSQL.

```
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

**Conectando ao Banco de Dados**: Configure o Sequelize para se conectar ao contêiner PostgreSQL.

```jsx
const sequelize = new Sequelize('postgres', 'postgres', 'mysecretpassword', {
  host: 'localhost',
  dialect: 'postgres',
});

```

## Exercícios Práticos

1. **Configuração do Sequelize**: Configure o Sequelize para se conectar a um banco de dados PostgreSQL ou MySQL e teste a conexão.
2. **Definição de Modelos**: Crie um modelo de `Product` com os campos `name` e `price`. Sincronize o modelo com o banco de dados.
3. **Operações CRUD**: Implemente funções para criar, ler, atualizar e excluir registros no modelo `Product`.
4. **Docker**: Configure um contêiner Docker para PostgreSQL e conecte-o ao seu projeto Node.js usando Sequelize.
5. **Consultas Avançadas**: Implemente consultas avançadas no Sequelize, como filtragem por condições específicas e ordenação de resultados.

---

# 9. Autenticação e Autorização

A autenticação e a autorização são partes fundamentais de qualquer aplicação web, garantindo que apenas usuários autorizados possam acessar certos recursos ou executar determinadas ações. Neste tópico, vamos focar na autenticação básica usando JWT (JSON Web Tokens).

## 9.1 Introdução à Autenticação com JWT

JWT é um padrão aberto (RFC 7519) que define uma maneira compacta e segura de transmitir informações entre as partes como um objeto JSON. Essas informações podem ser verificadas e confiadas porque são assinadas digitalmente.

### Componentes de um JWT

Um JWT é composto por três partes separadas por pontos (`.`):

1. **Header**: Contém o tipo de token e o algoritmo de assinatura.
2. **Payload**: Contém as declarações (claims). São as informações que você quer transmitir.
3. **Signature**: É a assinatura gerada a partir do header, payload e uma chave secreta.

Exemplo de um JWT:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

```

## 9.2 Instalando Dependências

Para implementar a autenticação com JWT, vamos utilizar dois pacotes: `jsonwebtoken` para gerar e verificar tokens JWT, e `bcrypt` para hashing de senhas.

Instale as dependências necessárias:

```
npm install jsonwebtoken bcrypt
```

## 9.3 Gerando e Verificando Tokens

### Gerando um Token

**Criar um arquivo `auth.js` para gerenciar a autenticação**:

```jsx
const jwt = require('jsonwebtoken');

const SECRET_KEY = 'your_secret_key';

function generateToken(user) {
  const token = jwt.sign({ id: user.id, username: user.username }, SECRET_KEY, {
    expiresIn: '1h', // Token expira em 1 hora
  });
  return token;
}

module.exports = { generateToken };

```

### Verificando um Token

**Adicionar a função para verificar tokens em `auth.js`**:

```jsx
function verifyToken(token) {
  try {
    const decoded = jwt.verify(token, SECRET_KEY);
    return decoded;
  } catch (err) {
    return null;
  }
}

module.exports = { generateToken, verifyToken };

```

## 9.4 Hashing de Senhas

Para armazenar senhas de forma segura, devemos utilizar hashing. O `bcrypt` é uma biblioteca popular para hashing de senhas.

### Hashing de Senhas

**Criar um arquivo `user.js` para gerenciar usuários**:

```jsx
const bcrypt = require('bcrypt');

async function hashPassword(password) {
  const salt = await bcrypt.genSalt(10);
  const hashedPassword = await bcrypt.hash(password, salt);
  return hashedPassword;
}

async function verifyPassword(password, hashedPassword) {
  const isMatch = await bcrypt.compare(password, hashedPassword);
  return isMatch;
}

module.exports = { hashPassword, verifyPassword };

```

## 9.5 Implementando Autenticação em uma Aplicação Express

Vamos agora integrar a autenticação com JWT em uma aplicação Express.

### Configurando Rotas de Autenticação

**Criar as rotas de login e registro**:

```jsx
const express = require('express');
const { generateToken } = require('./auth');
const { hashPassword, verifyPassword } = require('./user');
const app = express();
const PORT = 3000;

app.use(express.json());

const users = []; // Simulação de banco de dados

app.post('/register', async (req, res) => {
  const { username, password } = req.body;
  
  const hashedPassword = await hashPassword(password);
  
  const user = { id: users.length + 1, username, password: hashedPassword };
  users.push(user);
  
  res.status(201).send('User registered');
});

app.post('/login', async (req, res) => {
  const { username, password } = req.body;
  
  const user = users.find(u => u.username === username);
  if (!user) {
    return res.status(400).send('Invalid credentials');
  }
  
  const isMatch = await verifyPassword(password, user.password);
  if (!isMatch) {
    return res.status(400).send('Invalid credentials');
  }
  
  const token = generateToken(user);
  res.send({ token });
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

## 9.6 Protegendo Rotas com JWT

Para proteger rotas, precisamos verificar o token JWT antes de permitir o acesso ao recurso.

### Middleware de Autenticação

**Criar um middleware para verificar tokens**:

```jsx
const { verifyToken } = require('./auth');

function authMiddleware(req, res, next) {
  const token = req.header('Authorization').replace('Bearer ', '');
  
  const user = verifyToken(token);
  if (!user) {
    return res.status(401).send('Access denied');
  }
  
  req.user = user;
  next();
}

module.exports = authMiddleware;

```

**Usar o middleware em uma rota protegida**:

```jsx
const express = require('express');
const { generateToken } = require('./auth');
const { hashPassword, verifyPassword } = require('./user');
const authMiddleware = require('./authMiddleware');
const app = express();
const PORT = 3000;

app.use(express.json());

const users = []; // Simulação de banco de dados

app.post('/register', async (req, res) => {
  const { username, password } = req.body;
  
  const hashedPassword = await hashPassword(password);
  
  const user = { id: users.length + 1, username, password: hashedPassword };
  
  users.push(user);
  
  res.status(201).send('User registered');
});

app.post('/login', async (req, res) => {
  const { username, password } = req.body;
  const user = users.find(u => u.username === username);
  if (!user) {
    return res.status(400).send('Invalid credentials');
  }
  
  const isMatch = await verifyPassword(password, user.password);
  if (!isMatch) {
    return res.status(400).send('Invalid credentials');
  }
  
  const token = generateToken(user);
  res.send({ token });
});

app.get('/protected', authMiddleware, (req, res) => {
  res.send('This is a protected route');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Exercícios Práticos

1. **Registro e Login**: Implemente as rotas de registro e login em uma aplicação Express e teste a criação de usuários e a geração de tokens JWT.
2. **Protegendo Rotas**: Adicione um middleware de autenticação para proteger uma rota e teste o acesso com e sem um token JWT válido.
3. **Hashing de Senhas**: Crie funções para hash e verificação de senhas usando bcrypt e integre-as nas rotas de registro e login.
4. **Refresh Tokens**: Implemente a lógica de refresh tokens para renovar tokens JWT expirados de forma segura.
5. **Permissões**: Adicione diferentes níveis de permissão aos usuários e proteja rotas específicas com base nas permissões do usuário.
