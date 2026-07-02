# Status e compatibilidade

Esta página separa o que já foi **observado em testes** do que está apenas **documentado como procedimento**. Ela não é uma garantia de que toda unidade BTV13 terá o mesmo resultado.

## Estado atual

| Área | Estado | Observação |
| --- | --- | --- |
| Hardware-alvo | BTV13 com plataforma Amlogic SC2 | A revisão da placa, RAM, eMMC e periféricos deve ser conferida em cada aparelho. |
| Linux pelo pendrive | Em validação | O fluxo está documentado, mas o método de boot pode variar por revisão e configuração anterior. |
| Sessão gráfica | Problema registrado | Há relato de tela cinza e falha do LightDM; use o [guia de diagnóstico](04-tela-cinza-lightdm.md). |
| Gravação com AML Tools | Procedimento documentado | Exige modo de gravação Amlogic, cabo/porta corretos e uma imagem realmente compatível. |
| SlimBOX H96 Max | Não é compatibilidade genérica | A imagem referenciada por [@devmfc](https://github.com/devmfc) só deve ser usada após validar o hardware da unidade. |
| Gravação na eMMC | Alto risco | Faça backup privado e valide primeiro fora do armazenamento interno. |

## Checklist de compatibilidade antes de usar uma imagem

Uma imagem **ARM64** não é automaticamente compatível. Antes de iniciar qualquer gravação, compare:

- SoC e família da placa;
- revisão/serigrafia da placa, quando acessível;
- quantidade e tipo de RAM e eMMC;
- bootloader e `dtb`/device tree esperados pela imagem;
- vídeo HDMI, Wi-Fi/Bluetooth e controladores USB presentes;
- método de entrada no modo de gravação Amlogic;
- origem, nome exato, data e SHA-256 da imagem.

Se um desses pontos estiver incerto, trate a imagem como **não validada** para o aparelho.

## Como registrar um resultado

Ao concluir um teste, informe se o resultado é:

- **confirmado:** repetido e funcional naquele aparelho;
- **parcial:** inicia, mas algum periférico ou o modo gráfico falha;
- **não confirmado:** apenas procedimento documentado, sem resultado reproduzido;
- **não compatível:** falhou por incompatibilidade de hardware ou imagem.

Use o modelo em [Primeiro boot e validações](03-primeiro-boot.md) e nunca envie dumps de eMMC, chaves ou identificadores do aparelho.