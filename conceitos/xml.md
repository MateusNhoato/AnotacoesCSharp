XML é a sigla para "Extensible Markup Language", uma linguagem de marcação com regras para formatar documentos. Se trata de um documento em que as informações são guardadas por tags (parecido com HTML, mas as tags são mais flexíveis, uma vez que os próprios usuários podem fazer tags). Arquivos XML são utilizados para o registro de **notas fiscais** no Brasil.

## Como funciona?

```xml
<?xml version="1.0"> 
<livros> 
<livro id="1"> 
<titulo>O Pequeno Príncipe</titulo>  
<genero>Infantil</genero> 
</livro> 
</livros>
```

- Todo documento XML deve ter a tag introdutória  `<?xml version="1.0">`, para indicar a versão
- O documento deve trer uma tag principal, que sirva de "raiz" (root) para os outros elementos
- Todo elemtno XML deve ter uma tag de abertura e uma de fechamento, com exceção das tagas revervada de utilização única (como a introdutória)

## Regras de design do XML

Para um documento XML estar formatado de maneira correta, as seguintes condições têm de ser cumpridas:

- O documento tem de estar bem formado
- O documento tem que cumprir com todas as regras de *sintaxe* da XML
- O documento tem de estar nos padrões das regras *semânticas*, que geralmente ficam em um documento 'XML schema' ou um 'DTD' (Document Type Definition)

Exemplo: Um documento que contém uma tag que não foi definida no XML schema ou DTD é inválido.