# Como instalar os Adicionais para Convidados do VirtualBox no Debian?

### Antes de clicar em adicionais para convidados no Virtual Box (que na maioria das vezes não executa sem acusar erro). Faço o seguinte!

* Primeiro passo

```
sudo apt-get install build-essential linux-headers-`uname -r`
```

* Segundo passo

```
sudo apt install build-essential module-assistant
```

* Terceiro passo

```
sudo m-a prepare
```

* Quarto passo

   * clicar na opção inserir imagem para convidados (no virtual box).

* Quinto passo

```
sudo sh /media/cdrom/VBoxLinuxAdditions.run
``` 

* Sexto passo

```
reboot
```

Breve Jesus voltará para buscar todos aqueles que o esperam. Estou me praparando para esse dia glorioso, E você?

Fiquem com Deus!
