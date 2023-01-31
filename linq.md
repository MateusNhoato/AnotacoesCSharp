# LINQ

## Tabela de Conteúdo
- [Introdução](#introdução)
    - [Interfaces](#interfaces-da-linq)
    - [Vantages](#vantages-da-linq)
    - [Desvantagens](#desvantagens-da-linq)
- [Consulta](#consulta)
- [Sintaxe de Consultas](#sintaxe-de-consultas-linq)
    - [Query Syntax](#query-syntax)
    - [Method Syntax](#method-syntax)
    - [Tipos de Consulta](#tipos-de-consulta)
- [Filtrar Dados](#filtrar-dados)


## Introdução
`Language-Integrated Query(LINQ)` é um poderoso conjunto de tecnologias baseado na integração de recursos de consulta na linguagem C#.

A LINQ fornece uma experiência de consulta consistente para consultar objetos, bancos de dados relacionais, xml, entidades e outras fontes de dados. Além disso, possui uma sintaxe de consulta estruturada usando C#.

![Linq](img\linq1.png)


As consultas LINQ retornam resultados como objetos.
![Linq](img\linq2.png)
 Logo, permite usar uma abordagem orientada a objetos no conjunto de resultados sem se preocupar em transformar diferentes formatos de resultados em objetos.

 
 ## Interfaces da LINQ
As consultas LINQ usam métodos de extensão para classes que implementam as interfaces **IEnumerable** ou **IQueryable**.

**Enumerable** e **Queryable** são duas classes estáticas que contêm métodos de extensão para escrever consultas LINQ.

Isso significa que podemos chamar os métodos LINQ em qualquer objeto que implemente **IEnumerable&lt;T>** e **IQueryable&lt;T>** . Podemos criar classes que implementam essas interfaces, que vão 'herdar' todas as funcionalidades da LINQ.

### IEnumerable&lt;T>
É uma interface que garante que uma determinada classe seja *iterável*.
Uma classe que implementa IEnumerable&lt;T> pode ser pensada e usada como uma sequência de elementos.

**Os métodos da link que retornam sequências são todas sequências do tipo `IEnumerable<T>`**. Para transformar estas sequências em listas ou arrays, a LINQ fornece dois métodos de conversão:
1. **ToList()** - converte um IEnumerable&lt;T> para um List&lt;T>
2. **ToArray()** - converte um IEnumerable&lt;T> para um Array&lt;T>

## Vantages da LINQ
- Fornece uam sintaxe de consulta comum para consultar diferentes fontes de dados.
- Utiliza menos código em comparação com a abordagem tradicional de consulta.
- Fornece verificação de erros em tempo de compilação, bem como suporte de inteligência no Visual Studio, evitando erros em tempo de execução.
- Fornece muitos métodos embutiods que podemos usar para realizar diferentes operações, como filtragem, ordenação, agrupamento, etc.
- Permite a reutilização de consultas.

## Desvantagens da LINQ
- Consultas muito complexas são difícieis de escrever
- Não aproveita ao máximo os recursos da SQL, como o plano de execução em cache para o procedimento armazenado.
- Consultas mal escritas tendem a ter um desempenho pior.
- Alterações nas consultas exigem recompilar a aplicação e refazer o deploy.

<hr/>

## Consulta
Os métodos LINQ que retornam IEnumerable&lt;T> têm um conceito de **execução lenta** (também chada de adiada ou lazy execution).

Todos osmétodos genéricos LINQ podem **inferir implicitamente argumentos de tipo**, portanto não precisamos especificá-los na maioria dos casos (usamos *var*).

A maioria dos métodos LINQ aceita delegates Func<> e Predicate<>. A opção mais comum para fornecer um delegate é escrever uma **expressão lambda**.

Ao trabalhar com a interface IQueryable&lt;T>, a consulta é compilada (em SQL, por exemplo) e executada remotamente.


## Sintaxe de consultas LINQ
Existem dois tipos, **Query Syntax** e **Method Syntax**.

### **Query Syntax** 
Também conhecida como Query Expression Syntax (Sintaxe de Consulta).

É um tipo de consulta usada em bancos de dados SQL.
```sql
FROM objeto in FonteDeDados
Where condicao
Select objeto
```
1. Inicialização: iniciamos com alguma fonte de dados para consultar usando a palavra chave, ou cláusula, `FROM`.
2. Condição: Usamos operadores de consulta para adicionar **condições** para a consulta, começando com a palavra chave `Where`.
3. Seleção: Agrupamos ou selecionamos os objetos que queremos, usando a palavra chave `Select`, ou podemos usar `GroupBy`.

*Obs*: No final podemos utilizar a palavra **var** para tratar o resultado, mas o tipo de objeto que a consulta gerará será do tipo *IEnumerable* ou *IQueryable*.

Exemplo:
```cs
IList<string> frutas = new List<string>()
{
    "Banana", "Maça", "Uva", "Melão", "Laranja", "Pera"
};

var resultado = from f in frutas      // inicializando com a cláusula from
                where f.Contains('r') // usando operador para filtrar
                select f;            // terminando com cláusula select ou GroupBy

Console.WriteLine(string.Join(", ", resultado));
```
Saída no console:
```
Pera, Laranja
```


### **Method Syntax**
Também conhecida como Method Extension Syntax ou Fluent Syntax (Sintaxe de Método).

- Usa métodos de extensão incluídos nas classes estáticas **Enumerable** ou **Queryable**.
- Nem todos os métodos LINq podem ser utilizados com sintaxe de consulta, um dos motivos da sintaxe de método levar vantagem. Além disso, a sintaxe de método é estilisticamente semelhante ao código C#.
- A maior diferença na hora de se escrever uma consulta com a Sintaxe de Método, é que utilizamos um *delegate Predicate* que receba o mesmo tipo de objeto que a consulta e retorne um **bool**. Geralmente esse delegate é feito com expressões **lambdas**, e serve para filtrar, agrupar, ordenar, ou fazer outras coisas com a fonte de dados que estamos trabalhando.

Exemplo:
```cs
IList<string> frutas = new List<string>()
{
    "Banana", "Maça", "Uva", "Melão", "Laranja", "Pera"
};

var resultado = frutas.Where(f => f.Contains('r'));
// o método Where seria o método de extensão
// enquanto a expressão lambda dentro deste método
// seria a condição da consulta

Console.WriteLine(string.Join(", ", resultado));
```
Saída no console:
```
Pera, Laranja
```

*Obs*: O compilador converte a sintaxe de consulta em sintaxe de método em tempo de compilação.

### `Tipos de consulta`
![Linq](img\linq3.png)

## Expressão lambda
Uma **expressão lambda** é um *método anônimo* que podemos usar para criar *delegates* ou tipos de **árvore de expressão**.

Usando **expressões lambda**, podemos gravar *métodos locais*, que podem ser passados como argumentos ou serem retornados como o valor de chamadas de método.

### Sintaxe
Uma Expressão lambda tem um lado <font color="green">esquerdo</font> e um lado <font color="blue">direito</font>, seperados pelo *operador lambda* <font color="darkred">=></font> (significa "vá para").

Exemplo:

<font color="green">x</font> <font color="darkred">=></font> <font color="blue">x * x</font>

- <font color="green">Parâmetro de entrada</font>
- <font color="darkred">Operador lambda</font>
- <font color="blue">Tratamento da expressão, ou blocos de instruções. Gera o resultado esperado (no caso x * x).</font>

### Surgimento das Expressões Lambdas
Vamos utilizar de um exemplo para ilustrar o porquê do surgimento das expressões lambdas.
```cs
// lista de nomes
List<string> nomes = new();
nomes.Add("Maria");
nomes.Add("José");
nomes.Add("Sabrina");
nomes.Add("Ricardo");
nomes.Add("Pedro");

// função para consulta
static bool VerificaNomeNaLista(string nome)
{
    return nome.Equals("Pedro");
}


// consulta na lista passando como parâmetro uma função
string? resultado = nomes.Find(VerificaNomeNaLista("Pedro"));

// imprindo o resultado
Console.WriteLine(resultado);
```
Saída no Console:
```
Pedro
```

No exemplo acima estamos passando um ***delegate predicate*** para a consulta. Isto é um predicato que aceita uma string (mesmo tipo de objeto que a lista) e retorna um bool. Mas perceba como essa função é "hard coded", pois dentro dela só estamos checkando para um nome específico que digitamos (Pedro, no caso).

A evolução desse método foi começar a passar delegates anônimos para fazer a consulta, mas ainda não era a melhor alternativa. As expressões lambdas foram introduzidas para *simplificar* ainda mais o código, pois ela permite passar uma expressão embutida como um delegate com uma sintaxe enxuta.
```cs
...
//fazendo consulta com delegate anônimo
string? resultado1 = nomes.Find(delegate (string nome){
    return nome.Equals("José");
});

// fazendo a consulta com uma expressão lambda
string? resultado2 = nomes.Find(nome => nome.Equals("Pedro");
);

// imprindo o resultado
Console.WriteLine(resultado1);
Console.WriteLine(resultado2);
```
Saída no Console:
```
José
Pedro
```

## Filtrar Dados
Operadores de filtragem são usados para filtrar dados de uma **lista/coleção** com base nas condições do filtro. Usamos uma expressão booleana e somente os objetos que atenderem os requisitos dessa expressão são retornados.

- `Where` - usado para selecionar valores da coleção com base em *funções de predicado*
    ```
    fonteDados.Where(<expressão_lambda>);
    ```

Exemplo:
```cs
List<int> numeros = new List<int>();
numeros.Add(1);
numeros.Add(2);
numeros.Add(4);
numeros.Add(8);
numeros.Add(16);
numeros.Add(32);
numeros.Add(64);

List<int> numeros2 = new List<int>();
numeros2.Add(8);
numeros2.Add(16);
numeros2.Add(64);

// selecionando os números menores que 10
var resultado1 = numeros.Where(n => n < 10);

//  selecionando os números maiores que 1, menores que 20, e excluímos o 4
var resultado1 = numeros.Where(n => n > 1 && n != 4 && n < 20);

// selecionando todos os números da lista numeros menos os que também estão presentes na lista numeros2
var resultado3 = numeros.Where(n => !numeros2.Contains(n));

// mesmo resultado que o segundo exemplo, mas com o uso de 3 .Where seguidos
var resultado4 = numeros.Where(n => n > 1)
                        .Where(n=> n != 4)
                        .Where(n => n < 20);

Console.WriteLine(string.Join(" "), resultado1);
Console.WriteLine(string.Join(" "), resultado2);
Console.WriteLine(string.Join(" "), resultado3);
Console.WriteLine(string.Join(" "), resultado4);
```
Saída no Console:
```
1 2 4 8
2 8 16
1 2 4 32
2 8 16
```

Apesar de escrevermos as consultas de maneiras diferentes nos exemplos 2 e 4, não há diferença na velocidade e nem na performance dessas consultas, o compilador vai otimizar a consulta em ambos os casos.