### HABILITAR NO VIRTUALBOX A CONEXÃO NAT E REDE INERNA DEBIAN-8

#### Os passos abaixo foram usados após a instalação do servidor Debian-8 com a configuração de Rede no VirtualBox desabilitada

Esse é o caminho no caso da rede, para editar o arquivo 

```
vi /etc/network/interfaces
```

Segue o script e destaque, e algumas informações que o antecede
```
auto eth0
iface eth0 inet dhcp - Comando usado para configurar o ip automaticamente.
```

__*Comando universal para verificar se tem conexão com a rede, usa o protocolo ICMP ex:*__
* ping www.google.com

Comando para habilitar a placa de rede
```
ifup eth0
```
O teste do ping tem que ser OK após a configuração

Acesse novamente o arquivo interfaces
```
vi /etc/network/interfaces
```

**Configurar o ip manual com seguinte script**
```
auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
```

Logo após usar o comando abaixo para habilitar a rede
```
ifup eth1
```
Quando o Linux não se manifesta significa que aceitou o comando

### CONFIGURAR O REPOSITÓRIO
Editar o arquivo de configuração do Repositório
```
vi /etc/apt/sources.list
```
1. Comentar a linha 5
1. Descomentar a linha 8, 10, 17, 18 (não deixar espaço), são "linhas que se refere à segurança".
1. Acrescentar duas linhas, referentes aos repositórios oficiais do Brasil.
1. Após copiar e colar as linhas 17,18 (2yy) e (p) para colar onde quiser.
1. Acrescentar o (.br) nas linhas 19,20, e após o ftp, e mover o -update (nas linhas 19.20)

Atualizar o Servidor
```
apt-get update
```

### CONFIGURAR O ACESSO REMOTO

#### Instalando o pacote do acesso remoto.
```
apt-get install openssh-server
```

Conexão deve estar em "Modo Bridge
**Reinicie a rede**
```
service networking restart
```

Atualize
```
apt-get update && apt-get  -y upgrade
```
Abrir o putty (aplicativo para acesso remoto), não é aconselhável acessar como "root" por questões de segurança (nunca se sabe o ambiente da máquina cliente), evitando risco de captura de senha... Portanto pode acessar como usuário (cd /home/usuário) - usar o mkdir e criar pasta remotamente para testar.

* Após logar como usuário comum! Passe para usuário "root", no terminal "putty", basta digitar sem aspas "su", e a senha do "root", e será transformado no super usuário.

### PÓS-INSTALAÇÃO

**Relembrando**

**'etc' é o diretório de configuração do Linux**
```
cd /etc
```

**"issue" é o arquivo que configura pagina de login no Debian-8, e quando colocado o (*) o sistema apresenta tudo que contem (issue).**
```
ls issue*
```

Comando usado para mostrar o conteúdo do issue.
```
cat issue
```

* Copie esse arquivo (cp issue issue.bkp) dentro da pasta /etc caso de algum erro terá o original.*

Comando para baixar do repositório do Debian, o Linux logo
```
apt-get install linuxlogo
```

Comando para listar o arquivo e direciona a saída para o arquivo issue, isso devido ao uso do (>), ou seja, o arquivo issue agora exibirá o conteúdo do issue.linuxlogo.
```
cat issue.linuxlogo>issue
```

**Reiniciar**
```
reboot
```
#### É isso!!!


## INSTRUÇÕES PARA PERSONALIZAR A MESNSAGEM DE BOAS VINDAS NO DEBIAN-8
**Logar como root, e digitar o comando para o diretório de configuração do Linux (cd /etc) depois (pwd) para confirmar se está na pasta desejada.**

Renomeando para depois criar outro editando com Bem Vindo!
```
mv motd motd.bkp
```

Criar um novo arquivo com mensagem de boas vindas
```
vi motd
```

**Atualizar o servidor** 
```
apt-get update) 
```

**Atualiza os pacotes**
```
apt-get -u upgrade
```

Comando para instalar o pacote que verifica quais serviços está inicializando junto com o servidor.
```
apt-get install rcconf
```

Usado também para escolher app para inicializar com o sistema,se quiser  desmarque o "SSH".
```
rcconf
```

Obs. Essas informaçõe eu digitei para uso pessoal, assistindo as aulas do curso oferecido pelo Professor Jose de Assis no [Youtube](https://www.youtube.com/watch?v=fM3G7yLNAjQ&list=PLbEOwbQR9lqwtP82l8eIiWY5TOx10L1HO)

* Ja usei esses comandos para o Debian 9 e bateu certo. Espero que possa ajudar alguém!

Não se esqueçam meus queridos! JESUS voltará para buscar todos aqueles que creem! Meditem na palavra de Jesus no evangelho de João capitulo 14.

Fiquem com Deus!

_PAZ!_



