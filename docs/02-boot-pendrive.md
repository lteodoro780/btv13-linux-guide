# 2. Boot pelo pendrive

## Objetivo

Iniciar o Linux pelo pendrive sem modificar a eMMC interna. Só avance para instalação interna depois que vídeo, rede e armazenamento forem validados.

## 1. Escolha a imagem correta

Uma imagem **ARM64** não basta para garantir boot no BTV13. Ela também precisa ser compatível com o bootloader, `dtb`/device tree, kernel e drivers exigidos pelo hardware.

Antes de gravar o pendrive, registre:

- nome e versão exatos da imagem;
- origem e data do download;
- SHA-256 fornecido pela origem, quando houver;
- SoC, revisão da placa, RAM e eMMC do aparelho;
- método de boot esperado para aquela imagem.

Consulte [Status e compatibilidade](00-status-e-compatibilidade.md) antes de testar uma imagem nova.

## 2. Grave a imagem no pendrive

Use uma ferramenta de gravação como Balena Etcher, Raspberry Pi Imager ou equivalente. A gravação deve ser feita no **disco inteiro** do pendrive.

No Linux, também é possível usar `dd`, mas confirme o disco duas vezes antes de executar:

```bash
lsblk -o NAME,SIZE,MODEL,TRAN
sudo dd if=/caminho/da/imagem.img of=/dev/sdX bs=4M status=progress conv=fsync
sync
```

Substitua `/dev/sdX` pelo **disco inteiro do pendrive**, nunca por uma partição como `/dev/sdX1`. Um destino errado pode apagar o disco do computador.

## 3. Faça o teste de boot

1. Desligue totalmente o BTV13.
2. Conecte o pendrive e um teclado USB.
3. Ligue o aparelho e use somente o método de boot já confirmado para a sua revisão, quando houver.
4. Quando o sistema iniciar, aguarde a tela de login ou abra um terminal.

O acionamento do boot pode variar conforme revisão, firmware e configuração anterior. Quando descobrir um método funcional, publique o relato completo — incluindo porta usada, sequência de botões e comportamento da tela — sem expor identificadores do aparelho.

## 4. Confirme que o sistema veio do pendrive

No terminal, rode:

```bash
findmnt /
lsblk -f
```

O sistema de arquivos raiz (`/`) deve apontar para a mídia externa usada no teste. Se não estiver claro, pare e confira antes de continuar.

## 5. Primeira checagem

```bash
uname -a
ip a
systemctl status display-manager --no-pager -l || true
```

Se aparecer tela cinza ou o ambiente gráfico não abrir, siga o guia de [diagnóstico do LightDM](04-tela-cinza-lightdm.md).

## Importante

Não execute instaladores de eMMC, não formate `mmcblk*` e não copie arquivos para o armazenamento interno nesta fase. O pendrive serve exatamente para validar o sistema sem risco desnecessário.

Próximo: [primeiro boot e validações](03-primeiro-boot.md).