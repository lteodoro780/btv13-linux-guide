# 5. Recuperação e backup local

## Objetivo

Recuperar acesso ao sistema sem executar procedimentos destrutivos por impulso. Esta seção não disponibiliza nem solicita firmware, dumps ou arquivos proprietários.

## Prioridade de recuperação

1. Tente iniciar o Linux pelo pendrive.
2. Recolha logs e identifique as partições com `lsblk -f`.
3. Monte a partição do sistema interno apenas para inspeção, quando necessário.
4. Faça backup local antes de qualquer gravação na eMMC.
5. Só altere o armazenamento interno quando houver um procedimento validado para seu aparelho.

## Identifique a eMMC

```bash
lsblk -o NAME,SIZE,MODEL,TYPE,FSTYPE,LABEL,MOUNTPOINTS
sudo blkid
```

A eMMC frequentemente aparece como `mmcblk0`, mas isso pode variar. Não use comandos de montagem, formatação ou cópia até conferir tamanho e partições.

## Montagem somente para leitura

Depois de identificar a partição correta, monte-a inicialmente como leitura:

```bash
sudo mkdir -p /mnt/btv13
sudo mount -o ro /dev/mmcblk0pX /mnt/btv13
ls -la /mnt/btv13
```

Substitua `mmcblk0pX` pela partição correta mostrada por `lsblk -f`. Para desmontar:

```bash
sudo umount /mnt/btv13
```

## Backup local da eMMC

Faça isso apenas com espaço suficiente em um disco externo e após confirmar o dispositivo de origem. O arquivo gerado deve ficar **privado**: ele pode conter informações do aparelho e dados proprietários.

```bash
sudo dd if=/dev/mmcblk0 of=/media/SEU_DISCO/btv13-emmc-backup.img bs=4M status=progress conv=fsync
sync
```

Valide a cópia com um hash:

```bash
sha256sum /media/SEU_DISCO/btv13-emmc-backup.img > /media/SEU_DISCO/btv13-emmc-backup.img.sha256
```

> Não faça upload desse backup para GitHub, Drive público ou fóruns.

## Recuperação de um sistema Linux instalado internamente

Quando o problema for somente a sessão gráfica, inicialize pelo pendrive e colete os logs antes de alterar arquivos. Em alguns casos, montar a instalação e usar `chroot` pode ajudar, mas execute isso apenas se o sistema do pendrive tiver a mesma arquitetura e você souber quais partições está usando.

Exemplo de preparação de `chroot`:

```bash
sudo mount /dev/mmcblk0pX /mnt/btv13
sudo mount --bind /dev /mnt/btv13/dev
sudo mount --bind /proc /mnt/btv13/proc
sudo mount --bind /sys /mnt/btv13/sys
sudo chroot /mnt/btv13 /bin/bash
```

Ao terminar:

```bash
exit
sudo umount /mnt/btv13/dev
sudo umount /mnt/btv13/proc
sudo umount /mnt/btv13/sys
sudo umount /mnt/btv13
```

## Não faça sem validação

- não formate `mmcblk*`;
- não instale uma imagem aleatória no armazenamento interno;
- não compartilhe dumps de eMMC;
- não remova pacotes gráficos sem guardar os logs e saber como reverter;
- não desligue o aparelho durante gravações.

Volte ao [README](../README.md) para registrar resultados e contribuir com testes.