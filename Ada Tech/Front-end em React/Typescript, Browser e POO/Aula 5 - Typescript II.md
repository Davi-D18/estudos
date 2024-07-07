No typescript, ao atribuir um valor para uma variável do tipo const, o tipo da variável vai ser o mesmo do valor
```ts
const numero = 3.14 // ou seja, o tipo dela será o próprio valor
```

Outro exemplo:
```ts
const nomeDoUsuario = prompt('Qual seu nome? ');
console.log(nomeDoUsuario.toUpperCase());
// caso o usuário aperte em cancelar lá no browser, o resultado disso será null
// e o ts vai emitir um erro
console.log(nomeDoUsuario?.toUpperCase());
//porém fazendo dessa forma, ele vai colocar o nome em Caixa alta apenas quando a variável não for null ou undefined 
```

## Tipando Arrays
### 1° Método
Basicamente a mesma coisa que fazemos para tipar uma variável também serve para um array
```ts
const numeros: number[] = [1, 2, 3, 4, 5]
// Uma forma de tipar um array
```

### 2° Método
Caso tenha mais de um tipo de dado no array, poderá fazer assim
```ts
const numeros2: (number | string)[] = ['Davi', 19, 1.72]
// também é possível definir mais de um tipo para um array utilizando essa sintaxe acima
```


> [Importante] Tipar Array
> Evite colocar mais de um tipo de dado em uma variável, não é recomendado

### Tuplas
Em vez de usar o método anterior para tipar que não é indicado,  poderá fazer de outra forma utilizando uma tupla, basicamente, quando você sabe quantos elementos vai ter no array e quais tipos de dados, você pode usar essa sintaxe
```ts
const pessoas: [string, number] = ['Davi', 19];
```
É mais indicado essa sintaxe para tipar um array

### Modelos de Objetos
Ao criar um object, você pode criar um "modelo" para os objetos seguirem aquele modelo, existem 2 tipos:
- `Interface`:
- `Type`: 

#### Interface
Em um objeto se você quiser que ele siga um certo padrão de valores, poderá usar o `interface`. Aqui você cria um modelo para os objetos seguir, exemplo: 
```ts
interface Person {
	nome: string;
	idade: number;
	profissao?: string;
	altura: number;
}

const pessoas: Person = {
	nome: "Davi",
	idade: 19,
	profissao: "estudante",
	altura: 1.70
}
```
Caso algum atributo tenha `?` indica que ele é opcional, isso significa que se esse "modelo" não tiver e você atribuir a um objeto, terá que colocar todas as propriedades e dará erro se não colocar

#### Type
A estrutura do type é a mesma do interface porém com o sinal de `=` 
```ts
type Person = {
	nome: string;
	idade: number;
	profissao?: string;
	altura: number;
}

const pessoas: Person = {
	nome: "Davi",
	idade: 19,
	profissao: "estudante",
	altura: 1.70
}

```

##### Diferenças do Interface X Type
`Interface` está mais associado a orientação de objetos semanticamente falando, é mais indicado para essa situação você definir uma interface para uma classe
`Type` é mais genérico, pode ser qualquer coisa, desde uma `string` até um `boolean` 

### Union Types
É possível passar um parâmetro em uma função sendo opcional usando o `?` 
```ts
function numeroAleatorio (num1: number, num2: number, criterio?: "lower" | "greter") {
	switch (criterio) {
		case "greater":
			return num1 > num2 ? num1 : num2;
		case "lower":
			return num1 < num2 ? num1 : num2;
		default:
			const numeroGeradoAleatorio = Math.random();
			if (numeroGeradoAleatorio >= 0.5) {
				return num1
			} else {
				return num2
			}
	}
}

const numeroEscolhido = numeroAleatorio(10, 20, 'lower');
console.log(numeroEscolhido)
```

o Type pode ser usado para dar "apelidos" seria um type aliase
```ts
type Criterio = "greater" | "lower" 

function numeroAleatorio (num1: number, num2: number, criterio?: Criterio) {
	//comandos
}
```

#### Tipando Funções
obs: Evite usar parâmetros opcionais no inicio, use mais no final
```ts
function numeroAleatorio (num1: number, num2: number, criterio?: Criterio): number {
	//comandos
}
```

### Utility Types
Eles servem para criar novos [[#Type]] a partir dos que já existem, alguns exemplos:
- `Partial`
- `Required`
- `Pick`
- `Omit`
- `Exclude`
- `Record`

#### Partial
Depois de ter criado uma [[#Interface]] você pode usar uma palavra reservada `partial` para definir que todos os atributos dentro da daquele "modelo" de objeto serão opcionais 
```ts
type PartialPerson = Partial<person>;

const outraPessoa: PartialPerson = {
	//atributos
}
```

#### Required
Os atributos que eram opcionais passam a ser obrigatórios usando o required
```ts
type PersonRequired = Required<person>;

const outraPessoa: PersonRequired = {
	//atributos
}
```

#### Pick
Ele irá pegar alguns atributos de uma [[#Interface]] já existente e poderá usar esse type apenas com os atributos que escolher
```ts
type PersonPicked = Pick<person, "nome", "idade">;

const outraPessoa: PersonPicked = {
	// atributos
	// aqui irá mostrar os atributos que escolheu em PersonPicked
}
```

#### Omit
Vai omitir uma propriedade de uma interface, em outras palavras, remover 
```ts
type PersonOmit = Omit<person, "profissao">;

const outraPessoa: PersonOmit = {
	//atributos
}

```

#### Exclude
Vai remover algum elemento de uma união
```ts
type Criterio = "greater" | "lower" 

type CriterioExclude = Exclude<Criterio, "lower">
```

#### Record
Vai criar um objeto e então atribuir a #interface  person, quando criar um objeto e relaciona-lo a `Pessoas` ele criará uma chave com qualquer string e o o objeto que está dentro da `person` vai ser o valor daquela chave
```ts
type Pessoas = Record<string, person>

const pessoas: Pessoas {
	'qualquer_coisa': {
		nome: "fulano"
		idade: 25
		altura: 1.65
	}
}
