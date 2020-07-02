# Comandos básicos Linux, MySQL, vi, MariaDB 

# [_MySQL_]()

## COMANDOS RELACIONADOS AO USUÁRIO
font: arquivos pessoais de diversas consultas na internet, nem sempre salvo o link, ia salvando no notpad, mas os que tiverem o link, faço qusteão de postar.

* CRIANDO USUARIO
```
MariaDB [(none)]> CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'senha'
```
* DELETANDO USUÁRIOS
```
DROP USER ‘demo’@‘localhost’;
```

* SELECIONANDO USUARIOS DO BANCO DE DADOS
```
mysql> SELECT user FROM mysql. user;
```

* ALTERANDO SENHA DO USUÁRIO
```
mysqladmin -h localhost -u <usuario> -p password
```

* SE ESQUECER A SENHA USAR AS 4 LINHAS DE COMANDO ABAIXO
```
sudo /etc/init.d/mysql stop
sudo mysqld --skip-grant-tables &
mysql -u root mysql 
UPDATE user SET Password=PASSWORD('NOVASENHA') WHERE User='root'; FLUSH PRIVILEGES; exit;
```

## COMANDOS RELACIONADOS A PREMISSÕES

* CONCEDENDO PRIVILEGIOS PARA USUARIOS
```	
GRANT ALL PRIVILEGES ON * . * TO 'novousuario'@'localhost';
```

* ATUALIZANDO PERMISSÃO
```	
FLUSH PRIVILEGIOS	
```

*  VERIFICANDO PRIVILEGIOS PARA USUARIOS
```
SHOW GRANTS FOR CURRENT_USER;
SHOW GRANTS FOR 'mandic'@'localhost';
```

* TIRANDO PRIVILÉGIOS
```	
REVOKE [tipo de permissão] ON [nome da base de dados].[nome da tabela] FROM ‘[nome do usuário]’@‘localhost’;	
```

--- 

