Programação Orienta a Objetos - se trata de um paradigma, isto é, uma maneira diferente (ou um modelo) de se pensar. POO nos permite trazer coisas reais para nossos programas através de **_Abstrações_**. Em outras palavras, podemos criar representações de objetos tangíveis ou conceitos intangíveis, dividindo suas características (atributos) e ações (métodos) em [classes](classe.md) personalizadas que podemos usar em nosso programa. Essas classes personalizadas são úteis porque nos permitem organizar o código de forma mais clara e concisa. 

Podemos criar objetos a partir dessas classes, que contêm informações e comportamentos específicos, tornando nosso código mais modular e fácil de entender e manter. Com a POO, podemos criar programas mais robustos e flexíveis, capazes de lidar com uma variedade de situações reais. 

## Os quatro pilares de POO:

1. Abstração 
2. Encapsulamento 
3. [Herança](heranca.md) 
4. [Polimorfismo](polimorfismo.md) 

### Abstração

Se trata do processo de **descrever algo usando apenas os detalhes relevantes ao contexto em que está sendo usado**.

Em POO, isso significa que criamos classes e objetos que representam entidades reais, mas apenas incluímos atributos e métodos relevantes para o objetivo do programa. Ao usar a abstração, podemos criar classes que são mais fáceis de entender, manter e reutilizar, tornando nossos programas mais eficientes e eficazes. 

### Encapsulamento

Se trata do processo de esconder, isto é, **ocultar detalhes que não precisam ser mencionados**.

Em POO encapsulamento tem dois significados muito importantes:
1. Em uma classe, podemos definir quais atributos e métodos devem ser [acessíveis](modificadores_de_acesso.md) de fora da classe e quais devem ser mantidos privados. A ideia é permitir que outras partes do programa usem a classe de forma segura, sem precisar saber como ela funciona internamente. Por exemplo, podemos definir um método privado numa classe que realiza alguma operação interna, mas que não precisa ser acessado de fora da classe. Isso garante que o método seja seguro e estável, sem interferências de outras partes do programa. 
2. Ao utilizar classes de programas e bibliotecas de terceiros, não precisamos saber exatamente como a classe funciona por dentro, mas precisamos entender a ação resultante dos métodos da classe. Isso permite que possamos usar o código de maneira eficiente, sem precisar conhecer todos os detalhes da implementação. Nesse sentido, a documentação da classe se torna extremamente importante, pois é nela que podemos encontrar informações sobre como usar os métodos de uma classe de forma eficaz. 

Ao encapsular uma classe, podemos tornar nossos programas mais robustos e fáceis de usar, permitindo que outras partes do programa usem a classe de forma segura e eficiente, sem precisar conhecer todos os detalhes da implementação. 

### Herança

A palavra herança tem como definição "ação de herdar, de adquirir por sucessão". No mundo real podemos herdar características (atributos) de nossos pais, como a cor dos olhos. Ou, da mesma maneira, podemos herdar trejeitos (métodos), como a forma de andar. 

Em POO, herança se trata de uma relação entre classes. Nesta relação uma classe filha (também chamado de classe derivada) _herda_, isto é, adquire as características de uma classe mãe (também chamada de classe pai ou classe base). O principal objetivo com herança é a redução de duplicidade de código, uma vez que a classe derivada tem acesso aos atributos e métodos da classe base.

Um conceito muito importante também é o de _classes abstratas_. Elas são classes que não podem ser instanciadas (ter um objeto criado a partir delas), mas são usadas como base para outras classes. 

Podemos criar uma hierarquia complexa de múltiplas camadas com a herança. Existem linguagens que permitem herança múltipla, isto é, que uma classe herde de várias outras, enquanto há outras que uma classe pode herdar de somente uma classe. 

### Polimorfismo

Polimorfismo é "qualidade ou estado de conseguir assumir diferentes formas".

Em POO, polimorfismo é uma característica que dá flexibilidade, uma vez que objetos de diferentes classes podem ser tratados de maneira uniforme, contanto que compartilharem da mesma classe base ou uma interface em comum. Existem duas formas de polimorfismo: o de sobrecarga (também conhecido como sobrecarga de método) e o polimorfismo de sobreposição(também conhecido como sobrescrita de método). 

No polimorfismo de sobrecarga, como diz no nome, adicionamos sobrecargas, isto é, fazemos mais funções com o mesmo nome, porém com parâmetros diferentes. Logo, ao chamar a mesma função com parâmetros diferentes, temos **comportamentos diferentes**. 

No polimorfismo de sobreposição, uma classe derivada, isto é, uma classe que herda os atributos e métodos de uma classe base, pode sobrescrever (ou mudar) as características que recebeu da classe base. Um exemplo seria uma classe derivada "ContaPoupanca" herdar da classe base "Conta", mas alterar o atributo "RendimentoDaConta" que foi herdado. Apesar de ambas as classes terem o mesmo atributo, ao observarmos estes atributos, eles são diferentes. No caso de métodos a analogia é parecida, mas dizemos que os métodos se **comportam de maneiras distintas**.