# 1. Requisitos e coleta de informações

## Objetivo

Preparar o ambiente e registrar o estado do aparelho antes de testar Linux. Esta etapa reduz o risco de gravar no disco errado ou perder a instalação original.

## Materiais

- BTV13 ligado a uma TV/monitor por HDMI;
- fonte de alimentação estável;
- pendrive de boa qualidade, de preferência com 8 GB ou mais;
- teclado USB;
- outro computador para gravar a imagem do sistema;
- rede cabeada, quando possível, para facilitar os primeiros testes;
- espaço externo suficiente para um backup local da eMMC, caso você decida fazê-lo.

## Antes de alterar qualquer coisa

1. Teste primeiro pelo pendrive. Não faça instalação na eMMC como primeira etapa.
2. Registre fotos do aparelho, da tela de boot e de eventuais mensagens de erro.
3. Guarde backups apenas localmente. Uma imagem bruta da eMMC pode conter identificadores e conteúdo proprietário e não deve ser publicada neste repositório.
4. Nunca rode comandos de gravação sem confirmar o dispositivo com `lsblk`.

## Coleta básica no Linux iniciado pelo pendrive

Abra um terminal e salve a saída abaixo em um arquivo de texto:

```bash
uname -a
cat /proc/cpuinfo
lsblk -o NAME,SIZE,MODEL,TYPE,FSTYPE,MOUNTPOINTS
lsblk -f
ip a
sudo dmesg -T | tail -n 200
```

Para localizar mensagens ligadas a vídeo, GPU ou Amlogic:

```bash
sudo dmesg -T | grep -Ei 'amlogic|meson|drm|gpu|mali|hdmi|fb'
```

## Identificando os discos

Em geral:

- `mmcblk*` costuma ser o armazenamento eMMC interno;
- `sd*` costuma ser um pendrive ou disco USB.

Isso **não é uma garantia**. Confirme pelo tamanho, modelo e pontos de montagem mostrados por `lsblk` antes de continuar.

## Registro sugerido para cada teste

| Item | Exemplo |
| --- | --- |
| Data | 2026-07-02 |
| Distribuição | Kubuntu/Ubuntu e versão |
| Forma de boot | Pendrive / outro método |
| Vídeo | OK / sem imagem / tela cinza |
| Rede | Ethernet / Wi-Fi / indisponível |
| Áudio | OK / pendente |
| Observações | Mensagens ou comportamento visto |

Próximo: [boot pelo pendrive](02-boot-pendrive.md).