# CORRIGIGIR O ERRO 'INITRAMFS-CRYPTSETUP' DESCRITO LOGO ABAIXO. 
Esse procedimento funcionou Debian, e no BunsenLabs.
```
After system update the following is displayed in terminal:
_WARNING: Setting CRYPTSETUP in /etc/initramfs-tools/initramfs.conf is deprecated and will stop working in the future. Use /etc/cryptsetup-initramfs/conf-hook instead._
Solution
Add CRYPTSETUP=y in /etc/cryptsetup-initramfs/conf-hook. Terminal command for this:
```

Na própria mensagem de erro trás a solução que funcionou comigo usando Debian-9. Que é 'Add CRYPTSETUP=y in /etc/cryptsetup-initramfs/conf-hook'.


## PRIMEIRO OPÇÃO
Acessar o arquivo de configuração 'conf-hook' para alterar manualmente, descomentar e deixar '=y'
```

sudo nano /etc/cryptsetup-initramfs/conf-hook
Add CRYPTSETUP=y

``` 


## SEGUNDO OPÇÃO
Direcionando e confirmando cryptsetup para o arquivo criado
```

sudo sh -c 'echo "CRYPTSETUP=y" >> /etc/cryptsetup-initramfs/conf-hook'

```

**Obs. Considerem todas as aspa na linha de comando da segundo opção!**

> Breve Jesus voltará para buscar todos aqueles que o esperam. Estou me praparando para esse dia glorioso, E você?
> Que paz do Senhor repouse sobre ti!
