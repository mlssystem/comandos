# Comandos básicos Linux, MySQL, vi, MariaDB 

# [_MySQL_]()

## COMANDOS RELACIONADOS AO USUÁRIO
* CRIANDO USUARIO
```
MariaDB [(none)]> CREATE USER 'mlssystem'@'localhost' IDENTIFIED BY 'senha'
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

### Comando mysqlshow

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
]
Obs.: Usamos % no final do comando para que o shell não interprete tbl_autores como wildcard, e sim como o parâmetro tabela; esse problema ocorre quando temos o caractere underline (_) no nome da tabela.


# COMANDOS RELACIONADOS A SERVIÇOS
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
