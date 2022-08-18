# Regras e tipos relacionamentos em SQL

Voltando a partir de onde paramos, veja mais um tipo de relacionamento:

N:N – O relacionamento N:N (muitos-para-muitos) possui uma característica diferente dos outros. Neste caso, os dados estão diretamente relacionados ao fato, e não as entidades, como observamos nos outros tipos de relacionamentos vistos anteriormente.
Importante destacar que podem não haver associação de fatos nas situações em que os relacionamentos são de caráter condicional.
Neste caso, a cardinalidade deve ser determinada por meio de uma ampla análise quanto à possibilidade de ocorrerem relacionamentos.

Regras de Relacionamento N:N– Para estabelecer este tipo de relacionamento, devemos ter três tabelas, sendo que a terceira é responsável por relacionar as outras duas. Para isso, é preciso que essas duas primeiras tabelas contenham uma coluna que seja chave primária.
As colunas que são chaves primárias na primeira e na segunda tabela devem ser colunas com chave estrangeira na terceira. Assim, esta tabela terá duas chaves estrangeiras, as quais formam uma chave primária composta.

Vimos os tipos de relacionamentos existentes, vamos fazer agora os exemplos práticos com eles.

1:1 –Lembrando que neste relacionamento, cada um dos elementos de uma entidade só pode se relacionar com apenas um elemento de outra entidade. Então, consideremos as tabelas Clientes e Documentos, em que cada um dos clientes pode ter apenas um documento (considerando que nesta tabela um mesmo cliente não pode ter mais de um documento), assim como cada um dos documentos só pode pertencer a apenas um cliente.

Confira nas imagens abaixo a criação das tabelas, das constraints e inserção de alguns registros:
 
Perceba que na tabela Documentos criei uma Foreign Key (chave estrangeira) se relacionando com a Primary Key da tabela Clientes.Veja como ficarão as tabelas:

Assim temos o relacionamento de um-para-um.
1:N – Como dito no artigo anterior, neste relacionamento, que é um dos mais comuns hoje em dia, cada elemento da entidade “A” pode ter um relacionamento com vários elementos da entidade “B”. Em contrapartida, cada um dos elementos da entidade B pode estar relacionado a apenas um elemento da A. Dito isto, consideremos a tabela Clientes já criada e agora vamos criar a tabela Telefones com o código a seguir, já que neste caso cada cliente pode ter vários telefones, mais cada telefone pode pertencer a um, e somente um cliente:

```sql
CREATE TABLE Telefones
(
  IdTelefone      INT IDENTITY(1,1),
  IdCliente     INT NULL,
  TipoTelefone    VARCHAR(15) NOT NULL,
  NumeroTelefone    VARCHAR(15) NOT NULL

  CONSTRAINT PK_Telefone PRIMARY KEY (IdTelefone),
  CONSTRAINT FK_Telefones_IdCliente FOREIGN KEY (IdCliente)
          REFERENCES Clientes (IdCliente)
)
```

--Insiro alguns registros na tabela Telefones
```sql
INSERT INTO Telefones VALUES (1, 'Residencial', '3243-2015')
INSERT INTO Telefones VALUES (3, 'Comercial', '3221-0132')
INSERT INTO Telefones VALUES (1, 'Celular', '9777-2112')
INSERT INTO Telefones VALUES (2, 'Residencial', '3353-9899')
INSERT INTO Telefones VALUES (2, 'Celular', '8871-1015')
```

Confira nas imagens a seguir a inserção de alguns registros e o resultado da consulta a ela:
 
Assim temos o relacionamento de um-para-muitos.

N:N – Relembrando, neste relacionamento, que é diferente dos outros, os dados estão diretamente relacionados ao fato, e não às entidades, como os outros dois anteriores. Seguindo as regras deste tipo de relacionamento, temos que, obrigatoriamente, criar três tabelas, já que a terceira tem a responsabilidade crucial de fazer o relacionamento entre as outras duas.

Para uma melhor compreensão, vamos usar novamente a tabela Clientes e a tabela Pedidos, criada no artigo anterior. Com elas, temos a seguinte situação: um cliente pode fazer diversos pedidos, ao passo que um pedido pode ser feito por diversos clientes.

Como já temos as tabelas criadas, vamos apenas criar a terceira tabela, denominada ClientesXPedidos, responsável por interliga-las. Veja as imagens a seguir de sua criação, inserção de registros (note que ela conterá apenas as chaves das duas outras tabelas) e posterior consulta:

Perceba na imagem acima que os mesmos campos, IdCliente e IdPedido, são chaves primárias e também são chaves estrangeiras, criando assim o relacionamento entre as tabelas Cliente e Pedido.

