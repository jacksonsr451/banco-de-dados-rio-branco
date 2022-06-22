[Retornar](../README.md)

# CREATE DATABASE

Nome CREATE DATABASE -- cria um banco de dados

```sql
CREATE DATABASE nome
    [ [ WITH ] [ OWNER [=] dono_do_banco_de_dados ]
           [ TEMPLATE [=] modelo ]
           [ ENCODING [=] codificação ]
           [ TABLESPACE [=] espaço_de_tabelas ]
           [ CONNECTION LIMIT [=] limite_de_conexões ] ]
```

## Descrição

O comando CREATE DATABASE cria um banco de dados do SQL.

Para poder criar um banco de dados é necessário ser um superusuário ou possuir o privilégio especial CREATEDB. Consulte o comando CREATE USER.

Normalmente, o criador se torna o dono do novo banco de dados. Os superusuários podem criar bancos de dados cujos donos são outros usuários utilizando a cláusula OWNER e podem, até mesmo, criar bancos de dados cujos donos são usuários sem nenhum privilégio especial. Os usuários comuns com privilégio CREATEDB podem criar apenas bancos de dados cujos donos são eles mesmos.

Por padrão, o novo banco de dados é criado clonando o banco de dados padrão do sistema template1. Pode ser especificado um banco de dados modelo diferente escrevendo TEMPLATE modelo. Em particular, escrevendo TEMPLATE template0 pode ser criado um banco de dados básico contendo apenas os objetos padrão pré-definidos pela versão do PostgreSQL em uso. Esta forma é útil quando se deseja evitar a cópia de qualquer objeto da instalação local que possa ter sido adicionado ao banco de dados template1. 

### Parâmetros

* nome:
    
    ```O nome do banco de dados a ser criado.```
* dono_do_banco_de_dados:
    
    ```O nome do usuário do banco de dados que será o dono do novo banco de dados, ou DEFAULT para usar o padrão (ou seja, o usuário que está executando o comando).```
* modelo:
    
    ```Nome do modelo a partir do qual o novo banco de dados será criado, ou DEFAULT para utilizar o modelo padrão (template1).```
* codificação:
    
    ```Codificação do conjunto de caracteres a ser utilizado no novo banco de dados. Deve ser especificada uma constante cadeia de caracteres (por exemplo, 'SQL_ASCII'), ou o número inteiro da codificação, ou DEFAULT para utilizar a codificação padrão. Os conjuntos de caracteres suportados pelo PostgreSQL estão descritos na Seção 21.2.1.```
* espaço_de_tabelas:
  
    ```O nome do espaço de tabelas associado ao novo banco de dados, ou DEFAULT para utilizar o espaço de tabelas do banco de dados modelo. Este espaço de tabelas é o espaço de tabelas padrão para os objetos criados neste banco de dados. Para obter informações adicionais deve ser consultado o comando CREATE TABLESPACE.```
* limite_de_conexões:
    
    ```Quantas conexões simultâneas podem ser estabelecidas com este banco de dados. -1 significa sem limite.```

Os parâmetros opcionais podem ser escritos em qualquer ordem, e não apenas na ordem mostrada acima.
Observações

O comando ```CREATE DATABASE``` não pode ser executado dentro de um bloco de transação.

Erros contendo "could not initialize database directory" (não foi possível inicializar o diretório do banco de dados) estão normalmente relacionados com a falta de permissão no diretório de dados, disco cheio, ou outros problemas no sistema de arquivos.

Para remover o banco de dados deve ser utilizado o comando ```DROP DATABASE```.

O aplicativo createdb, fornecido por conveniência, é um programa escrito em C que chama internamente este comando.

Embora seja possível copiar outro banco de dados em vez do template1 especificando seu nome como modelo, não se pretende (ainda) que esta seja uma funcionalidade de "COPY DATABASE" de uso geral. A principal limitação é que não podem existir outras sessões conectadas ao banco de dados modelo enquanto este está sendo copiado. O comando ```CREATE DATABASE``` falha ao iniciar quando existe qualquer outra conexão; caso contrário, as novas conexões ao banco de dados modelo são bloqueadas até que o comando ```CREATE DATABASE``` termine. 

A opção ```CONNECTION LIMIT``` é imposta apenas aproximadamente; se duas novas sessões começarem aproximadamente ao mesmo tempo quando restar apenas um "encaixe" de conexão no banco de dados, será possível que ambas falhem. Além disso, o limite não é imposto aos superusuários.
Exemplos

Para criar um banco de dados:

```sql
CREATE DATABASE lusiadas;
```
Para criar o banco de dados vendas pertencendo ao usuário usuvendas com o espaço de tabelas padrão espvendas:

```sql
CREATE DATABASE vendas OWNER usuvendas TABLESPACE espvendas;
```
Para criar o banco de dados musica com suporte ao conjunto de caracteres ISO-8859-1:

```sql
CREATE DATABASE musica ENCODING 'LATIN1';
```
