# [Comandos básicos Linux, MySQL, vi, MariaDB ](https://mlssystem.github.io/comandos/)


## _MySQL_


# COMANDOS RELACIONADOS AO USUÁRIO
font: arquivos pessoais de diversas consultas na internet, nem sempre salvo o link, ia salvando no notpad, mas os que tiverem o link, faço qusteão de postar.


## CRIANDO USUARIO
```

MariaDB [(none)]> CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'senha';

```


## DELETANDO USUÁRIOS
```

DROP USER ‘demo’@‘localhost’;

```


## SELECIONANDO USUARIOS DO BANCO DE DADOS
```

mysql> SELECT user FROM mysql. user;

```


## ALTERANDO SENHA DO USUÁRIO
```

mysqladmin -h localhost -u <usuario> -p password

```


## SE ESQUECER A SENHA USAR AS 4 LINHAS DE COMANDO ABAIXO
```

sudo /etc/init.d/mysql stop
sudo mysqld --skip-grant-tables &
mysql -u root mysql 

UPDATE user SET Password=PASSWORD('NOVASENHA') WHERE User='root'; FLUSH PRIVILEGES; exit;

```


# COMANDOS RELACIONADOS A PREMISSÕES


## CONCEDENDO PRIVILEGIOS PARA USUARIOS
```	

GRANT ALL PRIVILEGES ON * . * TO 'novousuario'@'localhost';

```


## ATUALIZANDO PERMISSÃO
```

FLUSH PRIVILEGES;

```


## VERIFICANDO PRIVILEGIOS PARA USUARIOS
```

SHOW GRANTS FOR CURRENT_USER;
SHOW GRANTS FOR 'mandic'@'localhost';

```


## TIRANDO PRIVILÉGIOS
```

REVOKE [tipo de permissão] ON [nome da base de dados].[nome da tabela] FROM ‘[nome do usuário]’@‘localhost’;	

```

--- 

