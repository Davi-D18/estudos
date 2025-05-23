
## Sumário:
[Sumário:](#Sumário:)
[Introdução](#Introdução)
[==**Importante:**==](#Importante:)
[Sistema CPV](#Sistema CPV)
[1. Introdução ao TypeScript](#1. Introdução ao TypeScript)
[O que é TypeScript?](#O que é TypeScript?)
[Por que usar TypeScript?](#Por que usar TypeScript?)
[Um breve exemplo de código](#Um breve exemplo de código)
[2. Configurando um Ambiente TypeScript](#2. Configurando um Ambiente TypeScript)
[Instalação do Node.js e NPM](#Instalação do Node.js e NPM)
[Instalando o TypeScript](#Instalando o TypeScript)
[Configurando o compilador TypeScript](#Configurando o compilador TypeScript)
[Exemplo de Projeto TypeScript](#Exemplo de Projeto TypeScript)
[Utilizando o `ts-node-dev`](#Utilizando o ts-node-dev)
[Instalação](#Instalação)
[Configuração](#Configuração)
[Executando o Projeto](#Executando o Projeto)
[3. Tipos Básicos em TypeScript](#3. Tipos Básicos em TypeScript)
[Tipos Primitivos](#Tipos Primitivos)
[Exercícios para Praticar](#Exercícios para Praticar)
[4. Arrays em TypeScript](#4. Arrays em TypeScript)
[Definindo Arrays](#Definindo Arrays)
[Operações Comuns em Arrays](#Operações Comuns em Arrays)
[Métodos Avançados de Arrays](#Métodos Avançados de Arrays)
[Exercícios para Praticar](#Exercícios para Praticar)
[5. Funções em TypeScript](#5. Funções em TypeScript)
[Definindo Funções](#Definindo Funções)
[Parâmetros Opcionais e Padrões](#Parâmetros Opcionais e Padrões)
[Tipos Avançados em Funções](#Tipos Avançados em Funções)
[Exercícios para Praticar](#Exercícios para Praticar)
[6. Interfaces e Tipos Customizados](#6. Interfaces e Tipos Customizados)
[Definindo Interfaces](#Definindo Interfaces)
[Usando Tipos (Type Aliases)](#Usando Tipos (Type Aliases))
[Exercícios para Praticar](#Exercícios para Praticar)
[7. Orientação a Objetos em TypeScript](#7. Orientação a Objetos em TypeScript)
[Classes em TypeScript](#Classes em TypeScript)
[Encapsulamento e Modificadores de Acesso](#Encapsulamento e Modificadores de Acesso)
[Polimorfismo](#Polimorfismo)
[**Exercícios para Praticar**](#Exercícios para Praticar)
[8. Generics em TypeScript](#8. Generics em TypeScript)
[O que são Generics?](#O que são Generics?)
[Generics com Interfaces](#Generics com Interfaces)
[Generics em Classes](#Generics em Classes)
[Generics com Restrições](#Generics com Restrições)
[Exercícios para Praticar](#Exercícios para Praticar)
[9. Tipos Avançados e Utilitários em TypeScript](#9. Tipos Avançados e Utilitários em TypeScript)
[Tipos Union e Intersection](#Tipos Union e Intersection)
[Tipos Condicionais](#Tipos Condicionais)
[Utilitários Comuns](#Utilitários Comuns)
[Exercícios para Praticar](#Exercícios para Praticar)
---
# Introdução
Olá, muito obrigado por ter acessado esse guia, ele foi pensado e desenvolvido com muito carinho com o objetivo de ajudar você que está começando na programação.🧡
Com esse guia você vai ser capaz de dar os seus primeiros passos práticos no mundo da programação com TypeScript.
Não esquece de me seguir no Instagram ==**[@umporcentoprog](https://www.instagram.com/umporcentoprog/)**== ==que lá eu trago conteúdo educacional de programação todos os dias, e é por lá que eu solto esses guias gratuitos, como esse que você está lendo!==
  
## ==**Importante:**==
Para tirar melhor proveito desse guia, é bom que **você já tenha uma boa base de JavaScript** básico, caso você não tenha, acesse agora mesmo o meu ==**[Guia Gratuito de JavaScript](https://www.notion.so/guia-javascript-90241f2f64f140d1a77fbaaca4da32ce?pvs=21)**== **[](https://www.notion.so/guia-javascript-90241f2f64f140d1a77fbaaca4da32ce?pvs=21)**e pratique lá antes de continuar com seus estudos em TypeScript.
  
## Sistema CPV
O sistema CPV é um sistema de 3 passos para aprender programação e aplicar os conceitos aprendidos. É o método que eu usei quando estava começando na programação e que uso até hoje para aprender novas tecnologias.
CPV Significa:
**Conceito** → Aprender um conceito, a teoria;
**Pratica** → Praticar o conceito aprendido com exercícios ou projetos práticos;
**Vitrine** → Expor o que você aprendeu para o mundo, colocar em um repositório do GitHub, fazer um post no Linkedin, enfim, faz uma vitrine do seu conhecimento.
Recomendo fortemente que você aplique esse sistema para tirar o melhor proveito desse guia.
  
---
  
# 1. Introdução ao TypeScript
### O que é TypeScript?
TypeScript é uma linguagem de programação desenvolvida pela Microsoft que adiciona tipos estáticos ao JavaScript. Isso significa que, enquanto o JavaScript é dinâmico e mais flexível, o TypeScript ajuda a capturar erros antes mesmo da execução do código, durante a fase de desenvolvimento! 🛠️
Com TypeScript, você pode escrever aplicações mais robustas e com menos bugs. É especialmente útil em projetos grandes, onde a complexidade e o número de desenvolvedores envolvidos tornam o controle de qualidade mais desafiador.
### Por que usar TypeScript?
1. **Segurança de tipo:** Reduz os bugs em tempo de execução ao verificar os tipos durante a compilação.
2. **Ferramentas de desenvolvimento:** Aproveite autocompletação poderosa, refatoração e muito mais.
3. **Compatibilidade com JavaScript:** O TypeScript é um superset de JavaScript, então todo código JavaScript é também um código TypeScript válido.
4. **Adoção na comunidade:** Grandes frameworks como Angular, React e Vue.js têm adotado e recomendado o uso de TypeScript para projetos de grande escala.
### Um breve exemplo de código
Vamos ver uma rápida comparação para entender o poder do TypeScript:
**JavaScript:**
```JavaScript
function soma(a, b) {
    return a + b;
}
console.log(soma(5, "3"));  // Resultado: "53"
```
**TypeScript:**
```TypeScript
function soma(a: number, b: number): number {
    return a + b;
}
console.log(soma(5, 3));  // Resultado: 8
// O TypeScript emitiria um erro se tentássemos passar uma string aqui.
```
No exemplo TypeScript, definimos tipos para os parâmetros e para o retorno da função. Isso ajuda a evitar erros como a concatenação acidental de números e strings, um problema comum em JavaScript.
Esse é o começo da jornada com TypeScript! Com esses fundamentos, você já começa a perceber as vantagens de adicionar tipos ao JavaScript. No próximo capítulo, vamos configurar o ambiente TypeScript para começar a codar. 🎯
  
---
  
# 2. Configurando um Ambiente TypeScript
### Instalação do Node.js e NPM
Antes de instalar o TypeScript, você precisa ter o Node.js e o NPM (Node Package Manager) instalados no seu sistema. O Node.js é um runtime de JavaScript que permite executar código JS no seu computador, e o NPM é o gerenciador de pacotes que usaremos para instalar o TypeScript.
1. **Baixe e instale o Node.js**: Visite [nodejs.org](https://nodejs.org/) e baixe a versão recomendada para a maioria dos usuários.
2. **Verifique a instalação**: Abra seu terminal e digite os seguintes comandos para verificar se o Node.js e o NPM foram instalados corretamente:  
    Você deverá ver as versões instaladas exibidas no terminal.  
    
    ```Shell
    node -v
    npm -v
    ```
    
### Instalando o TypeScript
Com o Node.js e o NPM prontos, instalar o TypeScript é um processo simples:
```Shell
npm install -g typescript
```
Este comando instala o TypeScript globalmente em seu sistema, permitindo que você o use em qualquer projeto.
### Configurando o compilador TypeScript
O próximo passo é configurar o compilador TypeScript. Isso é feito através de um arquivo chamado `tsconfig.json`, que define como o TypeScript compila o código JS.
1. **Crie um novo projeto**: Crie uma nova pasta para o seu projeto e navegue até ela no terminal.
2. **Inicialize um projeto Node.js**:  
    Isso cria um arquivo  
    `package.json` padrão.
    
    ```Shell
    npm init -y
    ```
    
3. **Crie um arquivo** `**tsconfig.json**`:
    - Você pode gerar um `tsconfig.json` padrão com o seguinte comando:
        
        ```Shell
        tsc --init
        ```
        
    - Abra o `tsconfig.json` e ajuste as configurações conforme necessário. As mais importantes incluem:
        - `"target": "es6"`: Define a versão do ECMAScript para a saída do JS.
        - `"module": "commonjs"`: Define o sistema de módulos.
        - `"strict": true`: Ativa todas as restrições de tipo para uma segurança máxima.
### Exemplo de Projeto TypeScript
Para garantir que tudo está funcionando, vamos criar um simples script TypeScript:
1. **Crie um arquivo** `**index.ts**`:
    - Adicione o seguinte código:
        
        ```TypeScript
        let message: string = "Hello, TypeScript!";
        console.log(message);
        ```
        
2. **Compile seu código**:
    
    ```Shell
    tsc index.ts
    ```
    
    Isso deve criar um arquivo `index.js` compilado a partir do seu TypeScript.
    
3. **Execute o script**:
    
    ```Shell
    node index.js
    ```
    
    Você deve ver "Hello, TypeScript!" sendo impresso no terminal.
    
  
### Utilizando o `ts-node-dev`
O `ts-node-dev` combina o `ts-node`, que permite a execução de TypeScript diretamente no Node.js sem compilação prévia, com a capacidade de monitorar mudanças nos arquivos do projeto e reiniciar automaticamente. É uma ferramenta perfeita para desenvolvimento rápido, pois você não precisa recompilar seu código manualmente a cada mudança.
### Instalação
Para começar a usar o `ts-node-dev`, primeiro você precisa instalá-lo. Como é uma ferramenta de desenvolvimento, é uma boa prática instalá-la como uma dependência de desenvolvimento em seu projeto:
```Shell
npm install --save-dev ts-node-dev
```
### Configuração
Com o `ts-node-dev` instalado, você pode configurá-lo para executar seu projeto. Adicione um script no seu `package.json` para facilitar a execução:
```JSON
"scripts": {
    "start": "ts-node-dev --respawn --transpile-only ./index.ts"
}
```
- `**-respawn**`: garante que o processo seja reiniciado após cada alteração.
- `**-transpile-only**`: acelera a execução ao pular as verificações de tipo completas do TypeScript (que você pode querer em um ambiente de produção).
### Executando o Projeto
Para rodar seu projeto com `ts-node-dev`, basta usar o comando:
```Shell
npm run start
```
Isso inicia seu aplicativo e monitora qualquer alteração nos arquivos TypeScript, reiniciando automaticamente o servidor sempre que você salvar um arquivo. Isso é incrivelmente útil durante o desenvolvimento, pois você vê as alterações em tempo real sem a necessidade de reiniciar manualmente o servidor.
Agora que seu ambiente está configurado, você está pronto para mergulhar mais fundo no TypeScript! No próximo capítulo, vamos discutir os tipos básicos e como usá-los para melhorar seu código. 🌟
  
---
  
# 3. Tipos Básicos em TypeScript
TypeScript traz uma camada adicional de segurança ao JavaScript através da tipagem estática. Isso significa que você define tipos para suas variáveis e funções, o que ajuda o compilador a detectar erros antes que seu código seja executado. Vamos explorar os tipos básicos que você usará na maioria dos projetos.
### Tipos Primitivos
1. **Boolean**
    
    - O tipo mais simples, `boolean`, representa um valor lógico: verdadeiro ou falso.
    
    ```TypeScript
    let estaAtivo: boolean = true;
    ```
    
2. **Number**
    
    - Assim como no JavaScript, todos os números em TypeScript são valores de ponto flutuante. TypeScript fornece suporte tanto para números inteiros quanto para valores de ponto flutuante.
    
    ```TypeScript
    let total: number = 0;
    let pi: number = 3.14159;
    ```
    
3. **String**
    
    - Para textos e caracteres, use o tipo `string`. Você pode usar aspas simples (' '), aspas duplas (" ") ou crases ( ) para strings que precisam de interpolação ou múltiplas linhas.
    
    ```TypeScript
    let nome: string = "João";
    let saudacao: string = `Olá, ${nome}!`;
    ```
    
4. **Array**
    
    - Arrays podem ser escritos de duas formas: usando o tipo dos elementos seguido de `[]` ou usando um tipo de array genérico.
    
    ```TypeScript
    let numeros: number[] = [1, 2, 3];
    let frutas: Array<string> = ["maçã", "banana", "cereja"];
    ```
    
5. **Tuple**
    
    - Os tuples permitem expressar um array com um número fixo de elementos cujos tipos são conhecidos, mas não precisam ser iguais.
    
    ```TypeScript
    let endereco: [string, number] = ["Av. Paulista", 1578];
    ```
    
6. **Enum**
    
    - Um `enum` permite definir um conjunto de constantes nomeadas. O TypeScript suporta numéricos e baseados em string.
    
    ```TypeScript
    enum Cor {Vermelho, Verde, Azul};
    let c: Cor = Cor.Verde;
    ```
    
7. **Any**
    
    - Use `any` para capturar valores cujo tipo não é importante e sobre os quais você não quer realizar checagem de tipo. Ideal para migração de JavaScript para TypeScript.
    
    ```TypeScript
    let variavelIndefinida: any = 4;
    variavelIndefinida = "talvez uma string";
    ```
    
8. **Void, Null e Undefined**
    
    - `void` é usado em funções que não retornam nada. `null` e `undefined` são subtipos de todos os outros tipos.
    
    ```TypeScript
    function alerta(): void {
        alert("Esta é uma mensagem de alerta!");
    }
    ```
    
### Exercícios para Praticar
1. **Trabalhando com Tipos:**
    - Crie variáveis para cada tipo básico e imprima-as.
    - Tente atribuir valores incorretos a essas variáveis para ver o que acontece.
2. **Função com Tipos:**
    - Escreva uma função que aceita um array de números e retorna a soma de todos os elementos.
    - Assegure-se de tipar tanto a entrada quanto a saída da função.
3. **Enumerações:**
    - Crie um enum para representar os dias da semana e use-o em uma função que imprime uma mensagem de acordo com o dia passado.
4. **Tuplas:**
    - Crie uma tupla que representa um produto (com nome e preço). Use essa tupla em uma função que imprime o nome e o preço do produto.
5. **Any:**
    - Crie uma variável do tipo `any` e atribua diferentes tipos de valores a ela. Note como o TypeScript não emite erros nesse caso.
6. **Void, Null e Undefined:**
    - Crie uma função que não retorna nada (`void`) e outra que retorna `undefined`. Compare as duas.
Com esse conhecimento sobre tipos básicos, você está pronto para escrever código TypeScript mais seguro e eficiente! No próximo capítulo, exploraremos como utilizar arrays em detalhes. 🚀
  
---
  
# 4. Arrays em TypeScript
Arrays em TypeScript são utilizados para armazenar múltiplos valores em uma única variável. Com a adição de tipos, o TypeScript permite que você defina o tipo dos elementos dentro do array, garantindo maior controle e segurança sobre os dados que você manipula.
### Definindo Arrays
1. **Array com Tipo Único**
    
    - Você pode declarar um array onde todos os elementos são do mesmo tipo usando a notação de colchetes após o tipo de dado.
    
    ```TypeScript
    let numeros: number[] = [1, 2, 3, 4, 5];
    let nomes: string[] = ["Ana", "Beatriz", "Carlos"];
    ```
    
2. **Array com Generic Array Type**
    
    - Alternativamente, TypeScript oferece a sintaxe genérica `Array<tipo>` para declarar um array.
    
    ```TypeScript
    let frutas: Array<string> = ["maçã", "banana", "manga"];
    let pontos: Array<number> = [9.5, 7.3, 8.6];
    ```
    
  
### Operações Comuns em Arrays
- **Adicionando Elementos**
    
    - Use o método `.push()` para adicionar elementos ao final de um array.
    
    ```TypeScript
    numeros.push(6);
    ```
    
- **Removendo Elementos**
    
    - Use `.pop()` para remover o último elemento de um array.
    
    ```TypeScript
    let ultimoNumero = numeros.pop();  // Remove e retorna o último elemento
    ```
    
- **Acessando Elementos**
    
    - Acesse um elemento específico pelo seu índice.
    
    ```TypeScript
    let primeiroNome = nomes[0];  // "Ana"
    ```
    
- **Iterando sobre Elementos**
    
    - Arrays em TypeScript podem ser iterados usando loops como `for` ou métodos como `.forEach()`.
    
    ```TypeScript
    numeros.forEach((numero) => {
        console.log(numero);
    });
    ```
    
### Métodos Avançados de Arrays
- **Filtrar Elementos**
    
    - Use `.filter()` para criar um novo array com elementos que satisfazem uma condição específica.
    
    ```TypeScript
    let numerosFiltrados = numeros.filter(n => n > 2);
    ```
    
- **Transformar Elementos**
    
    - O método `.map()` permite transformar cada elemento de um array e retornar um novo array com os elementos transformados.
    
    ```TypeScript
    let numerosDobrados = numeros.map(n => n * 2);
    ```
    
- **Reduzindo um Array**
    
    - O método `.reduce()` aplica uma função que resulta em um único valor resumido de todo o array.
    
    ```TypeScript
    let soma = numeros.reduce((acumulador, atual) => acumulador + atual, 0);
    ```
    
### Exercícios para Praticar
1. **Criação e Acesso:**
    - Crie um array de strings com os nomes de cinco cidades. Em seguida, escreva um código que imprime o nome da terceira cidade na lista.
2. **Adicionando e Removendo Elementos:**
    - Dado o array `[10, 20, 30, 40, 50]`, adicione o número `35` entre `30` e `40`, e depois remova o número `20` do array. Imprima o array final.
3. **Método** `**.map()**`**:**
    - Crie um array de números `[1, 2, 3, 4, 5]`. Use o método `.map()` para criar um novo array onde cada número é multiplicado por 3. Imprima o novo array.
4. **Filtrando Valores:**
    - Utilize o método `.filter()` para criar um novo array contendo apenas os números ímpares do array original `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`.
5. **Usando** `**.reduce()**` **para Soma:**
    - Dado um array de números `[5, 7, 10, 12, 15]`, utilize o método `.reduce()` para calcular e imprimir a soma total dos elementos do array.
  
Arrays são ferramentas versáteis e poderosas em TypeScript, permitindo gerenciar e processar conjuntos de dados com facilidade. No próximo capítulo, discutiremos como definir e usar funções em TypeScript para realizar tarefas e manipular dados de forma mais eficaz.
  
---
  
# 5. Funções em TypeScript
Funções são blocos fundamentais no desenvolvimento de software, permitindo reutilizar código e criar estruturas modulares. TypeScript adiciona uma camada de segurança adicional com a tipagem de parâmetros e valores de retorno, ajudando a evitar muitos erros comuns.
### Definindo Funções
1. **Função com Tipos nos Parâmetros e Retorno**
    
    - Em TypeScript, você pode especificar o tipo de cada parâmetro e o tipo do valor de retorno.
    
    ```TypeScript
    function soma(a: number, b: number): number {
        return a + b;
    }
    ```
    
2. **Funções Anônimas e Arrow Functions**
    
    - Funções anônimas e arrow functions também suportam tipagem nos parâmetros e no retorno.
    
    ```TypeScript
    const multiplica = (x: number, y: number): number => x * y;
    ```
    
### Parâmetros Opcionais e Padrões
- **Parâmetros Opcionais**
    
    - Parâmetros opcionais são marcados com um `?` e devem vir após os parâmetros obrigatórios.
    
    ```TypeScript
    function saudacao(nome: string, sobrenome?: string): string {
        return `Olá, ${nome} ${sobrenome || ''}!`;
    }
    ```
    
- **Parâmetros com Valores Padrão**
    
    - Você pode definir valores padrão para parâmetros, que serão usados caso nenhum valor seja fornecido.
    
    ```TypeScript
    function potencia(base: number, expoente: number = 2): number {
        return base ** expoente;
    }
    ```
    
### Tipos Avançados em Funções
- **Tipos de Função**
    
    - Você pode criar um tipo específico para uma função, que define a assinatura da função.
    
    ```TypeScript
    type OperacaoMatematica = (x: number, y: number) => number;
    const subtrai: OperacaoMatematica = (x, y) => x - y;
    ```
    
- **Overloads de Função**
    
    - TypeScript permite definir múltiplas assinaturas para uma função, conhecidas como overloads, permitindo que a função aceite diferentes tipos de parâmetros e retorne diferentes tipos de valores.
    
    ```TypeScript
    function ajustarValor(valor: number): number;
    function ajustarValor(valor: string): string;
    function ajustarValor(valor: any): any {
        return typeof valor === 'number' ? valor.toFixed(2) : valor.trim();
    }
    ```
    
### Exercícios para Praticar
1. **Implementando Funções:**
    - Escreva uma função `concatenaNomes` que recebe dois parâmetros, `nome` e `sobrenome`, e retorna o nome completo.
2. **Uso de Arrow Functions:**
    - Converta a função `soma` para uma arrow function e implemente a mesma lógica.
3. **Explorando Parâmetros Opcionais:**
    - Modifique a função `saudacao` para incluir um parâmetro opcional `titulo`, que se usado, precederá o nome no cumprimento.
4. **Trabalhando com Overloads:**
    - Crie uma função `ajustar` que pode receber tanto um `number` quanto uma `string`, retornando o valor ajustado conforme o tipo.
5. **Função com Valor Padrão:**
    - Implemente uma função `incrementa` que recebe um número e um valor de incremento opcional, que, se não fornecido, será `1`.
  
Essas informações e exercícios ajudarão a dominar o uso de funções em TypeScript, tornando seu código mais seguro e reutilizável. No próximo capítulo, mergulharemos em interfaces e tipos customizados para estruturar ainda melhor seu código.
  
---
  
# 6. Interfaces e Tipos Customizados
TypeScript oferece poderosas ferramentas para a definição de estruturas de dados complexas e contratos de função através de interfaces e tipos customizados. Neste capítulo, vamos explorar como essas definições podem ser usadas para tipar parâmetros de funções, garantindo que os dados passados e retornados sejam rigorosamente verificados.
### Definindo Interfaces
1. **Interface para Parâmetros de Função**
    
    - Defina uma interface que especifique a estrutura esperada para os parâmetros de uma função.
    
    ```TypeScript
    interface Usuario {
        nome: string;
        idade: number;
    }
    
    function imprimeUsuario(usuario: Usuario): void {
        console.log(`Nome: ${usuario.nome}, Idade: ${usuario.idade}`);
    }
    ```
    
2. **Interface com Método Opcional**
    
    - Interfaces podem incluir métodos opcionais, o que aumenta a flexibilidade na implementação.
    
    ```TypeScript
    interface Produto {
        nome: string;
        preco: number;
        descrever?(): string;
    }
    
    function etiquetaProduto(produto: Produto): string {
        return produto.descrever ? produto.descrever() : `${produto.nome} custa R$${produto.preco}`;
    }
    ```
    
### Usando Tipos (Type Aliases)
- **Type Alias para Funções**
    
    - Type aliases podem ser usados para definir assinaturas de funções, tornando o código mais limpo e organizado.
    
    ```TypeScript
     type ProcessadorPagamento = (quantia: number, conta: string) => boolean;
    
     function processarPagamento(processador: ProcessadorPagamento, quantia: number, conta: string) {
         return processador(quantia, conta);
     }
    ```
    
- **Combinando Tipos com Uniões**
    
    - Utilize uniões para criar tipos que podem aceitar múltiplas formas de dados.
    
    ```TypeScript
     type EntradaFormulario = string | number;
    
     function entradaDados(campo: string, valor: EntradaFormulario) {
         console.log(`Entrada para ${campo}: ${valor}`);
     }
    ```
    
### Exercícios para Praticar
1. **Interface para Funções:**
    - Defina uma interface `Contato` com propriedades para `email` e `telefone`. Crie uma função que aceite um `Contato` e imprima os detalhes de contato.
2. **Usando Type Alias em Funções:**
    - Crie um type alias `OperacaoMatematica` que define uma função que aceita dois números e retorna um número. Implemente funções para soma, subtração, multiplicação e divisão usando este alias.
3. **Interface com Métodos Opcionais:**
    - Crie uma interface `Configuracao` com uma propriedade opcional `background` (string). Escreva uma função que defina a configuração de um aplicativo e trate a ausência de `background`.
4. **Funções com Type Alias de União:**
    - Implemente uma função que aceite `string` ou `string[]` como entrada e retorne uma string sempre, tratando adequadamente a entrada caso seja um array.
5. **Parâmetros Complexos com Interfaces:**
    - Defina uma interface `Jogo` com `nome`, `preco` e um método opcional `jogar`. Crie uma função que aceite um `Jogo` e imprima uma descrição ou convide o usuário a jogar, se disponível.
Este capítulo mostra como interfaces e tipos customizados podem ser integrados em funções para criar aplicações robustas e tipicamente seguras em TypeScript. No próximo capítulo, abordaremos conceitos de orientação a objetos em maior profundidade.
  
---
  
# 7. Orientação a Objetos em TypeScript
TypeScript é uma linguagem que suporta os conceitos fundamentais de orientação a objetos como classes, interfaces, herança, e polimorfismo. Vamos detalhar como esses conceitos são implementados e utilizados em TypeScript para ajudar a organizar e estruturar melhor seu código.
### Classes em TypeScript
1. **Definindo e Instanciando Classes**
    
    - Classes são usadas como moldes para criar objetos. Aqui está um exemplo de como definir e instanciar uma classe.
    
    ```TypeScript
    class Pessoa {
        nome: string;
        idade: number;
    
        constructor(nome: string, idade: number) {
            this.nome = nome;
            this.idade = idade;
        }
    
        descrever(): string {
            return `Nome: ${this.nome}, Idade: ${this.idade}`;
        }
    }
    
    // Instanciando a classe Pessoa
    let pessoa1 = new Pessoa("Maria", 30);
    console.log(pessoa1.descrever());
    ```
    
2. **Herança e Instanciação**
    
    - Demonstração de como uma classe pode herdar de outra e como instanciar a classe derivada.
    
    ```TypeScript
    class Empregado extends Pessoa {
        salario: number;
    
        constructor(nome: string, idade: number, salario: number) {
            super(nome, idade); // Chama o construtor da classe base
            this.salario = salario;
        }
    
        descrever(): string {
            return `${super.descrever()}, Salário: R$${this.salario}`;
        }
    }
    
    // Instanciando a classe Empregado
    let empregado1 = new Empregado("João", 45, 5000);
    console.log(empregado1.descrever());
    ```
    
### Encapsulamento e Modificadores de Acesso
- **Classes com Encapsulamento**
    
    - Exemplo de como encapsular propriedades e permitir acesso controlado através de métodos.
    
    ```TypeScript
     class Conta {
         private saldo: number;
    
         constructor(saldoInicial: number) {
             this.saldo = saldoInicial;
         }
    
         depositar(valor: number): void {
             if (valor > 0) {
                 this.saldo += valor;
             }
         }
    
         obterSaldo(): number {
             return this.saldo;
         }
    
         protected calcularJuros(taxa: number): void {
             this.saldo += this.saldo * taxa;
         }
     }
    
     // Instanciando e usando a classe Conta
     let minhaConta = new Conta(1000);
     minhaConta.depositar(500);
     console.log(`Saldo atual: R$${minhaConta.obterSaldo()}`);
    ```
    
### Polimorfismo
- **Polimorfismo com Métodos Sobrescritos**
    
    - Como classes derivadas podem sobrescrever métodos de suas classes base.
    
    ```TypeScript
     class ContaPoupanca extends Conta {
         calcularJuros(): void {
             super.calcularJuros(0.02); // Aplica uma taxa de juros específica
         }
     }
    
     // Instanciando e usando a classe ContaPoupanca
     let poupanca = new ContaPoupanca(2000);
     poupanca.calcularJuros();
     console.log(`Saldo com juros: R$${poupanca.obterSaldo()}`);
    ```
    
  
### **Exercícios para Praticar**
1. **Criando e Instanciando Classes:**
    - Defina uma classe `Carro` com propriedades para `marca`, `modelo`, e `ano`. Adicione um método que imprime uma descrição do carro.
2. **Explorando Herança:**
    - Crie uma classe `CarroEletrico` que herda de `Carro` e adiciona uma propriedade para a capacidade da bateria.
3. **Uso de Modificadores de Acesso:**
    - Modifique a classe `Conta` para prevenir acesso direto ao saldo, fornecendo métodos para depositar e obter o saldo atual.
4. **Implementando Polimorfismo:**
    - Crie uma classe `ContaCorrente` que sobrescreve o método `calcularJuros` com uma taxa específica para contas correntes.
5. **Classes com Interfaces:**
    - Implemente uma interface `Motorizavel` com um método `ligarMotor`. Crie classes `Barco` e `Motocicleta` que implementam esta interface.
  
Este capítulo fornece uma visão geral sólida sobre como utilizar conceitos de orientação a objetos em TypeScript para construir aplicações mais robustas e organizadas. No próximo tópico, vamos explorar Generics, outro recurso poderoso do TypeScript.
  
---
  
# 8. Generics em TypeScript
Generics são uma das características mais poderosas em linguagens de tipagem estática como TypeScript. Eles permitem que você crie componentes que são capazes de trabalhar com qualquer tipo de dado, mantendo a segurança dos tipos. 🔄🔧
### O que são Generics?
1. **Introdução aos Generics**
    
    - Generics permitem que você defina uma função, uma classe ou uma interface que pode trabalhar com qualquer tipo de dado que você especificar mais tarde.
    
    ```TypeScript
    function identidade<T>(arg: T): T {
        return arg;
    }
    ```
    
2. **Usando Generics em Funções**
    
    - Você pode passar qualquer tipo de dado para funções que usam generics, o que as torna extremamente versáteis.
    
    ```TypeScript
    let saidaString = identidade<string>("minhaString");
    let saidaNumero = identidade<number>(100);
    ```
    
### Generics com Interfaces
- **Interfaces que Usam Generics**
    
    - Generics podem ser usados em interfaces para definir propriedades ou métodos que serão determinados quando a interface for implementada.
    
    ```TypeScript
     interface ParGenerico<K, V> {
         chave: K;
         valor: V;
     }
    
     let item: ParGenerico<number, string> = { chave: 1, valor: "Teste" };
    ```
    
### Generics em Classes
- **Classes com Generics**
    
    - Classes também podem ser definidas com generics, permitindo que você crie estruturas de dados dinâmicas que trabalham com qualquer tipo de dado.
    
    ```TypeScript
     class Caixa<T> {
         conteudo: T;
         constructor(valor: T) {
             this.conteudo = valor;
         }
     }
    
     let caixaString = new Caixa<string>("Hello World");
     let caixaNumero = new Caixa<number>(123);
    ```
    
### Generics com Restrições
- **Restringindo Generics**
    
    - Você pode restringir os tipos que um generic pode aceitar, usando a palavra-chave `extends`.
    
    ```TypeScript
     function tamanho<T extends { length: number }>(arg: T): number {
         return arg.length;
     }
    
     let tamanhoString = tamanho("Teste");  // Ok
     let tamanhoArray = tamanho([1, 2, 3, 4]);  // Ok
     // let tamanhoNumero = tamanho(10);  // Erro: 'number' não tem 'length'
    ```
    
### Exercícios para Praticar
1. **Funções Generics:**
    - Crie uma função generic `primeiroElemento` que retorna o primeiro elemento de um array de qualquer tipo.
2. **Generics com Interfaces:**
    - Defina uma interface `Pilha<T>` que suporte operações de 'push' e 'pop'. Implemente esta interface em uma classe.
3. **Classes com Generics:**
    - Implemente uma classe `Mapa<K, V>` que simule a funcionalidade de um objeto Map, permitindo adicionar e buscar pares de chave-valor.
4. **Generics com Restrições:**
    - Crie uma função que aceite somente arrays ou strings como argumento, fazendo uso de generics com restrições.
5. **Generics Complexos:**
    - Escreva uma função `mergeObjects` que combine dois objetos e retorne um novo objeto que combine as propriedades de ambos, usando generics.
  
Generics são essenciais para criar software robusto e reutilizável em TypeScript, oferecendo a flexibilidade para trabalhar com diversos tipos enquanto mantém as garantias de tipo. No próximo tópico, exploraremos tipos avançados e utilitários que TypeScript oferece para facilitar ainda mais a manipulação de dados.
  
---
  
# 9. Tipos Avançados e Utilitários em TypeScript
TypeScript oferece uma variedade de tipos avançados e utilitários que ajudam a lidar com situações mais complexas de tipagem, permitindo uma maior flexibilidade e reusabilidade do código.
### Tipos Union e Intersection
1. **Union Types**
    
    - Union types permitem que uma variável aceite mais de um tipo de dado.
    
    ```TypeScript
    type NumeroOuString = number | string;
    function exibirId(id: NumeroOuString) {
        console.log(`ID: ${id}`);
    }
    exibirId(101);  // Válido
    exibirId("202");  // Válido
    ```
    
2. **Intersection Types**
    
    - Intersection types combinam múltiplos tipos em um só, juntando suas propriedades.
    
    ```TypeScript
    interface Negocio {
        nome: string;
        fundacao: Date;
    }
    
    interface Empregados {
        quantidade: number;
    }
    
    type Empresa = Negocio & Empregados;
    let minhaEmpresa: Empresa = { nome: "TechCorp", fundacao: new Date(), quantidade: 100 };
    ```
    
### Tipos Condicionais
- **Conditional Types**
    
    - Tipos condicionais permitem a criação de tipos que dependem de condições.
    
    ```TypeScript
     type PequenoOuGrande<T> = T extends "pequeno" ? number : string;
     let tamanhoPequeno: PequenoOuGrande<"pequeno"> = 10;  // number
     let tamanhoGrande: PequenoOuGrande<"grande"> = "muito grande";  // string
    ```
    
### Utilitários Comuns
TypeScript fornece várias funções utilitárias que ajudam a manipular tipos de maneiras úteis.
1. **Partial**
    
    - Torna todas as propriedades de um tipo opcional.
    
    ```TypeScript
    interface Carro {
        marca: string;
        modelo: string;
        ano: number;
    }
    
    function configurarCarro(config: Partial<Carro>) {
        return config;
    }
    configurarCarro({ modelo: "Fusca" });  // Outras propriedades são opcionais
    ```
    
2. **Readonly**
    
    - Torna todas as propriedades de um tipo somente leitura.
    
    ```TypeScript
    type CarroReadonly = Readonly<Carro>;
    let meuCarro: CarroReadonly = { marca: "VW", modelo: "Gol", ano: 2020 };
    // meuCarro.modelo = "Fusca";  // Erro: não pode modificar uma propriedade readonly
    ```
    
3. **Record**
    
    - Cria um objeto tipo com um conjunto de propriedades do mesmo tipo.
    
    ```TypeScript
    let cidades: Record<string, string> = {
        Tokyo: "Japão",
        Paris: "França",
        NovaYork: "EUA"
    };
    ```
    
  
### Exercícios para Praticar
1. **Trabalhando com Union e Intersection:**
    - Crie uma função que aceite um parâmetro que pode ser um `string` ou um `number`, e outro parâmetro que é uma interseção de dois tipos com diferentes propriedades.
2. **Explorando Conditional Types:**
    - Defina um tipo condicional que mude com base em um valor booleano passado, alternando entre dois tipos definidos.
3. **Aplicando Partial e Readonly:**
    - Use `Partial` para criar uma função que aceite configurações parciais de um objeto. Use `Readonly` para garantir que nenhum objeto passado para uma função específica possa ser modificado.
4. **Utilizando Record:**
    - Implemente uma função que use `Record` para mapear nomes de países para suas capitais e permita busca por qualquer país fornecido.
5. **Generics com Utilitários:**
    - Crie uma função generic que aceite um tipo e retorne um array de `Partial` desse tipo, permitindo a criação de listas com configurações parciais.
---