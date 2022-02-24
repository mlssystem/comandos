# PRIMEIROS PASSOS PÓS INSTALAÇÃO SERVIDOR DEBIAN-11-BULLSEYE
Versão debian-11.2.0-amd64-netinst.iso [baixar iso do site debian.org](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.2.0-amd64-netinst.iso)

> Fiz a instalação apenas com ultilitários do sistema e SSH



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


---


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


---


# SAMBA "SOFTWARE SERVIDOR"


## INSTALAR O SAMBA
```

# apt-get install samba -y

```


## CONFIGURAR DO SAMBA
Logar com privilégios root
Recomendado fazer o backup do arquivo a ser alterado
```

nano /etc/samba/smb.conf

```


## CRIAR O DIRETÓRIO A SER COMPARTILHADO
E conceder todos privilégios para todos
```

mkdir /home/nome_diretorio && chmod 777 /nome_diretorio

```

## NO FINAL DO ARQUIVO SMB.CONF, ADICIONE A CONFIGURAÇÃO 
```
Nome do diretório criado para ser compartilhado entre Windows e Debian e vice-versa
[nome_diretorio]

local arquivos
path = /home/nome_diretorio

Todos podem acessar o conteúdo compartilhado
public = yes

Deixando visivel na rede
browseable = yes

Permitindo escrita
writeable = yes

Impedindo apenas leitura
read only = no

Máscara que os arquivos serão criados
create mask = 0700

Máscara que os diretórios serão criados
directory mask = 0700
```


## REINICIAR O SAMBA
```

/etc/init.d/smbd restart
ou
systemctl restart smbd
systemctl restart nmbd

```

> Na barra de endereço do Explorador de arquivos do Windows é só digita o IP donde instalou o **SAMBA** 
> Depois de duas barras invertidas ' \\ '

Exemplo:
\\ numero_do_ip


# INSTALANDO UFW - FIREWALL
```

sudo apt install firewall

```

Alguns comando básico
```
sudo ufw status
sudo ufw app list
sudo ufw enable
sudo ufw reload
```


---


# PREPARANDO PARA INSTALAR WORDPRESS NO SERVIDOR DEBIAN-11


## PRÉ-REQUISITOS
Para concluir este tutorial, você precisará ter acesso a um servidor Debian 10/11.

Você precisará executar as seguintes tarefas antes de iniciar este guia:

* Criar um usuário sudo em seu servidor: Concluiremos as etapas deste guia usando um usuário não-root com privilégios sudo. Você pode criar um usuário com privilégios sudo seguindo nosso guia Debian 10 initial server setup.
* Instalar a pilha LAMP: O WordPress precisará de um servidor web, um banco de dados e o PHP para funcionar corretamente. A configuração de uma pilha LAMP (Linux, Apache, MariaDB e PHP) atende a todos esses requisitos. Siga este guia para instalar e configurar este software.
* Proteger seu site com SSL: o Wordpress fornece conteúdo dinâmico e cuida da autenticação e autorização do usuário. O protocolo TLS/SSL é a tecnologia que lhe permite criptografar o tráfego do seu site para que sua conexão esteja segura. A maneira como você irá configurar o SSL dependerá se você tem um nome de domínio para seu site.
 * Se você tiver um nome de domínio… a maneira mais fácil de proteger seu site é com o Let’s Encrypt, que oferece certificados confiáveis e gratuitos. Siga nosso guia do Let’s Encrypt para o Apache para configurar isto.
 * Se você não tiver um domínio… e você está usando essa configuração apenas para teste ou uso pessoal, pode usar um certificado autoassinado. Isso fornece o mesmo tipo de criptografia, mas sem a validação do domínio. Siga nosso guia de SSL autoassinado para o Apache para configurar isto.


# PASSO 1 — CRIANDO O CERTIFICADO SSL
https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-debian-10

O TLS/SSL funciona usando uma combinação de um certificado público e uma chave privada. A chave SSL é mantida em segredo no servidor. Ele é usado para criptografar o conteúdo enviado aos clientes. O certificado SSL é compartilhado publicamente com qualquer pessoa que solicite o conteúdo. Ele pode ser usado para descriptografar o conteúdo assinado pela chave SSL associada.

Podemos criar uma chave autoassinada e um par de certificados com OpenSSL em um único comando:
```

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

```

1. **openssl** : Esta é a ferramenta básica de linha de comando para criar e gerenciar certificados OpenSSL, chaves e outros arquivos.

2. **req** : Este subcomando especifica que queremos usar o gerenciamento de solicitação de assinatura de certificado (CSR) X.509. O “X.509” é um padrão de infraestrutura de chave pública ao qual SSL e TLS aderem para seu gerenciamento de chave e certificado. Queremos criar um novo certificado X.509, então estamos usando este subcomando.

