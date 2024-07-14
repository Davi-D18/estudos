![[Pasted image 20240708085200.png]]
![[Pasted image 20240708085359.png]]
![[Pasted image 20240708085551.png]]
![[Pasted image 20240708090024.png]]
# Criando Classes
Uma estrutura básica de uma classe
```ts
class Pessoas {
	// abaixo são os atributos dessa classe
	nome: string;
	idade: number;
	altura: number;

	// constructor vai construir usando os atributos acima
	constructor (nome: string, idade: number, altura: number){
		this.nome = nome;
		this.idade = idade;
		this.altura = altura;
	}

	// abaixo são métodos, que pode ser considerado ações
	dormir() {
		
	}
}

// Para criar um novo objeto a partir da classe, faça isso
const caio = new Pessoa('Davi', 19, 1.70)
// new vai criar um novo objeto a partir da classe Pessoa e vai chamar o constructor dela
```

Também é possível usar #interface, semânticamente falanado fica melhor e mais organizado porque evita você esqueçer algum atributo ao colocar na classe
interface seria tipo um "contrato" onde ao relaciona-la a uma classe, ela pegará os atributos da interface e ajuda a evitar esqueçer algo
```ts
interface Ipessoa {
	nome: string;
	idade: number;
	altura: number;
	peso: number;
}

class Pessoas implements Ipessoa {
	// abaixo são os atributos dessa classe
	nome: string;
	idade: number;
	altura: number;
	peso: number;
	// com o implements Ipessoa, eu preciso colocar o atributo peso

	// constructor vai construir usando os atributos acima
	constructor (nome: string, idade: number, altura: number, peso: number){
		this.nome = nome;
		this.idade = idade;
		this.altura = altura;
		this.peso = peso;
	}

	// abaixo são métodos, que pode ser considerado ações
	dormir() {
		
	}
}
```

# Encapsulamento
![[Pasted image 20240708094239.png]]
- `private`: deixa um atributo privado e não poderá visualizar nem alterar
- `readonly`: deixa o atributo privado porém consegue visualizar
- `acessors(get)`: permite acessar um atributo mesmo sendo privadop, criando um método

```ts
interface Ipessoa {
	nome: string;
	idade: number;
	altura: number;
}

class Pessoas implements Ipessoa {
	// abaixo são os atributos dessa classe
	nome: string;
	idade: number;
	altura: number;
	private _cpf: string;
	// com o implements Ipessoa, eu preciso colocar o atributo peso

	// constructor vai construir usando os atributos acima
	constructor (nome: string, idade: number, altura: number, cpf: string){
		this.nome = nome;
		this.idade = idade;
		this.altura = altura;
		this.cpf = cpf
	}

	// abaixo são métodos, que pode ser considerado ações
	dormir() {
		
	}

	// acessor: get
	get cpf(): string {
		return this._cpf
	}

	// acessor: setter
	set cpf(newCpf: string) {
		if (newCpf ! == 14 ) {
			// lançando um erro com throw new
			throw new Error("CPF length is incorrect")		
		}
		this._cpf = newCpf;
	}
}
```

# Herança (extends)
![[Pasted image 20240708100926.png]]

```ts
class Professor extends Pessoa {
	codigo: string

	constructor(nome: string, idade: number, altura: number, codigo: string) {
		super(nome, idade, altura)
		// herdará o construtor da classe pessoa (pai) evitando repetir código
		// entre parênteses, coloque os atributos que queira herdar
		this.codigo = codigo
	}
	
}
```


# Polimorfismo
![[Pasted image 20240708102555.png]]
### Verificando a instancia 
```ts
console.log(Professor instanceof Pessoa)
// a classe professor é uma instancia da classe pessoa(mãe)? retorna true
```

