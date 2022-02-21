# PRIMEIROS PASSOS PÓS INSTALAÇÃO SERVIDOR DEBIAN-11-BULLSEYE


## ATUALIZAR DEBIAN
Logar como administrador root do sistema
```
su -
apt update

```


# INSTALAR O SUDO
```

apt install sudo

```


## INCLUIR USUÁRIO AO GRUPO SUDO

### Acessar arquivo sudoers
```

nano /etc/sudoers

```


### Incuindo usuário
Abaixo da linha de comando "root ALL=(ALL:ALL) ALL"
Acrascetar o comando abaixo
```

marcus ALL=(ALL:ALL) ALL

```


# INSTALAR O RCCONF
```

sudo apt install rcconf

```


# INSTALAR APACHE2
```

apt install apache2 -y

```


## VERIFICANDO STATUS
```

systemctl status apache

```


## VERIFICAR O NÚMERO DO IP
```

ip a

```
Com o navegador aberto cole o número do **ip** e se tiver tudo **ok** aparecerá uma página com informações do Apache2


## ATUALIZAR DEBIAN
```

apt update

```


# INSTALAR MARIADB-SERVER
```

apt install mariadb-server -y

```


# INSTALAR MARIADB-CLIENT
```

apt install mariadb-client -y

```


## ATUALIZAR DEBIAN
```

apt update

```


# CONFIGURANDO MYSQL
```

sudo mysql_secure_installation

```
Apertar enter após digitar o comando acima, e depois de **CRIAR UMA SENHA FORTE PARA ROOT** é só digitar 'Y' para as outras opções.


# CRIANDO USUÁRIO
```

create user 'novo_usuario'@'localhost' identified by 'senha';

```


## CONCEDENDO PRIVILEGIOS AO NOVO_USUARIO 
O comando abaixo * . * dará permissão ao 'novo_usuario' para criar, e modificar; todos bancos de dados, e tabelas do localhost. 
```

grant all privileges on * . * to 'novo_usuario'@'localhost';

```


## ATUALIZANDO PRIVILÉGIOS
```

flush privileges;

```


# CRIANDO BANCO DE DADOS 'cadastro_produtos'
```

create database cadastro_produtos;

```


## SELECIONANDO BANCO 'cadastro_produtos'
Precisa selecionar o banco de dados desejado para poder criar tabelas para o mesmo
```

use cadastro_produtos;

```


# CRIANDO TABELA 'produtos'
```

create table produtos (id int not null auto_increment, codigo int, descricao varchar(50), preco double, categoria varchar(20), primary key (id) );

```


## ATUALIZAR DEBIAN
```

sudo apt update

```

# INSTALAR PHP
```

sudo apt install php -y

```

## CRIAR ARQRUIVO 'info.php'
Com o comando abaixo acesse o local do diretório para criar o arquivo php
```

sudo nano /var/www/html/info.php

``` 

### Copie e cole o código abaixo no arquivo 'info.php' que você criou no comando acima
```

<?php
phpinfo();
?>

```

Com o navegador aberto cole o número do **ip/info.php** e se tiver tudo **ok** aparecerá uma página com informações do **PHP**


## ATUALIZAR DEBIAN
```

sudo apt update

```


# INSTALAR PHPMYADMIN
```

sudo apt install phpmyadmin -Y

```
Quando abrir janela de configuração; selecione **apache** e **ok**

Caso tenha configuando o mysql como descrito acima (criando banco de dados, usuário, e tabela), selecionar <não> na janela  dbconfig-common. Se não configurou selecione opção <sim>, e crie uma senha para usar quando acessar no navegador seu **ip/phmyadmin**. Obs: Login será phpmyadmin e a senha a que você criou.

Se você selecionou a opção <não> é só acessar **ip/phpmyadmin** com seu login e senha e terá total acesso para criar, aletar, e usar com todos os privilégios.


# CONFIGURANDO SSH


## ATUALIZAR O DEBIAN
```

$ sudo apt update

```


## VERIFICAR O STATUS DO SSH
```

$ systemctl status ssh

```

### Se necessário inicie o ssh
```

sudo systemctl start ssh

```

### Se necessário habilite
```

sudo systemctl enable ssh

```


# REGERANDO AS CHAVES DO SERVIDOR
```

$ sudo rm /etc/ssh/ssh_host_*
sudo dpkg-reconfigure openssh-server

```


## REICICIANDO SERVIÇOS DO APACHE2
```

$ sudo systemctl restart apache2.service


```


# COPIANDO CHAVES SSH DA ESTAÇÃO DE TRABALHO PARA O DEBIAN 11


## GERANDO CHAVE SSH
```

$ ssh-keygen

```


## TESTANDO CONEXÃO
```

$ ping -c 2 ip

```


## COPIANDO CHAVA PARA SEU LOCAL DE TRABALHO
```

$ ssh-copy-id usuario@ip

```


## VERIFICANDO
```

$ ssh usuario@ip

```


## NEGANDO ACESSO COM SENHA AO ROOT PERMITINDO LOGAR SÓ COM A CHAVE PRIVADA
```

$ sudo vim /etc/ssh/sshd_config
PermitRootLogin prohibit-password

```


## PRECISA ATRIBUIR A CHAVE AO ROOT (!IMPORTANT)
```

ssh-copy-id root@ip

```


## REINICIANDO SSH
```

sudo systemctl restart ssh

```


## TESTANDO 
```

$ ssh ip

```

Paz!!!