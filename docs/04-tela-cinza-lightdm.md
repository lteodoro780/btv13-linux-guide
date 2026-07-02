# 4. Tela cinza e diagnóstico do LightDM

## Sintoma

O sistema inicia, mas permanece em tela cinza ou não apresenta a sessão gráfica. Em um dos testes, o serviço `lightdm.service` encerrou com erro.

Antes de trocar pacotes ou reinstalar o sistema, colete os dados abaixo. Eles ajudam a separar falha do display manager, sessão gráfica, Xorg/Wayland, driver de vídeo, HDMI ou armazenamento cheio.

## 1. Acesse um terminal virtual

Tente `Ctrl` + `Alt` + `F2` ou `Ctrl` + `Alt` + `F3`. Entre com seu usuário e senha. Para voltar à sessão gráfica, tente `Ctrl` + `Alt` + `F1` ou `Ctrl` + `Alt` + `F7`.

## 2. Colete o estado do serviço

```bash
systemctl status display-manager --no-pager -l || true
systemctl status lightdm --no-pager -l || true
systemctl status tvbox-firstboot.service --no-pager -l || true
journalctl -b -u display-manager -n 120 --no-pager || true
journalctl -b -u lightdm -n 120 --no-pager || true
cat /etc/X11/default-display-manager 2>/dev/null || true
```

Também confira o espaço livre e erros gerais do boot:

```bash
df -hT
journalctl -b -p warning..alert --no-pager
```

## 3. Confira a parte gráfica

```bash
sudo dmesg -T | grep -Ei 'drm|gpu|mali|meson|amlogic|hdmi|fb|error|fail'
ls -la /var/log/lightdm 2>/dev/null || true
ls -la /var/log/Xorg* 2>/dev/null || true
```

Em imagens recentes, parte dos logs pode estar somente no `journalctl`; a ausência de arquivos em `/var/log` não confirma nem descarta o erro.

## 4. Ações de baixo risco

Estas ações não apagam dados, mas podem derrubar a sessão atual:

```bash
sudo systemctl restart lightdm
sudo systemctl reset-failed lightdm
sudo systemctl enable lightdm
```

Depois, veja o retorno:

```bash
systemctl status lightdm --no-pager -l
journalctl -b -u lightdm -n 120 --no-pager
```

## 5. O que registrar ao abrir uma issue

- foto da tela cinza;
- distribuição e versão;
- kernel (`uname -a`);
- saída dos comandos da seção 2;
- TV/monitor, resolução e tipo de cabo HDMI;
- se o aparelho aceita terminal virtual;
- se a falha acontece apenas pelo pendrive ou também no armazenamento interno.

## Observação

Não há uma correção única para tela cinza. A causa pode estar no LightDM, na sessão KDE/Xfce, no driver de vídeo, no kernel ou na negociação HDMI. Evite reinstalar ou alterar a eMMC antes de guardar os logs.