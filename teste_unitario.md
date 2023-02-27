Teste unitário é um tipo de teste feito na menor unidade do código, isto é, verificamos a funcionalidade de um método isolado, ou até uma parte de um método.  Por exemplo, se temos uma função que tem uma bifurcação com if e else, faríamos múltiplos testes unitários para ambos os casos (com entradas diferentes). 

O objetivo do teste unitário é assegurar a funcionalidade do código de maneira **modular**. Averiguando todas as partes pequenas temos uma segurança maior que o conjunto está funcionando como um todo. Esta definição é a oposta de Teste de Integração, o tipo de teste que está interessado em como uma unidade de código se comporta **em relação com as outras unidades**.

## 3 As

Os 3 As juntos formam um teste. São eles:

- Arrange -  Instânciamos os objetos necessários para o teste, além de fazer outros tipos de preparação (é opicional)
- Act - Chamamos a função alvo do teste
- Assert - Comparamos o resultado esperado com o que de fato aconteceu na função

Na plataforma .NET temos 3 bibliotecas nativas para testes, o MSTest, NUnit e o xUnit.
Para ilustrar o fucionamento de um teste unitário, vamos utilizar o xUnit. Note-se que é preciso **fazer um novo projeto xUnit** para utilizá-lo no seu projeto. Vamos a um exemplo:

```cs
public class Calculadora{
	public double Somar(double a, double b) => a + b;
}

public class TesteUnitario{
	// instanciando um objeto a partir da classe Calculadora
	private void Calculadora alvoDoTeste = new Calculadora();

	[Fact] // Tag que especifica que a função é um teste
	public void SomaDeDoisValoresRetornaValor()
        {
	        // Arrange - estamos iniciando as variáveis necessárias
	        double a = 10, b= 5;
			// Act - chamando a função que queremos
            double resultado = alvoDoTeste.Somar(a, b);
            // Assert - Comparando o resultado esperado com o retorno da função
            Assert.Equal(15, resultado);
        }
}
```

Usando a calculadora do exemplo acima para escrever múltiplos testes:

```cs				
	// A tag [Theory] especifica que aceita múltiplos testes
	// Quando utilizamos esta tag temos que colocar os parâmetros na função 
	// Assim, conseguimos passar testes diferentes na pela tag InlineData
		[Theory] 
        [InlineData(-500, -700, 200)]
        [InlineData(132, 67, 55)]
        public void SomaDeMultiplosValoresRetornaValor(double esperado, double a, double b)
        {
		    // Act
            double resultado = alvoDoTeste.Somar(a,b);
            // Assert
            Assert.Equal(esperado, resultado);
        }
```

## TDD

Test Driven Development ou Test Driven Design. Se trata de um tipo de design de software onde os testes precedem a escrita do código em si. Esta abordagem tem 2 focos: os pré-requisitos e o resultado. Quando escrevemos um teste antes do próprio código, o resultado é mais relevante que o processo que levará ao resultado e os pré-requisitos ficam mais claros.

O TDD é feito ciclicamente, e este ciclo é dividido em 3 fases:

![tdd](./img/tdd.png)
- Red - escrevemos um teste que **irá falhar**
- Green - fazemos o código funcionar de uma maneira que o teste passe
- Refactor - reescrevemos o código fazendo ajustes (se necessário) 

Após o Refactor, escrevemos outro teste para falhar (logo, voltamos para o Red).
