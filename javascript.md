## O que é javascript

JavaScript (JS) é uma lingua de fácil implementação, interpretada (sem compilação, as instruções são executadas diretamente) e orientada à objetos com funções de primeira-classe (podemos utilizar funções como valores) e é mais conhecida por ser a linguagem dos scripts de páginas Web. Ela pode ser usada em vários ambientes fora da web também.

### História 

- Foi criada por Brendan Eich.
- Foi criada para complementar Java.
- Originalmente era chamada de "LiveScript", mas para se projetar no sucesso de Java, foi feita uma troca de nome estratégica para JavaScript. Obs: Java e JavaScript não são relacionadas.
- O conceito principal do design era ser "fácil" de escrever.

## Sintaxe

### Variáveis

#### Declaração:

```js
var variavel = 42;
// var = variável
// variavel = nome da variavel
// 42 - valor dentro da variavel

var variavel2 = "Hello world";
var variavel3 = true;

// podemos também inicializar a variavel antes e usar depois:
var variavel4;
variavel4 = false;

// assim como podemos trocar o tipo que a variável carrega livremente:
variavel = true; // variavel era um tipo Number quando foi declarada
```

Como pôde ver acima, não precisamos declarar o tipo da variável. Simplesmente utilizamos a palavra chave **var** para indicar que é uma variável.

#### Tipos primitivos

- Number
```
O tipo Number é o tipo que usamos para conter números e estes números são valores de dupla-precisão com até 64-bits (como double no c#). No js não existe números inteiros, todos tem casas decimais (mesmo que seja .00).
```
```js
var valor = 10;
```

- String
```
O tipo String são sequencias de caracteres do Unicode (16-bit).
```
```js
var valor = "Hello World";
```

- Boolean
```
O tipo Boolean é representado pelos valores booleanos, true e false.
```
```js
var valor = true;
```

- Undefined
```
Quando declaramos uma variável, mas não atribuímos um valor a ela, o valor desta variável será Undefined.
```
```js
var valor; // o valor contido nesta variável é "undefined"

valor = 40; // após inicializada, a variável passa a ter outro valor (qualquer que definimos)
```

- null
```
Tipo que representa um valor nulo.
```
```js
var a = null;
```

==Nota: diferença entre null e undefined - variáveis só recebem o valor undefined se são declaradas, mas não definidas, enquanto que o valor null é algo que colocamos com código. Logo, se uma variável está com o valor 'undefined' podemos entender que esquecemos de atribuir um valor a ela, enquanto que com o valor 'null' entendemos que colocamos explicitamente que é um valor nulo (ou não valor). ==

#### Operador typeof

Usado para sabermos com que tipo de variável estamos trabalhando.

```js
// Sintaxe:
typeof <valor>
typeof <variável>

// Exemplo:
var a = 10;
var b = true;
var c = "Exemplo";
var d;
var e = null;
console.log(typeof a);
console.log(typeof b);
console.log(typeof c);
console.log(typeof d);
console.log(typeof e);
```
Saída:
```
number
boolean
string
undefined
object
```

### Operador == e ===

##### ==
O operador == é usado para comparar dois valores (os variáveis), como nas outras linguas. Mas, também podemos comparar tipos diferentes e a conversão de um tipo para o outro é feita automaticamente pela lingua (se for possível de ser feita).

```js
// Caso number e number
var a = 10;
var b = 10;

if(a == b)
{
	console.log("São iguais");
}
else
{
	console.log("Não são iguais");
}

// Caso number e string
var c = 10;
var d = "10";

if(c == d)
{
	console.log("São iguais");
}
else
{
	console.log("Não são iguais");
}
```

Saída:
```
São iguais
São iguais
```

##### ===
O operador === é usado para comparar dois valores (ou variáveis) com segurança de tipo, se ambos forem de tipos diferentes é retornado falso.

```js
// Caso number e number
var a = 10;
var b = 10;

if(a == b)
{
	console.log("São iguais");
}
else
{
	console.log("Não são iguais");
}

// Caso number e string
var c = 10;
var d = "10";

if(c == d)
{
	console.log("São iguais");
}
else
{
	console.log("Não são iguais");
}
```

Saída:
```
São iguais
Não são iguais
```

### if

Como podemos ver anteriormente podemos utilizar o if de maneira parecida das linguagens da família C. Mas o if, no javascript, também tem outros usos, uma vez que todos os tipos do javascript são associados com o tipo Boolean.

#### Number
```js
var a = 10;

if(a){
console.log("a é true");
}

var b = 0;

if(b){
console.log("b é true");
}
```

Saída:

```
a é true
```

Com o tipo number, podemos checar se seu valor é diferente de 0, o que retorna true. Caso seja 0 retorna false.

#### String

```js
var a = "Olá";

if(a){
console.log("a é true");
}

var b = "";

if(b){
console.log("b é true");
}
```