3. **-x509** : Isso modifica ainda mais o subcomando anterior, informando ao utilitário que queremos fazer um certificado autoassinado em vez de gerar uma solicitação de assinatura de certificado, como normalmente aconteceria.

4. **-nodes** : Isso diz ao OpenSSL para pular a opção de proteger nosso certificado com uma senha. Precisamos que o Apache seja capaz de ler o arquivo, sem intervenção do usuário, quando o servidor for inicializado. Uma senha impediria que isso acontecesse porque teríamos que inseri-la após cada reinicialização.

5. **-days 365** : Esta opção define o período de tempo que o certificado será considerado válido. Nós definimos isso para um ano aqui.

6. **-newkey rsa:2048** : Especifica que queremos gerar um novo certificado e uma nova chave ao mesmo tempo. Não criamos a chave necessária para assinar o certificado em uma etapa anterior, portanto, precisamos criá-la junto com o certificado. A rsa:2048 parte diz para fazer uma chave RSA com 2048 bits.

7. **-keyout** : Esta linha informa ao OpenSSL onde colocar o arquivo de chave privada gerado que estamos criando.

8. **-out** : Isso informa ao OpenSSL onde colocar o certificado que estamos criando.

Como afirmamos acima, essas opções criarão um arquivo de chave e um certificado. Serão feitas algumas perguntas sobre nosso servidor para incorporar as informações corretamente no certificado.

Preencha os prompts adequadamente. **A linha mais importante é aquela que solicita o arquivo Common Name (e.g. server FQDN or YOUR name). Você precisa inserir o nome de domínio associado ao seu servidor ou, mais provavelmente, o endereço IP público do seu servidor**.

A totalidade dos prompts será algo como isto:
```
Output
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:New York
Locality Name (eg, city) []:New York City
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Bouncy Castles, Inc.
Organizational Unit Name (eg, section) []:Ministry of Water Slides
Common Name (e.g. server FQDN or YOUR name) []:server_IP_address
Email Address []:admin@your_domain.com
```

Ambos os arquivos que você criou serão colocados nos subdiretórios apropriados em ```/etc/ssl```.


# ETAPA 2 — CONFIGURANDO O APACHE PARA USAR SSL
Criamos nossos arquivos de chave e certificado no ```/etc/ssl``` diretório. Agora só precisamos modificar nossa configuração do Apache para tirar proveito disso.

Faremos alguns ajustes em nossa configuração:

1. Criaremos um snippet de configuração para especificar configurações de SSL padrão fortes.

2. Modificaremos o arquivo SSL Apache Virtual Host incluído para apontar para nossos certificados SSL gerados.

3. (Recomendado) Modificaremos o arquivo de Host Virtual não criptografado para redirecionar automaticamente as solicitações para o Host Virtual criptografado.

Quando terminarmos, devemos ter uma configuração SSL segura.


## CRIANDO UM SNIPPET DE CONFIGURAÇÃO DO APACHE COM CONFIGURAÇÕES DE CRIPTOGRAFIA FORTES
Primeiro, criaremos um trecho de configuração do Apache para definir algumas configurações de SSL. Isso configurará o Apache com um conjunto de criptografia SSL forte e habilitará alguns recursos avançados que ajudarão a manter nosso servidor seguro. Os parâmetros que definiremos podem ser usados por qualquer Host Virtual habilitando SSL.

Crie um novo snippet no ```/etc/apache2/conf-available``` diretório. Vamos nomear o arquivo ```ssl-params.conf``` para deixar claro seu propósito:
```

sudo nano /etc/apache2/conf-available/ssl-params.conf

```

Para configurar o Apache SSL com segurança, usaremos as recomendações de Remy van Elst no site Cipherli.st . Este site foi projetado para fornecer configurações de criptografia fáceis de usar para softwares populares.

> As configurações sugeridas no site do link acima oferecem segurança forte. Às vezes, isso tem o custo de uma maior compatibilidade do cliente. Se você precisar dar suporte a clientes mais antigos, há uma lista alternativa que pode ser acessada clicando no link na página chamada “Sim, me dê um ciphersuite que funcione com software legado/antigo”. Essa lista pode ser substituída pelos itens copiados abaixo.

> A escolha de qual configuração você usa dependerá em grande parte do que você precisa suportar. Ambos fornecerão grande segurança.

Para nossos propósitos, podemos copiar as configurações fornecidas em sua totalidade. Faremos apenas uma pequena alteração e desativaremos o ```Strict-Transport-Security``` cabeçalho (HSTS).

O pré-carregamento do HSTS oferece maior segurança, mas pode ter consequências de longo alcance se ativado acidentalmente ou incorretamente. Neste guia, não habilitaremos as configurações, mas você poderá modificá-las se tiver certeza de que compreende as implicações.

Antes de decidir, reserve um momento para ler sobre HTTP Strict Transport Security, ou HSTS , e especificamente sobre a funcionalidade de “pré-carregamento” .

