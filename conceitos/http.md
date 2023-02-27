## Request

Uma requisição HTTP se divide em 3 partes:

1. `Request line` - Método HTTP + URI + protocolo HTTP
```
GET /api/exemplo HTTP/1.1
POST /api/exemplo/ HTTP/1.1
```

2. `Headers` - Metadados que se enviam na requisição com informação
```
Host: Microsoft.com
Cache-Control: no-cache
Accept: text/*
Accept-Language: pt-br
```

3. `Body` (opcional) - Informação adicional enviado ao servidor
```
Dados de Texto
Dados JSON / XML
```

==O request GET não possui Body==.

## Response

Uma resposta HTTP se divide em 3 partes:

1. `Status line` - Indica o status da requisição (Código Status HTTP)
```
HTTP/1.1 200 OK
HTTP/1.1 404 Not Found
```

2. `Headers` - Metadados enviados na resposta
```
Content-type: text-plain
Content-length: 80
```

3. `Body`(opicional) - Dados enviados pelo servidor
```
Dados de Texto
Dados JSON
```


## Métodos HTTP

Para consumir os recursos de uma Web API RESTful usamos os métodos HTTTP.

### GET

- Método de leitura, é usado para recuperar informações (retornar a representação do recurso)
- Não altera o estado do recurso (método seguro)
- é idempotente (produz o mesmo resultado se a requisição é repetida)
- Possíveis retornos para o código de status HTTP
	- recurso encontrado: 200 OK
	- recurso não encontrado: 404 NOT FOUND

Exemplos de URI:
```
GET http://localhost/api/exemplo
GET http://localhost/api/exemplo/id
```

### POST

- Método de criação, usado para criar uma informação (cria um novo recurso)
- Altera o estado do recurso (não é um método seguro)
- Não são idempotentes (não produz o mesmo resultado se repetida)
- Possíveis retornos para o código de status HTTP
	- recurso criado: 201 CREATED
	- recurso não identificado: 200 OK ou 204 NO CONTENT

Exemplos de URI:
```
POST http://localhost/api/exemplo 

/*informações do recurso são passadas no body*/
```

### PUT

- Usado para atualizar uma informação (atualizar um recurso)
- Altera o estado do recurso (não é um método seguro)
- É idempotentente (produz o mesmo resultado se a requisição é repetida)
- Possíveis retornos para o código de status HTTP
	- recurso alterado: 200 OK ou 204 NO CONTENT
	- recurso criado: 201 CREATED (*API decide*)
	- recurso não localizado: 404 NOT FOUND

Exemplos de URI:
```
PUT http://localhost/api/exemplo 

/*informações do recurso são passadas no body*/
```

### DELETE

- Usado para deletar uma informação (excluir um recurso)
- Altera o estado do recurso (não é um método seguro)
- É idempotente (produz o mesmo resultado se a requisição é repetida)
- Possíveis retornos para o código de status HTTP
	- recurso excluído: 200 OK
	- recurso não localizado: 404 NOT FOUND

Exemplos de URI:
```
DELETE http://localhost/api/exemplo/id
```

![web_api5](img/web_api5.png)

[CRUD](conceitos/crud.md) - Create (POST) Read (GET) Update (PUT) Delete (DELETE)

## HTTPS

O **HTTPS** é uma extensão **segura** do HTTP.

TLS - Transport Layer Security: permite a comunicação criptografada entre um site e uma navegador e substitui o protocolo SSL (Secure Sockets Layer). Os sites que configurarem um certificado TLS podem utilizar o protocolo HTTPS para estabelecer uma comunicação segura com o servidor.

O objetivo do TLS é tornar segura a transmissão de informações sensíveis, como dados pessoas, de pagamentos ou login.

### ASP .NET Core e HTTPS

Ao criar o projeto ASP .NET Core são definidos os middlewares:

1. HTTP de redirecionamento - `app.UseHtppsRedirection` - que redireciona uma requisição HTTP para HTTPS
2. HSTS - `app.UseHsts` - Envia ao cliente um header `Strict-Transport-Security(HSTS)` que indica aos navegadores que nossa API deve ser acessada via https e não via http

==Nota: WEB APIS não devem usar o atributo **RequireHttps**==.


