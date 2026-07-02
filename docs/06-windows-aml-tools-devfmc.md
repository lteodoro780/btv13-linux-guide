# 6. Windows — SlimBOX H96 Max com AML Tools e DevFMC

> **Risco alto:** uma imagem `.img` grava o armazenamento interno. Ela pode apagar o sistema atual, dados do aparelho e, se não for compatível com a placa, deixar o equipamento sem iniciar. Este procedimento só deve ser usado depois de confirmar a compatibilidade do BTV13 com a imagem SlimBOX destinada ao H96 Max.

## Escopo

Esta página registra o fluxo de gravação pelo **Windows**, usando a imagem `.img` do **SlimBOX para H96 Max**, o **AML Tools** e o procedimento de entrada em modo de gravação chamado aqui de **DevFMC**.

O nome comercial `H96 Max` sozinho não comprova compatibilidade. Antes de gravar, confira o máximo possível: SoC, revisão da placa, tipo e tamanho de RAM/eMMC, portas e um teste anterior relatado para a mesma placa. Não publique a imagem no repositório; registre apenas nome, versão, origem e hash.

## Materiais

- computador com Windows;
- AML Tools instalado e executado como administrador;
- imagem SlimBOX no formato `.img`, já extraída em uma pasta local curta, por exemplo `C:\AML\images\`;
- cabo de dados compatível com a porta **OTG/USB de gravação** do BTV13; evite hub USB;
- fonte de alimentação estável do aparelho;
- acesso ao botão de reset/recovery, caso sua revisão possua um;
- backup local da eMMC, quando possível.

## Antes de começar

1. Salve fotos do aparelho, da etiqueta e dos conectores.
2. Guarde um backup privado da eMMC ou, pelo menos, registre os dados de hardware já levantados.
3. Confirme o hash da imagem recebida:

```powershell
Get-FileHash "C:\AML\images\SlimBOX-H96-Max.img" -Algorithm SHA256
```

4. Anote o hash no seu relato de teste. Não suba a imagem ou backup para o GitHub.
5. Feche programas que possam ocupar portas USB e conecte o computador diretamente ao aparelho, sem hub.

## Parte A — preparar o AML Tools

1. Clique com o botão direito no AML Tools e escolha **Executar como administrador**.
2. Instale/atualize o driver Amlogic pelo próprio AML Tools, quando a versão usada oferecer essa opção. Reconecte o cabo se o Windows pedir novo reconhecimento de dispositivo.
3. No menu de imagem, use **Import image** / **Importar imagem** e selecione o arquivo `.img` do SlimBOX H96 Max.
4. Aguarde o programa terminar de ler a imagem. Só continue quando o AML Tools mostrar que o pacote foi carregado sem erro.
5. Revise as opções de gravação antes de iniciar:
   - mantenha **Overwrite Key** desmarcado;
   - não use opções de apagar tudo/bootloader sem uma necessidade documentada e uma forma de recuperação conhecida;
   - quando o AML Tools mostrar tipos de limpeza, prefira o modo menos destrutivo exigido pelo seu teste.

Os nomes de menus e caixas variam conforme a versão do AML Tools; a regra é preservar chaves e evitar apagamento total sem motivo comprovado.

## Parte B — entrar no DevFMC / modo de gravação

Neste projeto, **DevFMC** é o passo de colocar o BTV13 em modo de gravação para que o AML Tools o reconheça. Faça a sequência com o aparelho desligado:

1. Deixe o BTV13 sem alimentação.
2. Conecte o cabo de dados na porta OTG/USB usada para gravação e no computador.
3. Mantenha pressionado o botão **reset/recovery** se a sua revisão usar esse método.
4. Com o reset pressionado, conecte a alimentação somente se a porta USB não fornecer detecção suficiente.
5. Solte o reset apenas depois de o AML Tools identificar um dispositivo na lista.
6. Se o dispositivo não aparecer, desligue, desconecte tudo e tente novamente com outro cabo, outra porta USB do computador e sem hub.

**Sinal esperado:** o AML Tools passa a exibir uma linha/dispositivo conectado, pronto para receber a imagem. Não clique em iniciar enquanto o aparelho não estiver identificado.

## Parte C — gravar a imagem

1. Com a imagem já importada e o BTV13 detectado no AML Tools, clique em **Start** / **Iniciar**.
2. Acompanhe a barra de progresso e o status mostrado pelo programa.
3. Não desconecte o cabo, não desligue a fonte e não feche o AML Tools durante a gravação.
4. Ao aparecer **Success** / **Sucesso**, clique em **Stop** / **Parar**.
5. Desconecte o cabo USB, desligue o aparelho e faça o primeiro boot normalmente pela HDMI.

O primeiro boot pode fazer configurações internas. Não interrompa o aparelho enquanto ele ainda estiver inicializando.

## Depois da gravação

Registre:

```text
Imagem usada:
Versão/data da imagem:
SHA-256:
Versão do AML Tools:
Método DevFMC usado:
Cabo/porta OTG utilizada:
Resultado da gravação:
Primeiro boot:
Vídeo:
Rede:
Áudio:
Wi-Fi/Bluetooth:
Problemas encontrados:
```

Faça também uma verificação básica do sistema: vídeo HDMI, Wi-Fi/Ethernet, áudio, USB, Bluetooth e estabilidade após reinicialização.

## Se o AML Tools não detectar o BTV13

1. Confira se o cabo é de **dados**, não apenas de carga.
2. Tente outra porta USB direta no computador.
3. Reinstale o driver Amlogic pelo AML Tools.
4. Repita o DevFMC começando com o aparelho totalmente desligado.
5. Verifique se está usando a porta OTG correta do BTV13.
6. Não avance para opções de apagar bootloader/chaves apenas para tentar forçar a detecção.

## Se a gravação falhar ou o aparelho não iniciar

- pare o procedimento e guarde a mensagem exata do AML Tools;
- registre em que porcentagem ocorreu a falha;
- confirme hash e compatibilidade da imagem;
- volte ao método de boot/recovery já documentado para o aparelho;
- não alterne imagens aleatórias entre tentativas.

Volte ao [README](../README.md) para registrar um relato de teste ou abrir uma issue com logs e fotos sem dados pessoais.