Cole a seguinte configuração no ```ssl-params.conf``` arquivo que abrimos:

```/etc/apache2/conf-available/ssl-params.conf```
```
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLHonorCipherOrder On
# Disable preloading HSTS for now.  You can use the commented out header line that includes
# the "preload" directive if you understand the implications.
# Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
# Requires Apache >= 2.4
SSLCompression off
SSLUseStapling on
SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
# Requires Apache >= 2.4.11
SSLSessionTickets Off
```
Salve e feche o arquivo quando terminar.

## MODIFICANDO O ARQUIVO DE HOST VIRTUAL APACHE SSL PADRÃO
Em seguida, vamos modificar ```/etc/apache2/sites-available/default-ssl.conf```, o arquivo padrão do Apache SSL Virtual Host. Se você estiver usando um arquivo de bloco de servidor diferente, substitua seu nome nos comandos abaixo.

Antes de prosseguirmos, vamos fazer backup do arquivo SSL Virtual Host original:
```

sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.bak

```

Dentro, com a maioria dos comentários removidos, o bloco Virtual Host deve ficar assim por padrão:
```
/etc/apache2/sites-available/default-ssl.conf
```
```
<IfModule mod_ssl.c>
        <VirtualHost _default_:443>
                ServerAdmin webmaster@localhost

                DocumentRoot /var/www/html

                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined

                SSLEngine on

                SSLCertificateFile      /etc/ssl/certs/ssl-cert-snakeoil.pem
                SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key

                <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                SSLOptions +StdEnvVars
                </FilesMatch>
                <Directory /usr/lib/cgi-bin>
                                SSLOptions +StdEnvVars
                </Directory>

        </VirtualHost>
</IfModule>
```

Faremos alguns pequenos ajustes no arquivo. Definiremos as coisas normais que gostaríamos de ajustar em um arquivo de Host Virtual (endereço de e-mail ServerAdmin, ServerName, etc.) e ajustaremos as diretivas SSL para apontar para nossos arquivos de certificado e chave. Novamente, se você estiver usando uma raiz de documento diferente, certifique-se de atualizar a ```DocumentRoot``` diretiva.

Depois de fazer essas alterações, seu bloco de servidor deve ser semelhante a este:
```

/etc/apache2/sites-available/default-ssl.conf

```
```
<IfModule mod_ssl.c>
        <VirtualHost _default_:443>
                ServerAdmin your_email@example.com
                ServerName server_domain_or_IP

                DocumentRoot /var/www/html

                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined

                SSLEngine on

                SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt
                SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

                <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                SSLOptions +StdEnvVars
                </FilesMatch>
                <Directory /usr/lib/cgi-bin>
                                SSLOptions +StdEnvVars
                </Directory>

        </VirtualHost>
</IfModule>
```

Salve e feche o arquivo quando terminar.

## (RECOMENDADO) MODIFICANDO O ARQUIVO DE HOST HTTP PARA REDIRECIONAR PARA HTTPS
Como está agora, o servidor fornecerá tráfego HTTP não criptografado e HTTPS criptografado. Para maior segurança, é recomendado na maioria dos casos redirecionar HTTP para HTTPS automaticamente. Se você não deseja ou precisa dessa funcionalidade, pode pular esta seção com segurança.

Para ajustar o arquivo de Host Virtual não criptografado para redirecionar todo o tráfego para ser criptografado por SSL, abra o ```/etc/apache2/sites-available/000-default.conf``` arquivo:
```

sudo nano /etc/apache2/sites-available/000-default.conf

```

Dentro dos ```VirtualHost``` blocos de configuração, adicione uma Redirect diretiva, apontando todo o tráfego para a versão SSL do site:
```
/etc/apache2/sites-available/000-default.conf
```
```
<VirtualHost *:80>
        . . .

        Redirect "/" "https://your_domain_or_IP/"

        . . .
</VirtualHost>
```

Salve e feche o arquivo quando terminar.

Essas são todas as alterações de configuração que você precisa fazer no Apache. Em seguida, discutiremos como atualizar as regras de firewall ```ufw``` para permitir o tráfego HTTPS criptografado para o seu servidor.


---


# PASSO 3 — AJUSTANDO O FIREWALL
Se você tiver o ```ufw``` firewall ativado, conforme recomendado pelos guias de pré-requisitos, talvez seja necessário ajustar as configurações para permitir o tráfego SSL. Felizmente, quando instalado no Debian 10, ```ufw``` vem carregado com perfis de aplicativos que você pode usar para ajustar suas configurações de firewall

Podemos ver os perfis disponíveis digitando:
```

sudo ufw app list

```

Você deve ver uma lista como esta, com os quatro perfis a seguir na parte inferior da saída:
Output
```
Available applications:
. . .
  WWW
  WWW Cache
  WWW Full
  WWW Secure
. . .
```

Você pode ver a configuração atual digitando:
```

sudo ufw status

```

