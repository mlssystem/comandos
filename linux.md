# Adicionar novo usuário
fonte: [Digital Ocean](https://www.digitalocean.com/community/cdtutorials/initial-server-setup-with-debian-9
)

* Após criar o novo usuário ja aparecerá a opção para criação da senha
``` 
adduser nome-usuario
```

## Adicionar o usuário ao grupo sudo
```
usermod -aG sudo nome-usuario
```

---
# Aula 2
Fonte: [Professor José de Assis](https://youtu.be/agpNQ0Tv7ZU)

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


---

# Comando kill
Fonte: Meus arquivos

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