# CRIANDO BANCO DE DADOS teste MySQL
font: [Elias Praciano](https://elias.praciano.com/2013/02/mysql-comandos-basicos/)
```

CREATE DATABASE nome-do-banco;

```


## CONSULTAR BANCO DE DADOOS
```

SHOW DATABASES;

```


## LISTAR BANCO DE DADOS
```

SHOW DATABASES;

```


## SELECIONAR BANCO DE DADOS
```

USE testes;

```


# TABELAS

## CRIAR TABELA clientes
```

CREATE TABLE clientes (
idCliente INT NOT NULL auto_increment,
nomeEmpresa varchar(255),
nomeDiretor varchar(255),
numEmpregados varchar(255),
PRIMARY KEY (idCliente) auto_incremento=1);

```


## LISTAR TABELAS
```

SHOW tables;

```


## ESTRUTURA DA TABELA
```

DESCRIBE clientes;

```


## INSERIR DADOS NA TABELA
```

INSERT INTO clientes (idCliente, nomeEmpresa, nomeDiretor, numEmpregados) VALUES (1,"Malesuada Inc.","Johnny Pedd",4847);
INSERT INTO clientes (idCliente, nomeEmpresa, nomeDiretor, numEmpregados) VALUES (2,"Aliquam Inc.","Al Capino",4135);
INSERT INTO clientes (idCliente, nomeEmpresa, nomeDiretor, numEmpregados) VALUES (3,"Union Carbide","Robert Ne Diro",3755);
INSERT INTO clientes (idCliente, nomeEmpresa, nomeDiretor, numEmpregados) VALUES (4,"Magna Carta Ltda.","Wenzel Dashington",3071);
INSERT INTO clientes (idCliente, nomeEmpresa, nomeDiretor, numEmpregados) VALUES (5,"Nunc Corp.","",3859);
INSERT INTO clientes (idCliente, nomeEmpresa, nomeDiretor, numEmpregados) VALUES (6,"In Company","Macaulay Bulkin",4440);

```

Como o campo idCliente foi criado com o parâmetro auto_increment. Seu preenchimento é automático. Você não precisa informar o seu valor, portanto:
```

INSERT INTO clientes
(idCliente, nomeEmpresa, nomeDiretor , numEmpregados)
VALUES ('',"GameCorp.","Din Viesel",2071);

```


## CONSULTAR CONTEÚDO DA TABELA
```

SELECT * FROM clientes;

``` 

### Consultar conteúdo específico
```

SELECT id_cliente, nome_empresa FROM clientes;

```


## DELETAR DADO DA TABELA
```

DELETE FROM nome-da-tabela WHERE nome-da-coluna=texto;

``` 

### Exemplo DELETE
```

DELETE FROM clientes WHERE nomeEmpresa = 'GameCorp';

```

Com este comando, TODOS os registros que tiverem nomeEmpresa = 'GameCorp' serão eliminados. Neste caso, há apenas 1. Mas vamos imaginar que houvesse 10 ou 100 registros em que o nomeEmpresa fosse igual a GameCorp. Neste caso, seria necessário usar outro campo como referência para encontrar o registro que eu desejo eliminar. No nosso caso, há o campo idCliente, que é único – ele não se repete dentro da tabela:
```

DELETE FROM clientes WHERE idCliente = 7;

```


## DELETAR TABELA
Seja cuidadoso(a). O comando DROP apaga permanentemente uma tabela ou um banco de dados. Veja como usar o DROP para eliminar uma tabela:
```

DROP TABLE nome-da-tabela;

```


## DELETAR BANCO DE DADOS
```

DROP DATABASE nome-do-banco;

```


## LIMPAR CONTEÚDO DA TABELA
Para limpar uma tabela, use o comando TRUNCATE. Internamente, ele remove a tabela primeiro e, depois, a recria com a mesma estrutura só que sem os dados. Se houver um contador AUTO_INCREMENT, na tabela em questão, ele é zerado e recolocado. Veja como funciona:
```

TRUNCATE TABLE nome-da-tabela;

```

## ALETAR UM REGISTRO NA TABELA
Aqui, o comando UPDATE entra em ação. Vamos ver como usá-lo para alterar o valor de um campo dentro de um registro:
```

UPDATE clientes SET numEmpregados=1999 WHERE idCliente = 1;

```
--- 


# COMANDOS _SHOW_, USADO PARA CONSULTAR OS DADOS

fonte: [Boson Treinamentos](http://www.bosontreinamentos.com.br/mysql/mysql-comandos-show-describe-e-mysqlshow-39/)



## ACESSE O BANCO DE DADOS
```

mysql -u root -p
HELP SHOW;

```


## EXEMPLOS DE USO DO COMANDO _SHOW_:
Ver os bancos de dados presentes no sistema:
```

SHOW DATABASES;

```


## INFORMAÇÕES SOBRE PROCEDIMENTOS ARMAZENADOS E FUNÇÕES
```

SHOW CREATE PROCEDURE verpreço;
SHOW CREATE FUNCTION calcula_desconto;

```


## CÓSDIGO USADO PARA CRIAR TABELA
```

SHOW CREATE TABLE tbl_Livro;

``` 


## MOSTRA TABELA DO BANCO ATUAL
```

SHOW TABLES;

```


## MOSTRAR COLUNAS DA TABELA
```

SHOW [FULL] COLUMNS FROM tbl_editoras;

```


## MOSTRAR COLUNA ESPECIFICA
```

SHOW COLUMNS FROM tbl_Livro LIKE ‘I%’;

```


## MOSTRAR TIPO DE DADO
```

SHOW COLUMNS FROM tbl_Livro WHERE Type like ‘varchar%’;

```


## MOSTRAR PRIVILÉGIOS PARA USUÁRIOS
```

SHOW GRANTS FOR root@localhost;

```


# COMANDO DESCRIBE
fonte: [Boson Treinamentos](http://www.bosontreinamentos.com.br/mysql/mysql-comandos-show-describe-e-mysqlshow-39/)

O comando DESCRIBE é um atalho para o comando SHOW COLUMNS FROM;
Exemplo:
```

DESCRIBE tbl_Livro;

```

O comando DESCRIBE também pode ser abreviado para:
```

DESC tbl_Livro;

```
Obs. O comando DESCRIBE não suporta as cláusulas LIKE e WHERE.


# COMANDO MYSQLSHOW
fonte: [Boson Treinamentos](http://www.bosontreinamentos.com.br/mysql/mysql-comandos-show-describe-e-mysqlshow-39/)

O comando mysqlshow opera diretamente no shell do Linux. 
Ele permite obter informações sobre os bancos de dados, tabelas e colunas.

```

mysqlshow -u usuário -p [banco [tabela [coluna]]]

```

Exemplos do comando mysqlshow:

## VER OS BANCOS DE DADOS DISPONÍVEIS:
```

mysqlshow -u root -p

```

## VER AS TABELAS EM UM BANCO DE DADOS ESPECÍFICO:
```

mysqlshow -u root -p db_Biblioteca

```

##  VER OS CAMPOS PERTENCENTES A UMA TABELA:
```

mysqlshow -u root -p db_Biblioteca tbl_autores %

```

## VER AS TABELAS COM CONTAGEM DE COLUNAS E LINHAS, COMEÇANDO COM UMA LETRA ESPECÍFICA:
```

mysqlshow -vv -u root -p db_Biblioteca ‘t*’

```

## VER INFORMAÇÕES SOBRE UMA COLUNA ESPECÍFICA EM UMA TABELA:
```

mysqlshow -u root -p db_Biblioteca tbl_autores ID_autor

```

**Obs: Usamos % no final do comando para que o shell não interprete tbl_autores como wildcard, e sim como o parâmetro tabela; esse problema ocorre quando temos o caractere underline ( _ ) no nome da tabela.**
