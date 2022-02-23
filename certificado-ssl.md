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