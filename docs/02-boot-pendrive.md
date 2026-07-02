# 2. Boot pelo pendrive

## Objetivo

Iniciar o Linux pelo pendrive sem modificar a eMMC interna. Só avance para instalação interna depois que vídeo, rede e armazenamento forem validados.

## 1. Grave a imagem no pendrive

Use uma imagem compatível com arquitetura ARM64 e um programa de gravação como Balena Etcher, Raspberry Pi Imager ou ferramenta equivalente.

No Linux, também é possível usar `dd`, mas confirme o disco duas vezes antes de executar:

```bash
lsblk -o NAME,SIZE,MODEL,TRAN
sudo dd if=/caminho/da/imagem.img of=/dev/sdX bs=4M status=progress conv=fsync
sync
```

Substitua `/dev/sdX` pelo **disco inteiro do pendrive**, nunca por uma partição como `/dev/sdX1`. Um destino errado pode apagar o disco do computador.

## 2. Faça o teste de boot

1. Desligue totalmente o BTV13.
2. Conecte o pendrive e um teclado USB.
3. Ligue o aparelho e use o método de boot disponível no seu equipamento.
4. Quando o sistema iniciar, aguarde a tela de login ou abra um terminal.

O acionamento do modo de boot pode variar conforme revisão, firmware e configuração anterior. Registre no repositório o método que funcionou no seu aparelho, com fotos ou descrição clara.

## 3. Confirme que o sistema veio do pendrive

No terminal, rode:

```bash
findmnt /
lsblk -f
```

O sistema de arquivos raiz (`/`) deve apontar para a mídia externa usada no teste. Se não estiver claro, pare e confira antes de continuar.

## 4. Primeira checagem

```bash
uname -a
ip a
systemctl status display-manager --no-pager -l || true
```

Se aparecer tela cinza ou o ambiente gráfico não abrir, siga o guia de [diagnóstico do LightDM](04-tela-cinza-lightdm.md).

## Importante

Não execute instaladores de eMMC, não formate `mmcblk*` e não copie arquivos para o armazenamento interno nesta fase. O pendrive serve exatamente para validar o sistema sem risco desnecessário.

Próximo: [primeiro boot e validações](03-primeiro-boot.md).