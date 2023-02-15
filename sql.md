## Banco de Dados

É um lugar onde guardamos informações padronizadas.

## SGBD

Sistema de Gerenciamento de Banco de Dados, um exemplo seria o mySQL.

## Tabela

### Índice / Chave

Valor que identifica uma determinada 'linha' da tabela.

### Tipos de dados numa tabela

- Int -> usado para Id, idade de pessoas, número de compras, etc

- Varchar -> se trata de uma string que podemos definir o tamanho

- Date -> usado para guardar datas   "2023-02-15"

- DateTime -> igual date, mas guarda horário também "2023-02-15 08:11:28"

- Decimal -> número que podemos limitar o número de casas e de casas decimais (padrão usar 10,2)

- LongText -> string grande, que não sabemos o tamanho

- Boolean -> true ou false

### Campo nulo

Ao colocar que um campo pode ser nulo, damos a possibilidade de dito campo não precisar ser preenchido.

### A_I - Auto Incremento

Ao marcar um campo com esta característica (e só funciona com tipos de dados numéricos), toda vez que tivermos uma nova entrada no banco de dados, este campo será igual o passado + 1, isto é, o id da primeira entrada seria 1 enquanto o id da segunda entrada seria 2 e por aí vai.  

### Valor predefinido

É o valor que será alocado no campo da tabela caso não mandarmos a informação do  dito campo.

### Comentários

Podemos atrelar comentários a cada campo de dados na nossa tabela, uma descrição do propósito do campo.

## Como Consultar dados?

Utilizando Structured Query Language -> SQL.

### Cláusulas / Palavras-chave

- `SELECT` - usada para **selecionar** o que queremos 

    Selecionando tudo de uma tabela:
```sql
SELECT * FROM nome_da_tabela
```

    Selecionando colunas de uma tabela:
```sql
SELECT coluna1,coluna2 FROM nome_da_tabela
```

- `WHERE` - usada para **filtar** os dados 

    Filtrando uma tabela:
```sql
SELECT * FROM nome_da_tabela WHERE condicao
```

- `LIMIT` - usada para **limitar** os resultados de uma pesquisa

    Limitando uma filtragem:
```sql
SELECT * FROM nome_da_tabela WHERE condicao LIMIT 10
```
   Retorna os 10 primeiros elementos que  atendem a condicao.

- `AND` - operador lógico "e"
```sql
SELECT * FROM nome_da_tabela WHERE condicao AND condicao2
```
   Retorna somente os elementos que atendem as 2 condições.

- `OR` - operador lógico "ou"
```sql
SELECT * FROM nome_da_tabela WHERE condicao OR condicao2
```
  Retorna os elementos que atendem a primeira condição  ou a  segunda condição. 
  
- `ORDER BY` - usada para **ordenar** os resultados de uma pesquisa

    Ordenando em ordem ascendente:
```sql
SELECT * FROM nome_da_tabela WHERE condicao ORDER BY nome_da_coluna ASC
```

   Ordenando em ordem descendente:
```sql
SELECT * FROM nome_da_tabela WHERE condicao ORDER BY nome_da_coluna DESC
```

   Multiplas ordenações encadiadas:
```sql
SELECT * FROM nome_da_tabela WHERE condicao ORDER BY nome_da_coluna ASC, 
nome_da_coluna2 DESC, nome_da_coluna3 DESC
```

- `COUNT` - retorna **quantos registros existem** no resultado da pesquisa
```sql
SELECT COUNT(*) FROM nome_da_tabela WHERE condicao
```

- `SUM` - retorna a **soma** de uma coluna com valor numérico
```sql
SELECT SUM(nome_da_coluna) FROM nome_da_tabela WHERE condicao
```

- `AVG` - retorna a **média** de uma coluna com valor numérico
```sql
SELECT AVG(nome_da_coluna) FROM nome_da_tabela WHERE condicao
```

- `AS` - usado para **dar um 'apelido'** para colunas (até colunas que criarmos durante a consulta)
```sql
SELECT nome_da_coluna AS coluna_exemplo_1 FROM nome_da_tabela WHERE condicao
```
   No retorno o nome da coluna apareceria como 'coluna_exemplo_1'.

- `UPDATE` - usado para **atualizar** 

   Atualizando pelo id:
```sql
UPDATE nome_da_tabela SET coluna = valor_a_mudar WHERE id = id_para_mudar
```

   Atualizando por condicao:
```sql
UPDATE nome_da_tabela SET coluna = valor_a_mudar WHERE condicao
```

- `DELETE` - usado para **deletar**, ==cuidado com o uso!==

   Deletando pelo id:
```sql
DELETE FROM nome_da_tabela WHERE id= id_para_deletar
```

   Deletando por condicao:
```sql
DELETE FROM nome_da_tabela WHERE condicao
```

- `LIKE` - procura coisas que são parecidas com o que passamos (geralmente usado em strings)
```sql
SELECT * FROM nome_da_tabela WHERE nome_da_coluna LIKE 'condicao'
```

- `IN` - usado para selecionar múltiplos itens da tabela
```sql
SELECT * FROM nome_da_tabela WHERE nome_da_coluna IN (item_da_coluna1, item_da_coluna2...)
```