Se você permitiu apenas tráfego HTTP regular anteriormente, sua saída pode ter esta aparência:
```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
WWW                        ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
WWW (v6)                   ALLOW       Anywhere (v6)
```

Para permitir adicionalmente o tráfego HTTPS, permita o perfil “WWW Full” e, em seguida, exclua a permissão do perfil “WWW” redundante:
```

sudo ufw allow 'WWW Full'
sudo ufw delete allow 'WWW'

```

Seu status deve ficar assim agora:
```

sudo ufw status

```
Output
```
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
WWW Full                   ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
WWW Full (v6)              ALLOW       Anywhere (v6)
```

Com seu firewall configurado para permitir tráfego HTTPS, você pode passar para a próxima etapa, onde veremos como habilitar alguns módulos e arquivos de configuração para permitir que o SSL funcione corretamente.


# PASSO 4 — HABILITANDO AS MUDANÇAS NO APACHE
Agora que fizemos nossas alterações e ajustamos nosso firewall, podemos habilitar os módulos SSL e de cabeçalhos no Apache, habilitar nosso Virtual Host pronto para SSL e reiniciar o Apache para colocar essas alterações em vigor.

Habilite mod_ssl, o módulo Apache SSL, e mod_headers, que é necessário para algumas das configurações em nosso trecho de SSL, com o a2enmodcomando:
```
sudo a2enmod ssl
sudo a2enmod headers

```

Em seguida, habilite seu Host Virtual SSL com o a2ensitecomando:
```

sudo a2ensite default-ssl

```

Você também precisará habilitar seu ```ssl-params.conf``` arquivo, para ler os valores que você definiu:
```

sudo a2enconf ssl-params

```

Neste ponto, o site e os módulos necessários estão habilitados. Devemos verificar se não há erros de sintaxe em nossos arquivos. Faça isso digitando:
```

sudo apache2ctl configtest

```

Se tudo for bem-sucedido, você obterá um resultado semelhante a este:

Output
```
Syntax OK
```

Contanto que sua saída esteja Syntax OKnele, seu arquivo de configuração não terá erros de sintaxe e você poderá reiniciar o Apache com segurança para implementar as alterações:
```

sudo systemctl restart apache2

```
Com isso, seu certificado SSL auto assinado está pronto. Agora você pode testar se seu servidor está criptografando corretamente seu tráfego.


# ETAPA 5 — TESTANDO A CRIPTOGRAFIA
Agora você está pronto para testar seu servidor SSL.

Abra seu navegador da web e digite https://seguido pelo nome de domínio ou IP do seu servidor na barra de endereços:
```
https://server_domain_or_IP
```

