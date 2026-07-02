# 3. Primeiro boot e validações

## Objetivo

Confirmar o que funciona no Linux iniciado pelo pendrive antes de pensar em instalar qualquer coisa no armazenamento interno.

## Checklist mínimo

### Sistema e armazenamento

```bash
uname -a
hostnamectl
lsblk -f
df -hT
```

Verifique se a raiz (`/`) está na mídia esperada e se há espaço livre.

### Rede

```bash
ip a
ip route
nmcli device status 2>/dev/null || true
ping -c 3 1.1.1.1
```

Se o ping por IP funcionar, mas nomes não resolverem, verifique DNS:

```bash
resolvectl status 2>/dev/null || cat /etc/resolv.conf
```

### Vídeo e sessão gráfica

```bash
systemctl status display-manager --no-pager -l || true
loginctl
sudo dmesg -T | grep -Ei 'drm|gpu|mali|meson|amlogic|hdmi|fb'
```

No BTV13, o modo gráfico pode depender de uma combinação específica de kernel, driver de vídeo, firmware e resolução HDMI. Registre resolução, cabo/TV usados e comportamento da tela.

### Áudio

```bash
aplay -l 2>/dev/null || true
pactl list short sinks 2>/dev/null || true
```

### USB e periféricos

```bash
lsusb
lsblk
```

Teste teclado, mouse, pendrive e rede cabeada. O controle remoto e o Wi-Fi podem precisar de configuração adicional ou não funcionar com a imagem utilizada.

## Resultado do teste

Use este modelo no final de cada relato:

```text
Distribuição e versão:
Kernel:
Método de boot:
Vídeo:
Rede:
Áudio:
USB:
Wi-Fi/Bluetooth:
Armazenamento interno detectado:
Erros encontrados:
```

Caso a tela permaneça cinza ou o ambiente gráfico não carregue, siga [Tela cinza e diagnóstico do LightDM](04-tela-cinza-lightdm.md).