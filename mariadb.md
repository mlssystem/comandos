# Instalando e configurando MariaDB no Debian 9
Posted by [Eriberto](https://eriberto.pro.br/blog/2018/09/04/instalando-e-configurando-mariadb-no-debian-9/)

O SGDB MariaDB é um fork do MySQL, feito pelo mesmo autor deste, após a sua aquisição pela Oracle. Neste post, veremos como se faz a instalação e a configuração básica do mesmo no Debian Stretch. Antigamente, bastava instalar o MySQL via APT, fornecendo uma senha de administrador durante tal instalação. Hoje em dia, alguns passos extras são necessários.

## A instalação

A instalação do MariaDB poderá ser feita com o comando:
```
apt-get install mariadb-server
```
Com isso, o serviço será instalado e nenhuma pergunta será feita. No caso deste post, foi instalada a versão 10.1.26. Uma configuração básica será necessária para o seu uso inicial.

## A configuração básica

O primeiro passo da configuração básica será fazer os ajustes iniciais no MariaDB. Para isso, execute o comando:
```
mysql_secure_installation
```
A não ser que você saiba o que está fazendo, responda às perguntas da seguinte forma:
```
Enter current password for root (enter for none): pressione Enter.
Set root password? [Y/n]: pressione Enter.
New password: digite uma senha forte para o ser usada pelo root do MariaDB.
Remove anonymous users? [Y/n]: pressione Enter.
Disallow root login remotely? [Y/n]: responda de acordo com a sua necessidade. A melhor resposta, caso não saiba o que fazer, será Y.
Remove test database and access to it? [Y/n]: pressione Enter.
Reload privilege tables now? [Y/n]: pressione Enter.
Agora, tente entrar no SGDB via linha de comando:
```
No ternminal como root digitar a linha de comando abaixo:
```
mariadb -u root -p
```
**Se tudo deu certo, você entrará no sistema e receberá um prompt, depois de um texto inicial.Veja:**

1. Welcome to the MariaDB monitor. Commands end with ; or \g.
1. Your MariaDB connection id is 10
1. Server version: 10.1.26-MariaDB-0+deb9u1 Debian 9.1
1. Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.
1. Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
Para sair do ambiente do SGDB, digite quit.

## Possíveis erros e soluções

* Existe a possibilidade de ocorrerem alguns erros no momento do acesso do banco de dados por aplicações, como o phpmyadmin. O principal deles é o #1698. Veremos a seguir como resolver esse problema.
```
1698 – Access denied for user ‘root’@’localhost’
```

* Para sanar esse erro, execute os seguintes comandos:

**No termina digite:**
```
mariadb -u root -p
> use mysql;
> update user set plugin='' where User='root';
> flush privileges;
> exit
```
Vá em frente
Agora que você tem o MariaDB instalado, use-o!

Não se esqueçam que JESUS voltará para buscar todos aqueles que creem! Meditem na palavra de Jesus no evangelho de João capitulo 14.

Fiquem com Deus!

_PAZ!_

