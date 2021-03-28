# Adicionar novo usuário

* Após criar o novo usuário ja aparecerá a opção para criação da senha
``` 
  adduser nome-usuario
```

## Adicionar o usuário ao grupo sudo
```
  usermod -aG sudo nome-usuario
```

Fonte: [Digital Ocean](https://www.digitalocean.com/community/cdtutorials/initial-server-setup-with-debian-9)

---
# Aula 2
* (clear) -> Limpa a tela
* (~) <- símbolo Diretório padrão do root
* (#) <- símbolo Logado como root usuario adim
* ($) <- símbolo Logado como usuário

## DESLIGAR E REINICIAR
* (reboot) - reinicia o linux
* (halt) - desliga
* (shutdown -h now) - também desliga o linux
* (shutdown -h 1) - desliga o computador em um minuto
* (Ctrl +c) - cancela a operação

## DIVERSOS
* (pwd) - mostra o diretorio q esta
* (cd /) - se povimenta para raiz
* (cd + enter) - leva ao diretório padrão d usuário + 
* (clear) - limpa tela
* (ls) - lista os principais diretórios do linux
* (cd home + enter) -  vai para a pasta do home
*  (cd ..) - volta um diretório
* (date) - exibe data e hora
* (cal) - calendario
* (date;cal) - exibe dois comandos com o ponte e virgula
* (man + comando) - descrição do comando especificado
* (whatis) - descrição específica
* (history) - historico dos comandos usados
* (clear) - limpa a tela
* (touch) - cria arquivo
* (userad -m )

## CRIAR E APAGAR DIRETÓRIO
* (mkdir -c) - cria diretórios ex: mkdir documentos
* (rm -r) - apaga diretorios ex: rm -r documentos
* (rm -rf) - apaga tdo sem perguntar

## EDITOR DE TEXTO(vi)
* Eh o editor q cai na "certificação LPI"
* (vi + nome do arquivo) - cria ou edita arquivo
* (i) - para escrever em cima do cursor
* (a) - para escrever a partir do cursor
* (Esc:wq) - salvar e salva
* (Esc u) - desfaz o q estava fazendo
* (Esc:q!) - sai do arquivo sem salvar
* (set number) - numera as linhas

## EDIÇÃO
* (cat) - mostra o conbteúdo do arquivo
* (tac + nome do arquivo) - mostra o conteudo de trás pra frente
* (mv + nome do arquivo) - mover ou renomear o arquivo ex: mv Serviços serviços
* (cp) - faz backup, ex: cp serviços serviços.bkp

## PESQUISA
* (ls carta) - mostra q tem carta
* (ls -l carta) - mostra detalhes
* DIRETORIOS SÃO PASTAS; ARQUIVOS SÃO DOCUMENTOS:
* (ls -l) - mostra o q eh arquivo e diretorio:
* começa com (-) - eh arquivo
* começa com (dr) - eh diretorio
* começa com (l) - eh link
* (cat + nome do arquivo) -  visualiza o conteudo do arquivo

## TECLAS DE ATALHO
* (Pra cima) - repete o último comando
* (Pra baixo) - idem
* (tab) - completa comando
* (cd ho+tab) - colpleta o comando
* (history) - exibe os mil últimos comando digitados

Fonte: [Professor José de Assis](https://youtu.be/agpNQ0Tv7ZU)

---

# Comando kill
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

# Definir editor padrão
```
  sudo update-alternatives --config editor
```
# Alterar o grupo de um arquivo ou diretório - chgrp (change group)

**sintexe:**
```
  chgrp [novo_grupo] [nome_arquivo]
```

# Alterar o proprietário de um arquivo ou diretório - chown (change owner)

**sintaxe:**
```
  chown [novo_proprietário] [novo_arquivo]
```
# Adiciona um novo grupo - addgroup

**sintaxe:** 
```
  addgroup [nome_grupo]
```

---
# Comando chmod- Altera permissões pelo terminal
```
  chmod +x <arquivo/diretorio>
```

# Comando chmod - altera as permissões de acesso a arquivos e diretórios.

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

# Proprietário	Grupo	Outros

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

---
# Comando para criar arquivo vazio - touch

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

# Alterando permissões para o Proprietário fazer tudo, Grupo só ler, Outros escrever.
```
touch - c
sudo chmod 724 arquivoteste
sudo ls -l arquivoteste
-rwxr---w-		
```

# Permissão geral para todos
```
sudo chmod 777 arquivoteste
sudo ls -l arquivoteste
-rwxrwxrwx
```