Saída:

```
a é true
```

Com o tipo string, retorna true caso tenha pelo menos 1 caractere e false se não contiver nenhum caractere.

#### Outros tipos

- Booleanos - funcionam como nas outras linguas.
- Undefined - retorna false.
- Null - retorna false.

### Objetos

- Os objetos no javascript são formatos livres, isto é, não são ligados a uma classe.
- As propriedades dos objetos podem ser acessadas diretamente (não há private)
- Propriedades novas podem ser adicionadas diretamente nos objetos
- Objetos podem ter métodos

#### Sintaxe:

```js
// Declarando um objeto in line
var meuObj = {};

console.log(typeof meuObj);
console.log(meuObj);

// Colocando um atributo no objeto
var meuObj = {};
meuObj.prop = "Olá";

console.log(meuObj);

// Colocando multiplos atributos no objeto
var meuObj = {};
meuObj.prop = "Olá";
meuObj.prop2 = 123;

console.log(meuObj);
console.log("Propriedade 1: " + meuObj.prop + " Propriedade 2: " + meuObj.prop2);
```

Saída:
```
object
object { }
object { prop: "Olá" }
object { prop: "Olá", prop2: 123 }
Propriedade 1: Olá Propriedade 2: 123
```

```js
// inicializando um objeto já com atributos
var meuObj = {
	"nome": "fulano",
	"id": "123",
	"casado": true
};
// podemos adicionar mais propriedas após a inicialização, normalmente.
console.log(meuObj);
console.log("Nome: " + meuObj.nome + " Id: " + meuObj.id + " Casado: " + meuObj.casado);
```

Saída:
```
Object { nome: "fulano", id: "123" }
Nome: fulano Id: 123 Casado: true
```

Acessando propriedades dos objetos:
```js
var meuObj = {
	"nome": "ciclano",
	"idade": 25
};

// Existem duas maneiras:

// Acessando com .
console.log("Nome: " + meuObj.nome);

// Acessando com []
console.log("Idade: " + meuObj["idade"]);

```

Saída:
```
Nome: ciclano 
Idade: 25
```

Usamos a notação [] para acessar um atributo de um objeto quando:
- O nome da propriedade é uma palavra reservada
- O nome da propriedade é inválido (começa com numero, por exemplo)
- O nome da propriedade é dinâmino 

==Nota: acessar propriedades com . é preferível, pois é otimizado pela própria lingua.==

#### Objetos aninhados
```js
var meuObj = {
	"prop1": "exemplo",
	"prop2": 3,
	"propObj": {
	"propInterna": "propriedade do objeto do meuObj"
	} 
}
// podemos misturar os usos de . e []
console.log(meuObj.propObj["propInterna"] );

```

Saída:
```
propriedade do objeto do meuObj
```

#### Deletar uma propriedade de um objeto

Usamos a palavra reservada delete:
```js
var pessoa = {
"primeiroNome": "João",
"segundoNome": "Silva",
"idade": 30
}
console.log(pessoa);
delete pessoa.idade;
console.log(pessoa);
```

Saída:
```
Object { primeiroNome: "João", segundoNome: "Silva", idade: 30 }
Object { primeiroNome: "João", segundoNome: "Silva" }
```

#### Wrapper Objects

Quando utilizamos certas funções em tipos primitivos (como .length em strings), é criado um objeto temporário com o valor do tipo primitivo que conta com a função que usamos. Então, nestas funções o que nos é retornado são propriedades do Wrapper Object (ou objeto temporário), não do tipo primitivo em si.

####  Palavra chave this

```js
var pessoa = {
"nome": "João",
"sobrenome": "Silva",
"getNomeCompleto": function(){
	return this.nome + " " + this.sobrenome;
	}
};

var nomeCompleto = pessoa.getNomeCompleto();
console.log(nomeCompleto);

// objeto dentro de objeto
var pessoa = {
"nome": "João",
"sobrenome": "Silva",
"getNomeCompleto": function(){
	return this.nome + " " + this.sobrenome;
	},
	"endereco": { "rua" : "avenida 1",
	"numero" : "123",
	"estado" : "SP",
	"getEndereco": function(){
		return this.rua + "- " + this.numero + " -" + this.estado;
	},
	"isFromEstado" : function(est){
	return (est === this.estado);
	}
	}
};

console.log(pessoa.endereco.isFromEstado("SP"));
console.log(pessoa.endereco.isFromEstado("RJ"));
```

Saída:
```
João Silva
avenida 1- 123 -SP
true
false
```


### Arrays

Em js arrays são ==objetos== e cada item que adicionamos é uma propriedade enumerada (começa de 0). Além das propriedades que adicionarmos, a array tem uma propriedade padrão chamada *length*, que nos retorna o tamanho da array (quantidade de elementos presentes nela).