## Como criar um banco de dados no MySQL
font: [Elias Praciano](https://elias.praciano.com/2013/02/mysql-comandos-basicos/)

* O comando para criar um banco de dados é este:
```
CREATE DATABASE nome-do-banco;
```

* Para ver todos os bancos de dados existentes no servidor:
```
SHOW DATABASES;
```

* Em um exemplo prático, a criação do banco de dados testes, ficaria assim:
```
CREATE DATABASE testes;
```

* Você pode exibir os bancos de dados criados, através do comando SHOW (já vimos isso!):
```
SHOW DATABASES;
```
* Antes de criar uma tabela ou realizar qualquer operação, é necessário selecionar o banco de dados que vai ser usado:
```
USE testes;
```

* Agora, vamos criar uma tabela dentro dele, com o nome clientes:

```
CREATE TABLE `clientes` (
`idCliente` mediumint(8) unsigned NOT NULL auto_increment,
`nomeEmpresa` varchar(255),
`nomeDiretor` varchar(255) default NULL,
`numEmpregados` mediumint default NULL,
PRIMARY KEY (`idCliente`)
) AUTO_INCREMENT=1;
```

* Você pode pedir pro sistema exibir todas as tabelas presentes no banco de dados selecionado:
```
SHOW tables;
```

* Para obter informações sobre uma tabela, você pode usar o comando DESCRIBE ou DESC:
```
DESCRIBE clientes;
```

* Como inserir mais dados em uma tabela

   * Vamos “povoar” mais a nossa tabela com alguns dados:

```
INSERT INTO `clientes` (`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES (1,"Malesuada Inc.","Johnny Pedd",4847);
INSERT INTO `clientes` (`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES (2,"Aliquam Inc.","Al Capino",4135);
INSERT INTO `clientes` (`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES (3,"Union Carbide","Robert Ne Diro",3755);
INSERT INTO `clientes` (`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES (4,"Magna Carta Ltda.","Wenzel Dashington",3071);
INSERT INTO `clientes` (`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES (5,"Nunc Corp.","",3859);
INSERT INTO `clientes` (`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES (6,"In Company","Macaulay Bulkin",4440);
```

* Lembra que o campo idCliente foi criado com o parâmetro auto_increment. Seu preenchimento é automático. Você não precisa informar o seu valor, portanto:

```
INSERT INTO `clientes`
(`idCliente`,`nomeEmpresa`,`nomeDiretor`,`numEmpregados`)
VALUES ('',"GameCorp.","Din Viesel",2071);
```

* Como ver os registros na tabela com o comando SELECT
   * Tal como o nome sugere, o comando SELECT seleciona e exibe os registros gravados na tabela.
   * A maneira mais simples de usá-lo é essa:
```
SELECT * FROM clientes;
``` 

* Você pode refinar a pesquisa de inúmeras maneiras.
   * Se quiser ver apenas o conteúdo dos campos id_cliente e nome_empresa, use-o assim:
```
SELECT id_cliente, nome_empresa FROM clientes;
```

* Como remover um registro de uma tabela
   * A sintaxe do comando para apagar um registro é:
```
DELETE FROM nome-da-tabela WHERE nome-da-coluna=texto;
``` 

* Veja um exemplo prático de uso do comando DELETE:
```
DELETE FROM clientes WHERE nomeEmpresa = 'GameCorp';
```

* Com este comando, TODOS os registros que tiverem nomeEmpresa = 'GameCorp' serão eliminados. Neste caso, há apenas 1. Mas vamos imaginar que houvesse 10 ou 100 registros em que o nomeEmpresa fosse igual a GameCorp. Neste caso, seria necessário usar outro campo como referência para encontrar o registro que eu desejo eliminar. No nosso caso, há o campo idCliente, que é único – ele não se repete dentro da tabela:

```
DELETE FROM clientes WHERE idCliente = 7;
```

* Como remover uma tabela ou um banco de dados
   * Seja cuidadoso(a). O comando DROP apaga permanentemente uma tabela ou um banco de dados. Veja como usar o DROP para eliminar uma tabela:
```
DROP TABLE nome-da-tabela;
```
* ou, como remover um banco de dados:
```
DROP DATABASE nome-do-banco;
```
* Como limpar uma tabela
   * Para limpar uma tabela, use o comando TRUNCATE. Internamente, ele remove a tabela primeiro e, depois, a recria com a mesma estrutura – só que sem os dados. Se houver um contador AUTO_INCREMENT, na tabela em questão, ele é zerado e recolocado. Veja como funciona:
```
TRUNCATE TABLE nome-da-tabela;
```

* Como alterar um registro no MySQL
   * Aqui, o comando UPDATE entra em ação. Vamos ver como usá-lo para alterar o valor de um campo dentro de um registro:
```
UPDATE clientes SET numEmpregados=1999 WHERE idCliente = 1;
```
--- 

## COMANDOS _SHOW_,  USADO PARA CONSULTAR OS DADOS

fonte: [Boson Treinamentos](http://www.bosontreinamentos.com.br/mysql/mysql-comandos-show-describe-e-mysqlshow-39/)


* ACESSE O BANCO DE DADOS
```
mysql -u root -p
HELP SHOW;
```
* EXEMPLOS DE USO DO COMANDO _SHOW_:

* Ver os bancos de dados presentes no sistema:
```
SHOW DATABASES;
```

* Informações sobre procedimentos armazenados e funções:

```
SHOW CREATE PROCEDURE verpreço;
SHOW CREATE FUNCTION calcula_desconto;
```
* Mostrar código usado na criação de uma tabela:

```
SHOW CREATE TABLE tbl_Livro;
``` 

* Mostrar as tabelas do banco de dados atual:
```
SHOW TABLES;
```
* Ver as colunas de uma tabela:
```
SHOW [FULL] COLUMNS FROM tbl_editoras;
```

* Ver colunas com nomes específicos:
```
SHOW COLUMNS FROM tbl_Livro LIKE ‘I%’;
```

* Especificando tipos de dados:
```
SHOW COLUMNS FROM tbl_Livro WHERE Type like ‘varchar%’;
```

* Mostrar privilégios de acesso aos DBs para um usuário:
```
SHOW GRANTS FOR root@localhost;
```

## Comando DESCRIBE
fonte: [Boson Treinamentos](http://www.bosontreinamentos.com.br/mysql/mysql-comandos-show-describe-e-mysqlshow-39/)

* O comando DESCRIBE é um atalho para o comando SHOW COLUMNS FROM;
   * Exemplo:
```
DESCRIBE tbl_Livro;
```
 * O comando DESCRIBE também pode ser abreviado para:
```
DESC tbl_Livro;
```
Obs. O comando DESCRIBE não suporta as cláusulas LIKE e WHERE.

## Comando mysqlshow
fonte: [Boson Treinamentos](http://www.bosontreinamentos.com.br/mysql/mysql-comandos-show-describe-e-mysqlshow-39/)


* O comando mysqlshow opera diretamente no shell do Linux. Ele permite obter informações sobre os bancos de dados, tabelas e colunas.

```
mysqlshow -u usuário -p [banco [tabela [coluna]]]
```

* Exemplos do comando mysqlshow:

   * Ver os bancos de dados disponíveis:
```
mysqlshow -u root -p
```

* Ver as tabelas em um banco de dados específico:
```
mysqlshow -u root -p db_Biblioteca
```

* Ver os campos pertencentes a uma tabela:
```
mysqlshow -u root -p db_Biblioteca tbl_autores %
```

* Ver as tabelas com contagem de colunas e linhas, começando com uma letra específica:
```
mysqlshow -vv -u root -p db_Biblioteca ‘t*’
```

* Ver informações sobre uma coluna específica em uma tabela:
```
mysqlshow -u root -p db_Biblioteca tbl_autores ID_autor
```

Obs.: Usamos % no final do comando para que o shell não interprete tbl_autores como wildcard, e sim como o parâmetro tabela; esse problema ocorre quando temos o caractere underline (_) no nome da tabela.


## COMANDOS RELACIONADOS A SERVIÇOS
fonte: meus arquivos

* Instalar o MySQL
```
sudo apt-get install mysql-server
```

* Iniciar o MYSQL
```
sudo /etc/init.d/mysql start
```

* Parar o MySQL
```
sudo /etc/init.d/mysql stop
```

* Para reiniciar o MySQL
```
sudo /etc/init.d/mysql restart
```

* Para checar o status do MySQL
```
sudo /etc/init.d/mysql status
```

* Apache
```
sudo /etc/init.d/apache2 stop
```
