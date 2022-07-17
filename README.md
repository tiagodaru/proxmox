# PROXMOX ADICIONAR HD REAL NA VM - pass-through Hard Drive


Anexar discos físicos a uma VM no Proxmox

To attach a pass-through pass-through 

No shell do seu node de Proxmox use o comando abaixo para listar os IDs dos discos 

```
ls -la /dev/disk/by-id
```

No meu caso encontrei o disco que eu quero adicionar a minha VM que está registrando no número 102
E usando o comando abaixo no shell do meu node de Proxmoxpos posso adicionar o dico fisico a minha VM 102

```
qm set 102 -scsi1 /dev/disk/by-id/ata-WDC_WD10SPZX-75Z10T1_WX11A283033T-part1
```
Veja que no comando acima estou registrando o -scsi1, pois a VM já possuí o SCSI 0 que é o HD principal da máquina
Caso queria adicioar mais um HD lembre-se de mudar o número do SCSI 


Agora acessando o shell da VM 102 preciso criar e mapear este disco.
Usando o comando abaixo posso ver onde está registrado o HD que anexei na VM 102
```
sudo lsblk
```

Abaixo a linha onde mostra que o HD que eu anexei está registrado no /dev/sdc
/dev/sdc                           293G   56K  278G   1%

Agora basta criar uma pasta
```
sudo mkdir /mnt/pve/HD01
```
Agora vamos usar o comando abaixo para montar o nosso HD
```
sudo mount /dev/sdc /mnt/pve/HDD01
```

E depois montar nosso HD caso queira listar o conetúdo do HD
```
ls -la /mnt/pve/HDD01
```
Outro comando que pode usar para ver seu HDD e o registro de montagem
```
df -h
```

