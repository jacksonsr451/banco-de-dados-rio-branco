[RETORNAR](../README.md)

# CREATE TABLE

*Use o comando CREATE TABLE para criar uma nova tabela inicialmente vazia no banco de dados atual. O comando CREATE TABLE cria automaticamente um tipo de dado que representa o tipo tupla (tipo de estrutura) correspondente a uma linha da tabela.*


### Uma tabela não pode ter:

- O mesmo nome que qualquer tipo de dado existente.
- O mesmo nome que uma tabela de catálogo do sistema.
- Mais de 1600 colunas. O limite efetivo é ligeiramente menor devido às  restrições de comprimento de tupla.
- Atributos de tabela ou visualização com os seguintes nomes:
    * cmax
    * cmin
    * createxid
    * ctid
    * datasliceid
    * deletexid
    * oid
    * rowid
    * tableoid
    * xmax
    * xmin


#### EXEMPLOS:


```sql
CREATE TABLE alunos (
    ID int,
    nome CHAR(255),
  	PRIMARY KEY(ID)
);

CREATE TABLE sala_de_aula(
	ID int,
  	vagas char(2),
  	PRIMARY KEY(ID)
);
```

**Com este simples comando criamos nossas tabelas** 
```sql
CREATE TABLE nome_da_tabela(
    campos tipo_de_dado
)
```