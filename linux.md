# ADICIONAR NOVO USUÁRIO

* Após criar o novo usuário ja aparecerá a opção para criação da senha
``` 
  adduser nome-usuario
```

## ADICIONAR USUÁRIO AO GRUPO SUDO
```
  usermod -aG sudo nome-usuario
```

Fonte: [Digital Ocean](https://www.digitalocean.com/community/cdtutorials/initial-server-setup-with-debian-9)

---
# CONTEÚDO AULA-2
* (clear) -> Limpa a tela
* (~) <- Símbolo Diretório padrão do root
* (#) <- Símbolo Logado como root usuario adim
* ($) <- Símbolo Logado como usuário

## DESLIGAR E REINICIAR
* (reboot) - Reinicia o linux
* (halt) - Desliga
* (shutdown -h now) - Também desliga o linux
* (shutdown -h 1) - Desliga o computador em um minuto
* (Ctrl +c) - Cancela a operação

## DIVERSOS
* (pwd) - mostra o diretorio q esta
* (cd /) - Se povimenta para raiz
* (cd + enter) - Leva ao diretório padrão d usuário + 
* (clear) - Limpa tela
* (ls) - Lista os principais diretórios do linux
* (cd home + enter) -  Vai para a pasta do home
* (cd ..) - Volta um diretório
* (date) - Exibe data e hora
* (cal) - Calendario
* (date;cal) - Exibe dois comandos com o ponte e virgula
* (man + comando) - Descrição do comando especificado
* (whatis) - Descrição específica
* (history) - Historico dos comandos usados
* (clear) - Limpa a tela
* (touch) - Cria arquivo

## CRIAR E APAGAR DIRETÓRIO
* (mkdir -c) - Cria diretórios ex: mkdir documentos
* (rm -r) - Apaga diretorios ex: rm -r documentos
* (rm -rf) - Apaga tdo sem perguntar

## EDITOR DE TEXTO(vi)
* É o editor que cai na "certificação LPI"
* (vi + nome do arquivo) - Cria ou edita arquivo
* (i) - Para escrever em cima do cursor
* (a) - Para escrever a partir do cursor
* (Esc:wq) - Salvar e salva
* (Esc u) - Desfaz o q estava fazendo
* (Esc:q!) - Sai do arquivo sem salvar
* (set number) - Numera as linhas

## EDIÇÃO
* (cat) - Mostra o conbteúdo do arquivo
* (tac + Nome do arquivo) - Mostra o conteudo de trás pra frente
* (mv + Nome do arquivo) - Mover ou renomear o arquivo ex: mv Serviços serviços
* (cp) - Faz backup, ex: cp serviços serviços.bkp

## PESQUISA
* (ls carta) - Mostra q tem carta
* (ls -l carta) - Mostra detalhes
* DIRETORIOS SÃO PASTAS; ARQUIVOS SÃO DOCUMENTOS:
* (ls -l) - Mostra o q eh arquivo e diretorio:
* (ls -lh) - Mostra Permissões Links Proprietários Grupo Tamanho Data e Hora Nome
* começa com (-) - É arquivo
* começa com (d) - É diretorio
* começa com (l) - É link
* (cat + nome do arquivo) - Visualiza o conteudo do arquivo

## TECLAS DE ATALHO
* (Pra cima) - Repete o último comando
* (Pra baixo) - Idem
* (tab) - Completa comando
* (cd ho+tab) - Completa o comando
* (history) - Exibe os mil últimos comando digitados

## comando para listar upgrade
```
apt list --upgradeable
```

## LOCALIZAR PROGRAMAS
```
  dpkg -l | grep apache2 
  dpkg -l | grep openjdk-8-jre
```

Fonte: [Professor José de Assis](https://youtu.be/agpNQ0Tv7ZU)

---

## COMPACTAR ARQUIVOS
```	
  tar -czvf arquivo.tar.gz arquivo/
    ou
  tar cf arquivo.tar arquivo  
```

## DESCOMPACTAR ARQUIVOS
```  
  tar -xzvf arquivo.tar.gz
    ou
  tar xf arquivo.tar arquivo  
```
---  

# COMANDO KILL
* Comando para parar um processo 
   * Verifica os programas que estão sendo executados
```
  top 
```

*  Mostra os programas em execução
``` 
  ps aux 
```
* Especificando 
``` 
  ps -ef | grep <nome>
```
* Interrompendo o programa
```
  kill <numero_PID>
```

Fonte: Meus arquivos

---

# COMANDO PARA VERIFICAR A VERSÃO DO SISTEMA:
```
  cat /etc/*-release
```

OU ENTÃO:

```
  cat /etc/*-release | grep PRETTY
  lsb_release -a
  uname -r (verifica versão do Kernel)
  uname -a
  uname -mrs
  uname --help
  cat /proc/version
```
---

# COMANDO PARA VERIFICAR INTEGRIDADE
```
  $ls <nomoe_programa>
  #Sha256sum <nome_programa> | grep <numero_sha256sum>
```
--- 

# DEDINIR EDITOR PADRÃO
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

---
# COMANDO chmod - ALTERA PERMISSÃO PELO TERMINAL
```
  chmod +x <arquivo/diretorio>
```

# COMANDO chmod - ALTERA AS PERMISSÕES DE ACESSO A ARQUIVOS E DIRETÓRIOS

**Modo de permissões octal**

* Sintaxe:
```
  chmod [permissões] [arquivos ou diretórios]
```
1. Execução - 1 
2. Escrita - 2 
3. Leitura - 4

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

# PROPRIETÁRIO | GRUPO | OUTROS

rwx|rw-|rw-
---|---|--- 
111|110|110
7|6|6

# 766
1. Proprietário > lê,escreve,executa; 
2. Grupo > lê, escreve; 
3. Outros > lê, escreve  


rw-|r--|x--
---|---|---
6|4|0

# 6	4	0
1. Proprietário > lê, escreve; 
2. Grupo > lê; 
3. Outros > lê

### PERMISSÕES ###

Proprietario|Grupo|Outros
---|---|---
rwx|r-x|r-x

### SIGNIFICADOS ###

* r = Read (Leitura)
* w = Write (Escrita)
* x = Execution (Execução)
* - = Sem Permissão

# PESQUISA COMPLETA DE PERMISSÕES

```
  ls -lh
```

Permissões|Links|Proprietários|Grupo|Tamanho|Data e Hora|Nome
---|---|---|---|---|---|---
drwxr-xr-x|2|marcus|marcus|4096|13/9/2017|mlssysem

---
# COMANDO PARA CRIAR ARQUIVO VAZIO - touch

* Criando arquivoteste
```
  sudo touch arquivoteste
```

* Mostra o arquivo criado 
```
  ls arquivoteste
```

* Mostra detalhes do arquivo criado
```
  ls -l arquivoteste
```

**Explicando**
```
-rwx-w-r-- (arquivo, Proprietário lê, escreve, executa; Grupo escreve; Outros lê)
```

# ALETRANDO PERMISSÕES 

1 .Proprietário, fazer tudo 
2. Grupo, só ler 
3. Outros, escrever

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
