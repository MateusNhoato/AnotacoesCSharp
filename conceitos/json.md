Java Script Object Notation, é um formato compacto e leve, de padrão aberto independente, de troca de dados simples e rápida entre sistemas que utiliza texto legível a humanos, no formato **atributo-valor**. Espeficado por Douglas Crockford em 2000.

## Sintaxe

- Dados JSON estão definidos aos pares no formato **chave:valor** ("nome": "João")
- Os dados são separados por vírgulas
- As chaves { } contém objetos
- Os colchetes [ ] expressam arrays

## Valores usados

- Um número (inteiro ou ponto flutuante)
- Uma string (entre aspas)
- Um booleano
- Um array (entre colchetes [ ])
- Um objeto (entre chaves { })
- Null (nulo)


## Json x XML

### Semelhanças:

- Ambos são textos simples
- São "auto-descritivos"
- São hierárquicos (valores dentro de valores)
- Podem ser analisados pelo JavaScript

### Diferenças:

- JSON não utiliza a tag de fechamento
- JSON é mais curto, simples e mais rápido de ler/escrever
- JSON utiliza arrays
- JSON não possui palavras reservadas
- JSON possui parser (analizador) nas principais linguagens

Logo, JSON é menor do que XML, mais rápido e mais fácil de ler, escrever,  e analisar.


## JSON - ASP .NET Core

A classe **HttpClient** é usada para enviar uma requisição HTTP e receber a resposta da solicitação.

Métodos:
- `GetAsync`
- `PostAsync`
- `DeleteAsync`
- `PutAsync`
