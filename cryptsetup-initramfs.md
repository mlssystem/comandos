## Corrigigir o erro 'initramfs-cryptsetup' descrito logo abaixo. Esse procedimento funcionou Debian, e no BunsenLabs.

**After system update the following is displayed in terminal:
_WARNING: Setting CRYPTSETUP in /etc/initramfs-tools/initramfs.conf is deprecated and will stop working in the future. Use /etc/cryptsetup-initramfs/conf-hook instead._
Solution
Add CRYPTSETUP=y in /etc/cryptsetup-initramfs/conf-hook. Terminal command for this:**

Na própria mensagem de erro trás a solução que funcionou comigo usando Debian-9. Primeiro deve ser criado um arquivo com nome "conf-hook", depois é só direcionar cryptsetup com confirmação 'y' para ele.

##### Para resolver esse erro é só digitar o seguintes passos logo abaixo.

Primeiro passo

* Criando o arquivo conf-hook

```
sudo nano /etc/cryptsetup-initramfs/conf-hook
``` 
Segundo passo

* Direcionando e confirmando cryptsetup para o arquivo criado

```
sudo sh -c 'echo "CRYPTSETUP=y" >> /etc/cryptsetup-initramfs/conf-hook'
```

**Obs. Considerem as aspa na linha de comando do segundo passo!**

Breve Jesus voltará para buscar todos aqueles que o esperam. Estou me praparando para esse dia glorioso, E você?

Fiquem com Deus!

Que paz do Senhor repouse sobre ti!
