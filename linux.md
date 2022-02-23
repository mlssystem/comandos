# ADICIONAR NOVO USUÁRIO
Após criar o novo usuário ja aparecerá a opção para criação da senha
``` 

adduser nome-usuario

```


## ADICIONAR USUÁRIO AO GRUPO SUDO
```

$ echo "usuario ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/usuario

```

Fonte: [Digital Ocean](https://www.digitalocean.com/community/cdtutorials/initial-server-setup-with-debian-9)

---

# CONTEÚDO AULA-2
```
(clear) -> Limpa a tela
(~) <- Símbolo Diretório padrão do root
(#) <- Símbolo Logado como root usuario adim
($) <- Símbolo Logado como usuário
```


## DESLIGAR E REINICIAR
Debian 11
```
sudo systemctl poweroff
sudo systemctl reboot
```
Demais distros
```
(reboot) - Reinicia o linux
(halt) - Desliga
(shutdown -h now) - Também desliga o linux
(shutdown -h 1) - Desliga o computador em um minuto
(Ctrl +c) - Cancela a operação
```


## DIVERSOS
```
(pwd) - mostra o diretorio q esta
(cd /) - Se povimenta para raiz
(cd + enter) - Leva ao diretório padrão d usuário + 
(clear) - Limpa tela
(ls) - Lista os principais diretórios do linux
(cd home + enter) -Vai para a pasta do home
(cd ..) - Volta um diretório
(date) - Exibe data e hora
(cal) - Calendario
(date;cal) - Exibe dois comandos com o ponte e virgula
(man + comando) - Descrição do comando especificado
(whatis) - Descrição específica
(history) - Historico dos comandos usados
(clear) - Limpa a tela
(touch) - Cria arquivo
```


## CRIAR E APAGAR DIRETÓRIO
```
(mkdir -c) - Cria diretórios ex: mkdir documentos
(rm -r) - Apaga diretorios ex: rm -r documentos
(rm -rf) - Apaga tdo sem perguntar
```


## EDITOR DE TEXTO(vi)
É o editor que cai na "certificação LPI"
```
(vi + nome do arquivo) - Cria ou edita arquivo
(i) - Para escrever em cima do cursor
(a) - Para escrever a partir do cursor
(Esc:wq) - Salvar e salva
(Esc u) - Desfaz o q estava fazendo
(Esc:q!) - Sai do arquivo sem salvar
(set number) - Numera as linhas
```


## EDIÇÃO
```
(cat) - Mostra o conbteúdo do arquivo
(tac + Nome do arquivo) - Mostra o conteudo de trás pra frente
(mv + Nome do arquivo) - Mover ou renomear o arquivo ex: mv Serviços serviços
(cp) - Faz backup, ex: cp serviços serviços.bkp
```


## PESQUISA
```
(ls carta) - Mostra q tem carta
(ls -l carta) - Mostra detalhes
DIRETORIOS SÃO PASTAS; ARQUIVOS SÃO DOCUMENTOS:
(ls -l) - Mostra o q eh arquivo e diretorio:
(ls -lh) - Mostra Permissões Links Proprietários Grupo Tamanho Data e Hora Nome
começa com (-) - É arquivo
começa com (d) - É diretorio
começa com (l) - É link
(cat + nome do arquivo) - Visualiza o conteudo do arquivo
```


## TECLAS DE ATALHO
```
(Pra cima) - Repete o último comando
(Pra baixo) - Idem
(tab) - Completa comando
(cd ho+tab) - Completa o comando
(history) - Exibe os mil últimos comando digitados
```


## LISTAR UPGRADE
```

apt list --upgradeable

```


# LOCALIZAR PROGRAMAS
```

dpkg -l | grep apache2 
dpkg -l | grep openjdk-8-jre

```
Fonte: [Professor José de Assis](https://youtu.be/agpNQ0Tv7ZU)

---


# COMPACTAR ARQUIVOS
```	

tar -czvf arquivo.tar.gz arquivo/
ou
tar cf arquivo.tar arquivo

```


# DESCOMPACTAR ARQUIVOS
```

tar -xzvf arquivo.tar.gz
ou
tar xf arquivo.tar arquivo

```


# COMANDO KILL
Comando para parar um processo 


## INTERROMPENDO O PROGRAMA
```

kill <numero_PID>

```


## VERRIFICAR PROGRAMAS QUE ESTÃO SENDO EXECUTADOS
```

top 

```


## MOSTRAR PROGRAMAS EM EXECUÇÃO
``` 

ps aux 

```


## ESPECIFICANDO 
``` 

ps -ef | grep <nome>

```
**Fonte: Meus arquivos**



# COMANDO PARA VERIFICAR A VERSÃO DO SISTEMA:
```

cat /etc/*-release

```
**OU ENTÃO**:
```

cat /etc/*-release | grep PRETTY
lsb_release -a
uname -r (verifica versão do Kernel)
uname -a
uname -mrs
uname --help
cat /proc/version

```


# COMANDO PARA VERIFICAR INTEGRIDADE
```

$ls <nomoe_programa>
#Sha256sum <nome_programa> | grep <numero_sha256sum>

```


# DEFINIR EDITOR PADRÃO
```

sudo update-alternatives --config editor

```


# CONFIGURAR TECLADO
```

dpkg-reconfigure keyboard-configuration

```

# ALTERAR O GRUPO DE UM ARQUIVO OU DIRETÓRIO - chgrp (change group)
**sintexe:**
```

chgrp [novo_grupo] [nome_arquivo]

```


# ALTERAR O PROPRIETÁRIO DE UM ARQUIVO OU DIRETÓRIO - chown (change owner)
**sintaxe:**
```

chown [novo_proprietário] [novo_arquivo]

```


# ADICIONAR UM NOVO GRUPO - addgroup
**sintaxe:**
```

addgroup [nome_grupo]

```


# COMANDO CHMOD


## COMANDO chmod - ALTERA PERMISSÃO PELO TERMINAL
```

chmod +x <arquivo/diretorio>

```


## COMANDO chmod - ALTERA AS PERMISSÕES DE ACESSO A ARQUIVOS E DIRETÓRIOS
**Modo de permissões octal**
Sintaxe:
```

chmod [permissões] [arquivos ou diretórios]

```
> 1. Execução - 1 
> 2. Escrita - 2 
> 3. Leitura - 4



## 1 = ligado / 0 = desligado

rwx|
---|
001	= 1|

--x|
---|
001 = 1|

-w-|
---|
010 = 2|

r--|
---|
100 = 4|

rw-|
---|
110 = 4 + 2 = 6|

rwx|
---|
111 = 4 + 2 + 1 = 7|


## PROPRIETÁRIO | GRUPO | OUTROS
rwx|rw-|rw-
---|---|--- 
111|110|110
7|6|6


## 766
> 1. Proprietário > lê,escreve,executa; 
> 2. Grupo > lê, escreve; 
> 3. Outros > lê, escreve

rw-|r--|x--
---|---|---
6|4|0


## 6	4	0
> 1. Proprietário > lê, escreve; 
> 2. Grupo > lê; 
> 3. Outros > lê


## PERMISSÕES
Proprietario|Grupo|Outros
---|---|---
rwx|r-x|r-x


## SIGNIFICADOS
```
r = Read (Leitura)
w = Write (Escrita)
x = Execution (Execução)
- = Sem Permissão
```


# PESQUISA COMPLETA DE PERMISSÕES
```

ls -lh

```

Permissões|Links|Proprietários|Grupo|Tamanho|Data e Hora|Nome
---|---|---|---|---|---|---
drwxr-xr-x|2|marcus|marcus|4096|13/9/2017|mlssysem


---
# COMANDO PARA CRIAR ARQUIVO VAZIO - touch


## CRIANDO ARQUIVO TESTE
```

sudo touch arquivoteste

```


## MOSTRAR ARQUIVO CRIADO 
```

ls arquivoteste

```

## MOSTRAR DETALHES DO ARQUIVO CRIADO
```

ls -l arquivoteste

```

### Explicando
```

-rwx-w-r-- (arquivo, Proprietário lê, escreve, executa; Grupo escreve; Outros lê)

```


# ALETRANDO PERMISSÕES 
> 1. Proprietário, fazer tudo 
> 2. Grupo, só ler 
> 3. Outros, escrever

```

touch - c
sudo chmod 724 arquivoteste
sudo ls -l arquivoteste
-rwxr---w-		

```


# PERMISSÃO GERAL PARA TODOS
```

sudo chmod 777 arquivoteste
sudo ls -l arquivoteste
-rwxrwxrwx

```


# LAMP
Normalmente, o diretório /var/www, mas também pode ser /var/www/html por exemplo. Por padrão, este diretório só pode ser escrito pelo root e para ficar mais prático, e poder acessar com o nosso usuário. 


## MUDANDO O DIRETÓRIO 
```

$ sudo chown -c -R seu_usuario /var/www/ 

```


# REINICIANDO O APACHE 
```

$ sudo /etc/init.d/apache2 restart 

```


# COMANDO CHOWN


## CHOWN DONO[:GRUPO] ARQUIVO

### Descrição
Este comando permite alterar o nome do dono e/ou do grupo de arquivos.

### Algumas opções do comando
```

-c : informa quais arquivos estão sendo alterados.
-h : altera o link, não o arquivo apontado pelo link.
-v : informa quais arquivos estão sendo processados (não necessariamente alterados).
-R : altera, recursivamente, dono e/ou grupo de arquivos.
−−help : exibe opções do comando.
−−version : exibe informações sobre o aplicativo.

```

### Exemplos
Suponha, por exemplo, a existência de um diretório de nome teste. Queremos que este diretório e todo o seu conteúdo passe a pertencer ao usuário aluno e ao grupo informatica. Podemos, então, digitar o comando
```

chown -Rc aluno:informatica teste

```
para alterar o dono e o grupo do diretório teste e de todos os arquivos e diretórios que estão hierarquicamente abaixo do diretório teste. Como o argumento -c é usado, será mostrada apenas a lista dos arquivos e diretórios alterados.

### Para alterar apenas o dono dos arquivos, digite
```

chown -Rc aluno teste

```

Se o objetivo é alterar apenas o grupo dos arquivos, basta digitar
```

chown -Rc :informatica teste

```

**Observações**
O comando **chgrp** altera o grupo de arquivos.
O comando **chmod** altera as permissões de arquivos.