Sintaxe:
```js
// declaração e definição
var array = [100, 200, 300];

// acessando
array[0]; // 100
array[1]; // 200
array[2]; // 300

// podemos acessar os elementos utilizando aspas também, mas não conseguimos acessar
// com a notação de ponto (.), uma vez que propriedades com números no começo não podem
// ser acessadas assim, então utilizamos a notação de chaves ([]).
array["0"]; // 100

// alocar novos valores
array[3] = 400;
array.push(500); // adiciona os elementos passados como argumentos no final da array
array.unshift(100); // adiciona os elementos passados como argumentos no começo da array


// deletar valor
array.pop(); // remove o último elemento da array e retorna o valor
array.shift(); // remove o primeiro elemento da array e retorna o valor


// descobrir o numero de elementos na array
array.length;

// loop foreach na array
array.forEach(function(){
console.log("Para cada elemento");
});
// vai imprimir "Para cada elemento" 3x (tamanho da array)

// loop foreach usando os elementos da array
array.forEach(function(item){
console.log("Elemento:" + item);
});
// vai imprimir "Elemento: 100", "Elemento: 200" e "Elemento: 300"
```



### Funções

- Funções são valores, logo ==podemos associar uma função com uma variável (parecido com delegate do c#)==
- Funções não têm sobrecarga
- Funções podem ser passadas como argumentos para outras funções
- Funções aceitam argumentos a mais ou a menos da assinatura da função
- Funções podem usar 2 argumentos padrões (*this* e *arguments*)

```js
// declarando funções:

// sem parâmetro
function dizerOla(){
	console.log('Olá');
}
dizerOla();

// com parâmetros
function dizerNome(nome){
console.log('Olá, ' + nome);
}

dizerNome('Fulano');

// o que acontece se charmarmos a mesma função de cima sem passar os argumentos?
dizerNome();

// expressão function:
var f = function saudacao(){
console.log('Olá!');
};

f();
```

Saída:
```
Olá
Olá, Fulano
Olá, undefined
Olá!
```

==Diferente das línguas compiladas, em que nem conseguiríamos compilar nosso programa se não passassemos os argumentos corretamentes para suas respectivas funções, no js podemos passar ou não argumentos pra uma função que tem parâmetros. Se não passarmos argumentos, acontece que todas as variáveis que a função receberia (se passados) são undefined. Da mesma maneira também podemos chamar uma função passando argumentos mesmo se ela nem precise dos argumentos, isto é, mesmo se ela não for utilizá-los (desta maneira, os argumentos a mais só são ignorados)==. 

#### Retornando Valores

```js
function soma(a, b){
return a + b;
}

soma(1, 4);

// um retorno vazio resulta em undefined
function vazia(){
return;
}
console.log(vazia());

// mesmo não utilizando um return em uma função, o retorno padrão será undefined
function vazia2(){

}
console.log(vazia2());
```

Saída:
```
5
undefined
undefined
```

==Obs: mesmo que a terceira função tivesse uma lógica ali dentro, só pelo fato de não contar com um return, o return será undefined.==

#### Expressões function anônimas
```js
// expressão function normal:
var f = function saudacao(){
console.log('Olá!');
};

f();

// expressão function anônima
var funcao = function(){
console.log("Olá");
}

funcao();
```

Saída:
```
Olá!
Olá!
```

==Uma vez que a função já está atrelada a uma variável que está nomeada, não precisamos nomear a função também. Mas detalhe: se atrelarmos outro valor sobrescrevendo a função na variável, a primeira função é perdida. E, além disso, se o tipo que o substitui não for uma função, se tentarmos invocar a variável um erro será gerado==.

#### Passando funções para funções
```js
var f = function (){
console.log('Olá!');
};

var execucao = function (func) {
// imprimindo a função em si
console.log(func);
// executando a função recebida
func();
}

execucao(f);
```

Saída:
```
function f()
Olá!
```

#### Funções dentro de Objetos

Em outras linguagens orientadas à objetos temos métodos e atributos. No js, objetos podem conter funções como atributos (simulando o mesmo efeito). 

```js
var meuObj = {
	"prop1": true
};

meuObj.metodoObj = function(){
console.log('Método dentro do objeto');
};

meuObj.metodoObj();
```

Saída:
```
Método dentro do objeto
```


#### Palavra chave arguments

Captura todos os argumentos passados na função em um objeto com os campos numerados (parecido com uma array).

```js
var add = function (a , b){
console.log(arguments);
return a + b;
};

console.log(add(10,20,30,40,50,60));

// usando os arguments para fazer uma função de adição que aceita mais argumentos
var add = function(){
	var i, sum = 0;
	for(i=0; i<arguments.length; i++){
		sum += arguments[i];
	}
	return sum;
};
console.log(add(10,20,30,40,50,60));
```

Saída:
```
Arguments { 0: 10, 1: 20, 2: 30, 3: 40, 4: 50, 5: 60, … }
30
210
```