Como o certificado que você criou não é assinado por uma das autoridades de certificação confiáveis do seu navegador, você provavelmente verá um aviso assustador como o abaixo:
[imagem](https://assets.digitalocean.com/articles/apache_ssl_1604/self_signed_warning.png)

Isso é esperado e normal. Estamos interessados apenas no aspecto de criptografia de nosso certificado, não na validação de terceiros da autenticidade de nosso host. Clique em **AVANÇADO** e, em seguida, no link fornecido para prosseguir para o seu host de qualquer maneira:
[imagem](https://assets.digitalocean.com/articles/apache_ssl_1604/warning_override.png)

Você deve ser levado ao seu site. Se você olhar na barra de endereços do navegador, verá um cadeado com um “x” sobre ele ou outro aviso semelhante “não seguro”. Nesse caso, isso significa apenas que o certificado não pode ser validado. Ele ainda está criptografando sua conexão.

Se você configurou o Apache para redirecionar HTTP para HTTPS, você também pode verificar se o redirecionamento funciona corretamente:
```
http://server_domain_or_IP
```

Se isso resultar no mesmo ícone, isso significa que seu redirecionamento funcionou corretamente. No entanto, o redirecionamento que você criou anteriormente é apenas um redirecionamento temporário. Se você quiser tornar o redirecionamento para HTTPS permanente, vá para a etapa final.


# PASSO 6 — MUDANDO PARA UM REDIRECIONAMENTO PERMANENTE
Se o redirecionamento funcionou corretamente e você tem certeza de que deseja permitir apenas tráfego criptografado, modifique novamente o Apache Virtual Host não criptografado para tornar o redirecionamento permanente.

Abra o arquivo de configuração do bloco do servidor novamente:
```

sudo nano /etc/apache2/sites-available/000-default.conf

```

Encontre a ```Redirect``` linha que adicionamos anteriormente. Adicione ```permanent``` a essa linha, que altera o redirecionamento de um redirecionamento temporário 302 para um redirecionamento 301 permanente:
```

/etc/apache2/sites-available/000-default.conf

```
```
<VirtualHost *:80>
        . . .

        Redirect permanent "/" "https://your_domain_or_IP/"

        . . .
</VirtualHost>
```

Salve e feche o arquivo.

Verifique sua configuração quanto a erros de sintaxe:
```

sudo apache2ctl configtest

```

Se este comando não relatar nenhum erro de sintaxe, reinicie o Apache:
```

sudo systemctl restart apache2

```

Isso tornará o redirecionamento permanente e seu site servirá apenas tráfego por HTTPS.

# CONCLUSÃO
Você configurou seu servidor Apache para usar criptografia forte para conexões de clientes. Isso permitirá que você atenda solicitações com segurança e impedirá que terceiros leiam seu tráfego.

---

# COMO INSTALAR O WORDPRESS COM LAMP NO DEBIAN 10
https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lamp-on-debian-10-pt
WordPressLAMP Stack Debian 10 - By Published on April 13, 2020


## INTRODUÇÃO
O WordPress é o CMS (sistema de gerenciamento de conteúdos) mais popular na Internet. Ele permite que você configure blogs e sites flexíveis com facilidade, em cima de um back-end em MariaDB com processamento em PHP. A adoção do WordPress teve um crescimento incrível, sendo uma ótima escolha para se colocar um website em funcionamento de maneira rápida. Após a configuração, quase toda a administração pode ser feita através do front-end web.

Neste guia, focaremos em configurar uma instância do WordPress em uma pilha LAMP (Linux, Apache, MariaDB e PHP) em um servidor Debian 10.


## PRÉ-REQUISITOS
Para concluir este tutorial, você precisará ter acesso a um servidor Debian 10.

Você precisará executar as seguintes tarefas antes de iniciar este guia:

* Criar um usuário sudo em seu servidor: Concluiremos as etapas deste guia usando um usuário não-root com privilégios sudo. Você pode criar um usuário com privilégios sudo seguindo nosso guia Debian 10 initial server setup.
* Instalar a pilha LAMP: O WordPress precisará de um servidor web, um banco de dados e o PHP para funcionar corretamente. A configuração de uma pilha LAMP (Linux, Apache, MariaDB e PHP) atende a todos esses requisitos. Siga este guia para instalar e configurar este software.
* Proteger seu site com SSL: o Wordpress fornece conteúdo dinâmico e cuida da autenticação e autorização do usuário. O protocolo TLS/SSL é a tecnologia que lhe permite criptografar o tráfego do seu site para que sua conexão esteja segura. A maneira como você irá configurar o SSL dependerá se você tem um nome de domínio para seu site.
 * Se você tiver um nome de domínio… a maneira mais fácil de proteger seu site é com o Let’s Encrypt, que oferece certificados confiáveis e gratuitos. Siga nosso guia do Let’s Encrypt para o Apache para configurar isto.
 * Se você não tiver um domínio… e você está usando essa configuração apenas para teste ou uso pessoal, pode usar um certificado autoassinado. Isso fornece o mesmo tipo de criptografia, mas sem a validação do domínio. Siga nosso guia de SSL autoassinado para o Apache para configurar isto.
Quando você terminar os passos de configuração, efetue login no seu servidor como seu usuário sudo e continue abaixo.


# PASSO 1 — CRIANDO UM BANCO DE DADOS MARIADB E UM USUÁRIO PARA O WORDPRESS
O primeiro passo que daremos é preparatório. O WordPress requer um banco de dados baseado em MySQL para armazenar e gerenciar informações do site e de usuário. Temos o MariaDB — um substituto para o MySQL — já instalado, mas precisamos criar um banco de dados e um usuário para o WordPress usar.

Para começar, abra o prompt do MariaDB como a conta root:
```

sudo mariadb

```
Nota: Se você configurou outra conta com privilégios administrativos ao instalar e configurar o MariaDB, você também poderá efetuar login como esse usuário. Você precisará fazer isso com o seguinte comando:
```

mariadb -u nome_do_usuário -p

```

Após executar este comando, o MariaDB solicitará a senha que você definiu para essa conta.

Comece criando um novo banco de dados que o WordPress irá controlar. Você pode chamar isso do que quiser, mas para simplificar para este guia, iremos chamá-lo de wordpress.

Crie o banco de dados para o Wordpress digitando:
```

CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;

```

Note que todo comando MySQL deve terminar em ponto e vírgula (;). Verifique se isso está presente, caso você estiver enfrentando algum problema.

Em seguida, crie uma conta de usuário MySQL separada que usaremos exclusivamente para operar em nosso novo banco de dados. Criar bancos de dados e contas de função única é uma boa ideia do ponto de vista de gerenciamento e segurança. Usaremos o nome wordpress_user neste guia, mas fique à vontade para alterar isso, se desejar.

Crie esta conta, defina uma senha e conceda ao usuário acesso ao banco de dados que você acabou de criar com o seguinte comando. Lembre-se de escolher uma senha forte para o usuário do banco de dados:
```

GRANT ALL ON wordpress.* TO 'wordpress_user'@'localhost' IDENTIFIED BY 'senha';

```

Agora você tem um banco de dados e uma conta de usuário, cada um feito especificamente para o WordPress. Execute o seguinte comando para recarregar as tabelas de concessão, para que a instância atual do MariaDB saiba sobre as alterações que você fez:
```

FLUSH PRIVILEGES;

```

Saia do MariaDB digitando
```

EXIT;

```

Agora que você configurou o banco de dados e o usuário que serão usados pelo WordPress, você pode instalar alguns pacotes relacionados ao PHP usados pelo CMS.


# PASSO 2 — INSTALANDO EXTENSÕES ADICIONAIS DO PHP
Ao configurar nossa pilha LAMP, exigimos apenas um conjunto mínimo de configurações para que o PHP se comunique com o MariaDB. O WordPress e muitos de seus plugins utilizam extensões adicionais do PHP.

Baixe e instale algumas das extensões PHP mais populares para uso com o WordPress digitando:
```

sudo apt update
sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip

```

Nota: Cada plugin do WordPress tem seu próprio conjunto de requisitos. Alguns podem exigir a instalação de pacotes PHP adicionais. Verifique a documentação do seu plugin para encontrar os requisitos de PHP. Se estiverem disponíveis, eles podem ser instalados com o apt como demonstrado acima.

Reiniciaremos o Apache para carregar essas novas extensões na próxima seção. Se você estiver retornando aqui para instalar plug-ins adicionais, poderá reiniciar o Apache agora, digitando:
```

sudo systemctl restart apache2

```

Neste ponto, tudo o que resta antes de instalar o WordPress é fazer algumas alterações na configuração do Apache para permitir que o CMS funcione sem problemas.


# PASSO 3 - AJUSTANDO A CONFIGURAÇÃO DO APACHE PARA PERMITIR SOBREPOSIÇÕES E REESCRITAS NO .HTACCESS
Com as extensões PHP adicionais instaladas e prontas para uso, a próxima coisa a fazer é fazer algumas alterações na sua configuração do Apache. Com base nos tutoriais de pré-requisito, você deve ter um arquivo de configuração para o seu site no diretório /etc/apache2/sites-available/. Usaremos /etc/apache2/sites-available/wordpress.conf como exemplo aqui, mas você deve substituir o caminho para o seu arquivo de configuração, quando apropriado.

Além disso, usaremos /var/www/wordpress como o diretório raiz ou o web root da nossa instalação do WordPress. Você deve usar o web root especificado em sua própria configuração.

> Nota: É possível que você esteja usando a configuração padrão 000-default.conf (com /var/www/html como seu web root). Isso é bom de usar se você estiver hospedando apenas um site neste servidor. Caso contrário, é melhor dividir a configuração necessária em partes lógicas, um arquivo por site.

Atualmente, o uso de arquivos .htaccess está desativado. O WordPress e muitos plugins do WordPress usam esses arquivos extensivamente para ajustes em diretório no comportamento do servidor web.

Abra o arquivo de configuração do Apache para o seu site. Observe que, se você já possui um arquivo de configuração do Apache para o seu site, o nome desse arquivo será diferente:
```

sudo nano /etc/apache2/sites-available/wordpress.conf

```

Para permitir arquivos .htaccess, você precisará adicionar um bloco Directory apontando para o seu document root com uma diretiva AllowOverride dentro dele. Adicione o seguinte bloco de texto dentro do bloco VirtualHost no seu arquivo de configuração, certificando-se de usar o diretório web root correto:
```

/etc/apache2/sites-available/wordpress.conf
<Directory /var/www/wordpress/>
        AllowOverride All
</Directory>

```

Quando terminar, salve e feche o arquivo.

Em seguida, ative o módulo rewrite para utilizar o recurso de link permanente ou permalink do WordPress:
```

sudo a2enmod rewrite

```

Antes de implementar as alterações que você fez, verifique se você não cometeu nenhum erro de sintaxe:
```

sudo apache2ctl configtest

```

Se a sintaxe do seu arquivo de configuração estiver correta, você verá o seguinte em sua saída:
```
Output
Syntax OK
```

Se este comando relatar algum erro, volte e verifique se você não cometeu nenhum erro de sintaxe no seu arquivo de configuração. Caso contrário, reinicie o Apache para implementar as alterações:
```

sudo systemctl restart apache2

```

Em seguida, baixaremos e configuraremos o próprio WordPress.


# PASSO 4 — BAIXANDO O WORDPRESS
Agora que o software do servidor está configurado, você pode baixar e configurar o WordPress. Por motivos de segurança em particular, é sempre recomendável obter a versão mais recente do WordPress diretamente do site dele.

Nota: Usaremos o curl para baixar o WordPress, mas este programa pode não estar instalado por padrão no seu servidor Debian. Para instalá-lo, execute:
```

sudo apt install curl

```

Mude para um diretório gravável e faça o download da versão compactada digitando:

cd /tmp
curl -O https://wordpress.org/latest.tar.gz
Extraia o arquivo compactado para criar a estrutura de diretórios do WordPress:
```
tar xzvf latest.tar.gz
```

Vamos mover esses arquivos para o nosso document root momentaneamente. Antes, porém, adicionamos um arquivo vazio .htaccess para que este fique disponível para uso posterior do WordPress.

Crie o arquivo digitando:
```

touch /tmp/wordpress/.htaccess

```

Em seguida, copie o arquivo de configuração de amostra para o nome de arquivo que o WordPress realmente lê:
```

cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php

```

Além disso, crie o diretório upgrade para que o WordPress não tenha problemas de permissão ao tentar fazer isso sozinho após uma atualização do software:
```

mkdir /tmp/wordpress/wp-content/upgrade

```

Em seguida, copie todo o conteúdo do diretório para seu document root. Observe que o comando a seguir inclui um ponto no final do diretório de origem para indicar que tudo dentro do diretório deve ser copiado, incluindo arquivos ocultos (como o arquivo .htaccess que você criou):
```

sudo cp -a /tmp/wordpress/. /var/www/wordpress

```

Com isso, você instalou o WordPress com sucesso em seu servidor web e executou algumas das etapas de configuração inicial. Em seguida, discutiremos algumas alterações adicionais na configuração que darão ao WordPress os privilégios necessários para funcionar, além do acesso ao banco de dados MariaDB e a conta de usuário que você criou anteriormente.


# PASSO 5 — CONFIGURANDO O DIRETÓRIO DO WORDPRESS
Antes de iniciarmos o processo de configuração baseado em web do WordPress, precisamos ajustar alguns itens em nosso diretório do WordPress.

Comece dando a propriedade de todos os arquivos ao usuário e grupo www-data. Este é o usuário com o qual o servidor web Apache é executado, e o Apache precisará ler e gravar arquivos do WordPress para servir o site e executar atualizações automáticas.

Atualize a propriedade com chown:

```

sudo chown -R www-data:www-data /var/www/wordpress

```

Em seguida, executaremos dois comandos find para definir as permissões corretas nos diretórios e arquivos do WordPress:
```

sudo find /var/www/wordpress/ -type d -exec chmod 750 {} \;
sudo find /var/www/wordpress/ -type f -exec chmod 640 {} \;

```

Devem ser definidas permissões razoáveis para começar, embora alguns plug-ins e procedimentos possam exigir ajustes adicionais.

Depois disso, você precisará fazer algumas alterações no arquivo de configuração principal do WordPress.

Quando você abre o arquivo, seu primeiro objetivo será ajustar algumas chaves secretas para fornecer segurança à sua instalação. O WordPress fornece um gerador seguro para esses valores, para que você não precise criar bons valores por conta própria. Eles são usados apenas internamente, portanto, não prejudicará a usabilidade ter valores complexos e seguros aqui.

Para obter valores seguros do gerador de chave secreta do WordPress, digite:
```

curl -s https://api.wordpress.org/secret-key/1.1/salt/

```

Você receberá valores únicos parecidos com os seguintes:

Atenção! É importante que você solicite valores exclusivos a cada vez. NÃO copie os valores mostrados abaixo!

Output
```
define('AUTH_KEY',         '1jl/vqfs<XhdXoAPz9 DO NOT COPY THESE VALUES c_j{iwqD^<+c9.k<J@4H');
define('SECURE_AUTH_KEY',  'E2N-h2]Dcvp+aS/p7X DO NOT COPY THESE VALUES {Ka(f;rv?Pxf})CgLi-3');
define('LOGGED_IN_KEY',    'W(50,{W^,OPB%PB<JF DO NOT COPY THESE VALUES 2;y&,2m%3]R6DUth[;88');
define('NONCE_KEY',        'll,4UC)7ua+8<!4VM+ DO NOT COPY THESE VALUES #`DXF+[$atzM7 o^-C7g');
define('AUTH_SALT',        'koMrurzOA+|L_lG}kf DO NOT COPY THESE VALUES  07VC*Lj*lD&?3w!BT#-');
define('SECURE_AUTH_SALT', 'p32*p,]z%LZ+pAu:VY DO NOT COPY THESE VALUES C-?y+K0DK_+F|0h{!_xY');
define('LOGGED_IN_SALT',   'i^/G2W7!-1H2OQ+t$3 DO NOT COPY THESE VALUES t6**bRVFSD[Hi])-qS`|');
define('NONCE_SALT',       'Q6]U:K?j4L%Z]}h^q7 DO NOT COPY THESE VALUES 1% ^qUswWgn+6&xqHN&%');
```

Essas são as linhas de configuração que você colará diretamente no seu arquivo de configuração para definir chaves seguras. Copie a saída que você recebeu na sua área de transferência e abra o arquivo de configuração do WordPress localizado em seu document root:
```

sudo nano /var/www/wordpress/wp-config.php

```

Encontre a seção que contém os valores fictícios para essas configurações. Vai parecer algo assim:
```

/var/www/wordpress/wp-config.php

```
```
. . .

define('AUTH_KEY',         'put your unique phrase here');
define('SECURE_AUTH_KEY',  'put your unique phrase here');
define('LOGGED_IN_KEY',    'put your unique phrase here');
define('NONCE_KEY',        'put your unique phrase here');
define('AUTH_SALT',        'put your unique phrase here');
define('SECURE_AUTH_SALT', 'put your unique phrase here');
define('LOGGED_IN_SALT',   'put your unique phrase here');
define('NONCE_SALT',       'put your unique phrase here');

. . .
```
Exclua essas linhas e cole os valores copiados da linha de comando:

/var/www/wordpress/wp-config.php

```
. . .

define('AUTH_KEY',         'VALUES COPIED FROM THE COMMAND LINE');
define('SECURE_AUTH_KEY',  'VALUES COPIED FROM THE COMMAND LINE');
define('LOGGED_IN_KEY',    'VALUES COPIED FROM THE COMMAND LINE');
define('NONCE_KEY',        'VALUES COPIED FROM THE COMMAND LINE');
define('AUTH_SALT',        'VALUES COPIED FROM THE COMMAND LINE');
define('SECURE_AUTH_SALT', 'VALUES COPIED FROM THE COMMAND LINE');
define('LOGGED_IN_SALT',   'VALUES COPIED FROM THE COMMAND LINE');
define('NONCE_SALT',       'VALUES COPIED FROM THE COMMAND LINE');

. . .
```

Em seguida, modifique as configurações de conexão do banco de dados na parte superior do arquivo. Você precisa ajustar o nome do banco de dados, o usuário do banco de dados e a senha associada que você configurou no MariaDB.

A outra alteração que você deve fazer é definir o método que o WordPress deve usar para gravar no sistema de arquivos. Como concedemos ao servidor web permissão para gravar onde ele precisar, podemos definir explicitamente o método do sistema de arquivos como “direct”. Se você não definir isso com nossas configurações atuais, o WordPress solicitará credenciais de FTP quando você executar determinadas ações.

Essa configuração pode ser adicionada abaixo das configurações de conexão com o banco de dados ou em qualquer outro local do arquivo:
```
/var/www/wordpress/wp-config.php

```
```
. . .

define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'wordpress_user');

/** MySQL database password */
define('DB_PASSWORD', 'senha');

. . .

define('FS_METHOD', 'direct');
```

Salve e feche o arquivo quando terminar. Finalmente, você pode concluir a instalação e a configuração do WordPress acessando-o através do seu navegador.

# PASSO 6 — COMPLETANDO A INSTALAÇÃO ATRAVÉS DA INTERFACE WEB
Agora que a configuração do servidor está concluída, podemos concluir a instalação através da interface web.

No seu navegador, navegue até o nome de domínio ou endereço IP público do seu servidor:
```
https://domínio_do_servidor_ou_IP
```

Selecione o idioma que você gostaria de usar:

[WordPress language selection](https://assets.digitalocean.com/articles/wordpress_lamp_1604/language_selection.png)

Em seguida, você chegará à página principal de configuração. Escolha um nome para o seu site WordPress e escolha um nome de usuário (é recomendável não escolher algo como “admin” por motivos de segurança). Uma senha forte é gerada automaticamente. Salve esta senha ou selecione uma senha forte alternativa.

Digite seu endereço de e-mail e escolha se você deseja desencorajar os mecanismos de pesquisa de indexar seu site:

[WordPress setup installation](https://assets.digitalocean.com/articles/wordpress_lamp_1604/setup_installation.png)

Quando estiver pronto, clique no botão Install WordPress. Você será direcionado para uma página que solicita que você faça login:

[WordPress login prompt](https://assets.digitalocean.com/articles/wordpress_lamp_1604/login_prompt.png)

Após o login, você será direcionado para o painel de administração do WordPress:

[WordPress login prompt](https://assets.digitalocean.com/articles/wordpress_lamp_1604/admin_screen.png)

No painel, você pode começar a fazer alterações no tema do seu site e publicar o conteúdo.


# CONCLUSÃO
O WordPress está instalado e pronto para uso! Alguns próximos passos comuns são escolher a configuração de permalinks para suas postagens (pode ser encontrada em Configurações > Links permanentes) ou selecionar um novo tema (em Aparência > Temas). Se esta é a primeira vez que você usa o WordPress, explore um pouco a interface para se familiarizar com o seu novo CMS ou verifique o guia [Primeiros Passos com o WordPress] (https://codex.wordpress.org/pt-br:Primeiros_Passos_com_o_WordPress) na documentação oficial.


Paz!!!