Utilizando crases ( `` ) você tem um "poder" a mais, podendo injetar código Javascript dentro de um texto
[[Aula 6 - Funções de Alta Ordem]]

Caso uma função tenha dois parâmetros e na hora da chamada da função envie só um parâmetro, pode definir na função um valor padrão 

```jsx
function saudacao (nomeDoEstudante, curso = "Front-end em react") {
	//comandos
}
// Observe que o parâmetro 'curso' está com um valor padrão caso onao seja
// repassado nada a váriavel
```

## Funções anônimas

Uma função anôima pode ser atribuida a uma váriavel e ser utilizada normalmente posteriormente, porém no Javascript, esse tipo de função é diferente da tradicional

### Arrow Functions - Funções de Seta

Uma estrutura de uma Arrow Function

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fecdf77a-529a-47e3-ba2b-97f20ca94fa6/3fb5fd81-fcb7-469c-878e-fe56b27d52d7/Untitled.png)

```jsx
const subtrair = (A, B) => {
	return A - B;
}
// => Significa algo do tipo 'Receba essa informação (Parâmetros) 
// Processe essas informações e entrega o que está dentro das chaves
```

Uma Arrow Function pode omitir o `return` sendo assim, já faz isso por padrão sem precisar adicionar `return`

Também é permitido omitir os `( )` nos parâmetros

## Objetos - Objects

<aside> 📌 **Chave** = Chave é um identificador que contém um valor dentro dela | **Valor** = Valor é o contéudo dentro dessa chave que vai ser exibido ao ser chamado

</aside>

Estrtura Básica de um Objeto

```jsx
const pessoa = {
nome: "Davi",
idade: "19",
aluno: true,
};

console.log(pessoa); // imprimi o object todo
// object pode ser bom para adicionar várias informações sobre uma pessoa
// 'nome' é a chave
// "Davi" é o valor
// a gente pode pensar em objetos como várias váriaveis, onde cada nome vai 
// conter uma informação que pode ser acessada 
```

No object pode ser adicionadas arrays dentro do object

Para imprimir uma posição específica do object, pode fazer assim:

```jsx
// Baseado no código anterior
console.log(pessoa.nome); // aqui irá imprimir o nome 
```

Também pode acessar os valores fazendo `console.log(pessoa[“nome”])` talvez seja bom usar essa outra forma caso a **chave seja** grande ou contenha espaços

É possível também reatribuir chaves novamente, ou seja atribuir outro valor naquela chave existente, o procedimento é o mesmo de passar um novo valor a uma váriavel

- Adicionar propriedades dentro do object
    Para adicionar uma nova propriedade dentro do object, basta fazer isso:
    
    ```jsx
    // Considerando o object anterior
    pessoa.profissao = "Desenvolvedor"
    console.log(pessoa)
    // na primeira linha foi chamado o object e depois do ponto foi criado
    // uma nova chave e depois atribuído um valor dentro dessa chave
    // depois que imprimir op object, a chave "profissao" aparecerá lá
    ```
    
- Deletando atributos
    
    Para deletar um atributo, basta usar o `delete nome_do_obejeto.atributo;` exemplo:
    
    ```jsx
    // Baseado no object existente
    delete pessoa.profissao;
    ```
    

No js pode adicionar funções dentro de um object, porém a forma mais indicada é usar uma Arrow Function, exemplo:

```jsx
const pessoa = {
nome: "Davi",
idade: "19",
aluno: true,
funcao: () => {
	//sessão de comandos
};
```

- Também é possível adicionar váriaveis existentes dentro de um object
 - É possível também criar uma váriavel com o mesmo nome de uma chave e armazenar nessa váriavel

```jsx
const { nome, hobbies } = pessoa; // as váriaveis nome e hobbies vão receber os conteúdos das chaves que // estão nesse object com o mesmo nome
```

