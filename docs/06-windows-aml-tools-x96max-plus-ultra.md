# 6. Windows — SlimBOX X96Max Plus Ultra com AML Tools

> **Risco alto:** uma imagem `.img` grava o armazenamento interno. Ela pode apagar o sistema atual, dados do aparelho e, se não for compatível com a placa, deixar o equipamento sem iniciar. Só prossiga depois de confirmar que a imagem é compatível com o hardware do seu BTV13.

## O que foi usado neste teste

- **Dispositivo-alvo:** BTV13;
- **Ferramenta no Windows:** AML Tools / USB Burning Tool compatível com Amlogic;
- **Cabo:** USB-A para USB-A, de dados;
- **Entrada no modo de gravação:** botão **reset** pressionado durante a detecção;
- **Imagem:** SlimBOX para **X96Max Plus Ultra**;
- **Página da imagem:** [slimBOXtv — X96Max Plus Ultra](https://slimboxtv.ru/x96max-plus-ultra/).

A página da SlimBOXtv identifica o X96Max Plus Ultra como plataforma Amlogic S905X4 e lista a slimBOXtv 11.45. Isso não torna a imagem oficialmente compatível com todo BTV13: o procedimento abaixo documenta um teste prático e precisa ser repetido com cautela em cada revisão de hardware.

> A imagem não deve ser reenviada neste repositório. Use a página de origem para download e registre o nome exato, versão e hash do arquivo utilizado.

## Antes de começar

1. Faça backup privado da eMMC, quando possível.
2. Use um cabo **USB-A × USB-A de dados**. Não use cabo apenas de carga nem hub USB.
3. Instale os drivers Amlogic e execute o AML Tools como administrador.
4. Baixe a imagem pela página oficial indicada acima e confirme seu hash:

```powershell
Get-FileHash "C:\AML\images\NOME-DA-IMAGEM.img" -Algorithm SHA256
```

5. Anote a versão do AML Tools e o SHA-256. Não publique a `.img`, backup de eMMC, serial, MAC, chaves ou credenciais.

## Parte A — carregar a imagem no AML Tools

1. Abra o AML Tools como administrador.
2. Instale ou atualize o driver Amlogic pelo próprio programa, se necessário.
3. Use **Import image** / **Importar imagem** e selecione a imagem `.img` do SlimBOX X96Max Plus Ultra.
4. Aguarde a importação terminar sem erros.
5. Antes de iniciar, mantenha **Overwrite Key** desmarcado e não use opções de apagar bootloader/chaves ou apagar tudo sem um motivo técnico e um método de recuperação validado.

## Parte B — colocar o BTV13 no modo de gravação

### Sequência registrada no teste

1. Deixe o BTV13 desligado.
2. Mantenha o botão **reset** pressionado.
3. Conecte o cabo **USB-A × USB-A** entre o computador e a porta USB/OTG usada para gravação no BTV13.
4. Continue segurando o reset enquanto o AML Tools tenta reconhecer o aparelho.
5. Quando o AML Tools mostrar um dispositivo conectado, prossiga para a gravação.

A posição exata da porta OTG e o instante de soltar o reset podem variar por revisão. Registre esses detalhes quando repetir o teste; não force cabos nem conectores.

**Sinal esperado:** o AML Tools mostra o dispositivo conectado e pronto para receber a imagem. Não clique em iniciar antes dessa detecção.

## Parte C — gravar a imagem

1. Com a imagem importada e o BTV13 detectado, clique em **Start** / **Iniciar**.
2. Acompanhe a barra de progresso e o status do programa.
3. Não desconecte o cabo USB, não desligue o aparelho e não feche o AML Tools durante a gravação.
4. Ao aparecer **Success** / **Sucesso**, clique em **Stop** / **Parar**.
5. Desconecte o cabo, desligue o BTV13 e faça o primeiro boot pela HDMI.

O primeiro boot pode levar mais tempo que o normal. Não interrompa enquanto houver atividade de inicialização.

## Registro do resultado

```text
Imagem usada:
Página de origem:
Versão/data da imagem:
SHA-256:
Versão do AML Tools:
Cabo utilizado: USB-A × USB-A
Botão reset: pressionado durante a detecção
Porta usada no BTV13:
Resultado da gravação:
Primeiro boot:
Vídeo:
Rede:
Áudio:
Wi-Fi/Bluetooth:
Problemas encontrados:
```

## Se o AML Tools não detectar o BTV13

1. Confirme que o cabo USB-A × USB-A é de dados e está em boas condições.
2. Tente outra porta USB direta no computador, sem hub.
3. Reinstale o driver Amlogic.
4. Repita desde o aparelho totalmente desligado, mantendo o reset pressionado durante a conexão.
5. Confirme a porta USB/OTG correta do BTV13.
6. Não use opções de apagar bootloader ou chaves para tentar forçar a detecção.

## Compatibilidade

A imagem foi publicada para **X96Max Plus Ultra**, não para BTV13. Antes de gravar, compare SoC, RAM, eMMC, bootloader, `dtb`/device tree, Wi-Fi/Bluetooth e controladores USB. Veja também [Status e compatibilidade](00-status-e-compatibilidade.md).