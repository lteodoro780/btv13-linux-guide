# 6. Windows — SlimBOX H96 Max com AML Tools

> **Risco alto:** uma imagem `.img` grava o armazenamento interno. Ela pode apagar o sistema atual, dados do aparelho e, se não for compatível com a placa, deixar o equipamento sem iniciar. Só prossiga depois de confirmar que a imagem é compatível com o hardware do seu BTV13.

## Escopo

Este guia registra um **procedimento de teste** no Windows com **AML Tools** para gravar uma imagem `.img` do **SlimBOX para H96 Max** no BTV13. Ele não é uma confirmação de compatibilidade para todas as unidades BTV13.

A referência informada para a imagem é o perfil [@devmfc](https://github.com/devmfc). **devmfc não é um modo de gravação**: é a referência/origem indicada neste relato. A etapa técnica é colocar o aparelho no **modo de gravação Amlogic**, normalmente por uma porta OTG e, em algumas revisões, pelo botão reset/recovery.

O nome comercial `H96 Max` sozinho não comprova compatibilidade. Antes de gravar, compare SoC, revisão da placa, RAM, eMMC, bootloader, `dtb`/device tree, conectores e relatos feitos no mesmo hardware. Consulte primeiro [Status e compatibilidade](00-status-e-compatibilidade.md).

## Materiais

- computador com Windows;
- AML Tools instalado e executado como administrador;
- imagem SlimBOX em formato `.img`, já extraída em uma pasta local curta, por exemplo `C:\AML\images\`;
- cabo de **dados** compatível com a porta OTG/USB de gravação do BTV13; evite hub USB;
- fonte de alimentação estável do aparelho;
- acesso ao botão de reset/recovery, caso sua revisão possua um;
- backup local da eMMC, quando possível.

## Antes de começar

1. Salve fotos do aparelho, etiqueta, conectores e — quando acessível — serigrafia da placa.
2. Guarde um backup privado da eMMC ou, no mínimo, registre os dados de hardware já levantados.
3. Registre a origem exata: perfil/repositório, nome completo do arquivo, versão/data, URL ou release e data do download.
4. Confirme o hash da imagem recebida:

```powershell
Get-FileHash "C:\AML\images\SlimBOX-H96-Max.img" -Algorithm SHA256
```

5. Anote o hash no relato de teste. Não suba a imagem ou o backup para o GitHub.
6. Feche programas que possam ocupar portas USB e conecte o computador diretamente ao aparelho, sem hub.

## Parte A — preparar o AML Tools

1. Clique com o botão direito no AML Tools e escolha **Executar como administrador**.
2. Instale ou atualize o driver Amlogic pelo próprio AML Tools, quando a versão usada oferecer essa opção. Reconecte o cabo se o Windows solicitar novo reconhecimento.
3. No menu de imagem, use **Import image** / **Importar imagem** e selecione a `.img` do SlimBOX H96 Max.
4. Espere o programa terminar de ler o pacote. Continue apenas quando a imagem estiver carregada sem erro.
5. Revise as opções antes de iniciar:
   - mantenha **Overwrite Key** desmarcado;
   - não use opções de apagar bootloader ou apagar tudo sem necessidade documentada e sem um método conhecido de recuperação;
   - quando houver escolha de limpeza, prefira a opção menos destrutiva exigida pelo seu teste.

Os nomes de menus e caixas variam por versão do AML Tools. A regra é preservar chaves e evitar apagamento total sem motivo comprovado.

## Parte B — entrar no modo de gravação Amlogic

A sequência física pode variar entre revisões. Não presuma que qualquer USB do aparelho serve como OTG e não force cabos ou conectores.

1. Comece com o BTV13 totalmente desligado.
2. Conecte o cabo de dados na porta OTG/USB que tenha sido identificada para gravação e no computador.
3. Mantenha pressionado o botão **reset/recovery** apenas quando esse for o método confirmado para a sua revisão.
4. Conecte a alimentação conforme a sequência já validada para aquele hardware; algumas unidades são reconhecidas pela USB, outras exigem alimentação externa.
5. Solte o reset depois que o AML Tools identificar um dispositivo na lista.
6. Se o aparelho não aparecer, desligue, desconecte tudo e tente novamente com outro cabo de dados, outra porta USB direta e sem hub.

**Sinal esperado:** o AML Tools exibe um dispositivo conectado, pronto para receber a imagem. Não clique em iniciar enquanto o aparelho não estiver identificado.

## Parte C — gravar a imagem

1. Com a imagem importada e o BTV13 detectado, clique em **Start** / **Iniciar**.
2. Acompanhe a barra de progresso e o status apresentado pelo programa.
3. Não desconecte o cabo, não desligue a fonte e não feche o AML Tools durante a gravação.
4. Ao aparecer **Success** / **Sucesso**, clique em **Stop** / **Parar**.
5. Desconecte o cabo USB, desligue o aparelho e faça o primeiro boot normalmente pela HDMI.

O primeiro boot pode executar configurações internas. Não interrompa o aparelho enquanto ele ainda estiver inicializando.

## Depois da gravação

Registre:

```text
Imagem usada:
Origem exata da imagem:
Versão/data do arquivo:
SHA-256:
Versão do AML Tools:
Método de entrada no modo Amlogic:
Cabo/porta OTG utilizada:
Resultado da gravação:
Primeiro boot:
Vídeo:
Rede:
Áudio:
Wi-Fi/Bluetooth:
Problemas encontrados:
```

Teste pelo menos vídeo HDMI, Ethernet/Wi-Fi, áudio, USB, Bluetooth e estabilidade após reinicialização.

## Se o AML Tools não detectar o BTV13

1. Confira se o cabo é de **dados**, não somente de carga.
2. Tente outra porta USB direta no computador.
3. Reinstale o driver Amlogic pelo AML Tools.
4. Repita o procedimento com o aparelho totalmente desligado.
5. Confirme a porta OTG correta na sua revisão do BTV13.
6. Não avance para opções de apagar bootloader ou chaves apenas para tentar forçar a detecção.

## Se a gravação falhar ou o aparelho não iniciar

- pare o procedimento e guarde a mensagem exata do AML Tools;
- registre em que porcentagem ocorreu a falha;
- confirme hash e compatibilidade da imagem;
- volte ao método de boot/recovery já documentado para o aparelho;
- não alterne imagens aleatórias entre tentativas.

Volte ao [README](../README.md) para registrar um relato de teste ou abrir uma issue com logs e fotos sem dados pessoais.