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
- [Operadores](#operadores)
    - [Filtrar Dados](#filtrar-dados)
    - [Projeção](#projeção)
- [Créditos](#creditos)

---

## Introdução

`Language-Integrated Query(LINQ)` é um poderoso conjunto de tecnologias baseado na integração de recursos de consulta na linguagem C#.

A LINQ fornece uma experiência de consulta consistente para consultar objetos, bancos de dados relacionais, xml, entidades e outras fontes de dados. Além disso, possui uma sintaxe de consulta estruturada usando C#.

![Linq](img/linq1.png)
As consultas LINQ retornam resultados como objetos.

![Linq](img/linq2.png)
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

---

## Consulta

Os métodos LINQ que retornam IEnumerable&lt;T> têm um conceito de **execução lenta** (também chamada de adiada ou lazy execution).

Todos os métodos genéricos LINQ podem **inferir implicitamente argumentos de tipo**, portanto não precisamos especificá-los  (na maioria dos casos usamos *var*).

A maioria dos métodos LINQ aceita delegates Func<> e Predicate<>. A opção mais comum para fornecer um delegate é escrever uma **expressão lambda**.

Ao trabalhar com a interface IQueryable&lt;T>, a consulta é compilada (em SQL, por exemplo) e executada remotamente.

### Execução Imediata na LINQ

O padrão da LINQ é somente fazer a consulta quando é necessário, para forçar a consulta LINQ a ser executada e a retornar o resultado imediatamente, é necessário usar os operadores de conversão:

- ToList()
- ToArray()
- AsEnumerable
- AsQueryable
- ToDicitionary()
- ToLookup


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
1. Inicialização: iniciamos com alguma fonte de dados para consultar usando a palavra-chave, ou cláusula, `FROM`.
2. Condição: Usamos operadores de consulta para adicionar **condições** para a consulta, começando com a palavra-chave `Where`.
3. Seleção: Agrupamos ou selecionamos os objetos que queremos, usando a palavra-chave `Select`, ou podemos usar `GroupBy`.

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
![Linq](img/linq3.png)

---

## Operadores

### Filtrar Dados
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
Saída:
```
1 2 4 8
2 8 16
1 2 4 32
2 8 16
```

Apesar de escrevermos as consultas de maneiras diferentes nos exemplos 2 e 4, não há diferença na velocidade e nem na performance dessas consultas. O compilador vai otimizar a consulta em ambos os casos.

#### *Filtrando objetos complexos*
```cs
public class Aluno{
    public string Nome {get; set;}
    public int Idade {get; set;}
}

List<Aluno> alunos = new List<Aluno>();
alunos.Add("Maria", 18);
alunos.Add("João", 20);
alunos.Add("Pedro", 25);
alunos.Add("Marlene", 28);
alunos.Add("Fabio", 23);

// sintaxe de método
// selecionando os alunos que têm nomes começados em M e que têm menos de 20 anos de idade 
var resultado = alunos.Where(a => a.Nome.StartsWith('M') 
                            && a.Idade < 20);

foreach(var aluno in resultado)
    {
        Console.WriteLine(aluno.Nome + " - " + aluno.Idade);
    }

// sintaxe de consulta
// mesma consulta que a anterior
var resultado2 = from aluno in alunos 
                where aluno.Nome.StartsWith('M') 
                && aluno.Idade < 20
                select aluno;

foreach(var aluno in resultado2)
    {
        Console.WriteLine(aluno.Nome + " - " + aluno.Idade);
    }

```
Saída:
```
Maria - 18
Maria - 18
```

### Projeção
É o mecanismo usado para selecionar os dados de uma fonte de dados.

Usado para:

1. Selecionar todos os dados no estado original.
2. Criar um novo formato de dados realiazndo operações nos dados originais.

Temos dois métodos usados para projeção na Linq:
- `Select`
    ```
    Permite especificar quais propriedades queremos recuperar: todas as propriedades ou algumas das propriedades.

    Permite realizar alguns cálculos.
    ```
- `SelectMany`
    ```
    É usado para projetar cada elemento de uma sequência para um IEnumerable<T> e, em seguida, nivelar as sequências resultantes em uma sequência.

    Combina os registros de uma sequência de resultados e os converte em um resultado.

    Ele transforma um IEnumerable<IEnumerable<T>> em IEnumerable<T>, ou seja, uma lista de lista para uma lista.
    ```

#### **Exemplos com Select**:

```cs
public class Pessoa{
    // atributos
    public string Nome {get; set;}
    public int Idade {get;set;}
    public double Altura {get;set;}
    
    // construtores
    public Pessoa(string nome, int idade)
    {
        Nome = nome;
        Idade = idade;
    }

    public Pessoa(string nome, int idade, double altura) : base(nome, idade)
    {
        Altura = altura;
    }
}

List<Pessoa> pessoas = new List<Pessoa>();
pessoas.Add(new Pessoa("Maria", 20, 1.68));
pessoas.Add(new Pessoa("João", 17, 1.80));
pessoas.Add(new Pessoa("Diego", 26, 1.76));
pessoas.Add(new Pessoa("Carla", 31, 1.73));
pessoas.Add(new Pessoa("Roberta", 35, 1.70));


//selecionando apenas o nome das pessoas
List<string> nomePessoas = pessoas.Select(p => p.Nome);

foreach(string nome in nomePessoas)
    Console.WriteLine(nome);

//fazendo novos objetos do mesmo tipo com o outro construtor
List<Pessoa> pessoas2 = pessoas.Select(p => new Pessoa(p.Nome, p.Idade)).ToList();

foreach(Pessoa p in pessoas2)
    Console.WriteLine($"{p.Nome} - {p.Idade}");

//criando objetos anônimos com a lista de pessoas
var pessoasTipoAnonimo = pessoas.Select(p => new
                                    {
                                        Nome = p.Nome,
                                        Idade = p.Idade,
                                        Altura = p.Altura
                                    }).ToList();

foreach(var anonimo in pessoasTipoAnonimo)
    Console.WriteLine($"{anonimo.Nome} - {anonimo.Idade} - {anonimo.Altura}");

```
Saída:
```
Maria
João
Diego
Carla
Roberta
Maria - 20  
João -  17
Diego - 26
Carla - 31  
Roberta - 35
Maria - 20 - 1.68
João -  17 - 1.80
Diego - 26 - 1.76
Carla - 31 - 1.73
Roberta - 35 - 1.70
```

```cs
public class Funcionario
{
    public string Nome {get; set;}
    public int Idade {get; set;}
    public decimal Salario {get; set;}
}

List<Funcionario> funcionarios = new List<Funcionario>();
funcionarios.Add(new Funcionario()
{
    Nome = "Manoel",
    Idade = 38,
    Salario = 4125.45m
});

funcionarios.Add(new Funcionario()
{
    Nome = "Carlos",
    Idade = 20,
    Salario = 2726.31m
});

funcionarios.Add(new Funcionario()
{
    Nome = "Alice",
    Idade = 27,
    Salario = 5817.67m
});

// calculando o salário anual de cada funcionário com tipo anonimo
var funcionariosSalarioAnual = funcionarios.Select(f => new
                                            {
                                                Nome = f.Nome,
                                                SalarioAnual = f.Salario * 12
                                            }).ToList();

foreach(var func in funcionariosSalarioAnual)
    Console.WriteLine($"{func.Nome} - R$ {func.SalarioAnual}");
```
Saída
```
Manoel - R$ 49.505.40
Carlos - R$ 32.715.72
Alice - R$ 69.812.04
```

#### **Exemplos com SelectMany**:

```cs
List<List<int>> listas = new List<List<int>>()
{
    new List<int>() {1, 2, 3},
    new List<int>() {12},
    new List<int>() {5, 6, 5, 7},
    new List<int>() {10, 10, 10, 12, 13}
};

IEnumerable<int> resultado = listas.SelectMany(lista => lista);

foreach(var i in resultado)
    Console.Write(i + " ");
Console.WriteLine();

//agora pegando elementos distintos
IEnumerable<int> resultado2 = listas.SelectMany(lista => lista.Distinct());

foreach(var n in resultado2)
	Console.Write(i + " ");
```
Saída:
```
1 2 3 12 5 6 5 7 10 10 10 12 13
1 2 3 12 5 6 7 10 13
```

#### **Comparando Select com SelectMany**:

```cs
public class Aluno{
	public string Nome {get; set;}
	public int Idade {get; set;}
	public List<string> Cursos {get; set;}
}

List<Aluno> alunos = new List<Aluno>()
{
	new Aluno("Maria", "18", new List<string>{"C#", "POO"});
	new Aluno("Alberto", "31", new List<string>{"Javascript", "HTML5", "CSS"});
	new Aluno("Miguel", "23", new List<string>{"Node", "React"});
};

// usando Select
IEnumerable<List<String>> retornoSelect = alunos.Select(a => a.Cursos);

foreach(List<String> listaCursos in retornoSelect)
{
	foreach(string curso in listaCursos)
	{
		Console.Write(curso + " ");
	}
	Console.WriteLine();
}

// usando SelectMany
IEnumerable<String> retornoSelectMany = alunos.SelectMany(a => a.Cursos);

foreach(string curso in retornoSelectMany)
{
	Console.Write(curso + " ");
}

```

Saída:
```
C# POO
Javascript HTML5 CSS
Node React
C# POO Javascript HTML5 CSS Node React
```






## Creditos
Estas anotações foram feitas baseado nas aulas do professor Jose Carlos Macoratti, que as disponibilizou em uma [playlist](https://www.youtube.com/watch?v=Mi2_wpcawGw&list=PLJ4k1IC8GhW0yky43O7TeNwRvaVrHdOmJ) no youtube.
