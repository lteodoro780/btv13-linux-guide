# Linux no BTV13

Documentação técnica comunitária sobre boot, instalação e testes de Linux no **BTV13** com SoC **Amlogic SC2**.

> **Status:** experimental. Revisões de hardware, memória e periféricos podem variar entre aparelhos. Leia tudo antes de alterar o armazenamento interno.

## Objetivo

Registrar, de forma reproduzível, o processo usado para iniciar e testar Linux no BTV13: preparação do pendrive, primeiro boot, diagnóstico do modo gráfico e recuperação em caso de erro.

Este repositório **não** distribui firmware original, dumps de eMMC, APKs, chaves, credenciais, instruções de ativação, nem qualquer conteúdo ou serviço da plataforma BTV.

## Comece por aqui

1. [Status e compatibilidade](docs/00-status-e-compatibilidade.md)
2. [Requisitos e coleta de informações](docs/01-requisitos.md)
3. [Boot pelo pendrive](docs/02-boot-pendrive.md)
4. [Primeiro boot e validações](docs/03-primeiro-boot.md)
5. [Tela cinza e diagnóstico do LightDM](docs/04-tela-cinza-lightdm.md)
6. [Recuperação e backup local](docs/05-recuperacao.md)
7. [Windows — SlimBOX X96Max Plus Ultra com AML Tools](docs/06-windows-aml-tools-x96max-plus-ultra.md)

## Resultado dos testes

- Dispositivo-alvo: **BTV13**
- Plataforma observada: **Amlogic SC2**
- Boot por pendrive: procedimento em validação; confira a compatibilidade da imagem antes de testar
- Sessão gráfica: há relato de tela cinza e falha do LightDM
- Gravação pelo Windows: teste documentado com AML Tools, cabo USB-A × USB-A e botão reset pressionado durante a detecção
- Imagem usada no teste Windows: SlimBOX para **X96Max Plus Ultra**, obtida na página de origem indicada no guia; não é compatibilidade genérica para todo BTV13

Consulte a página de [status e compatibilidade](docs/00-status-e-compatibilidade.md) antes de considerar qualquer procedimento como comprovado.

## Regras de segurança

- Faça backup local da eMMC antes de escrever nela.
- Primeiro valide o sistema pelo pendrive; não use instalação interna como primeira tentativa.
- Confirme o disco com `lsblk` antes de usar `dd`, formatar ou montar partições.
- Não publique imagens completas da eMMC, números de série, MAC address, tokens, senhas ou arquivos proprietários.
- Use fonte de alimentação estável durante qualquer gravação.
- Não considere uma imagem compatível apenas porque o nome comercial do aparelho é parecido; confirme placa, bootloader, `dtb`/device tree e hardware antes de gravar.

## Como contribuir

Relatos de teste são bem-vindos. Use o modelo em [CONTRIBUTING.md](CONTRIBUTING.md) e informe modelo/revisão, imagem, hash, método de boot, versões usadas e resultado de vídeo, rede, áudio, Bluetooth, USB, controle remoto e armazenamento.

Remova dados pessoais e identificadores do equipamento antes de enviar logs.

## Contexto de testes

Parte dos testes foi realizada em ambiente da ESA. Isso não representa projeto oficial, suporte institucional ou vínculo com a ESA ou com a BTV.

## Licença

A [MIT License](LICENSE) cobre apenas a documentação original deste repositório. Nomes, marcas, imagens, ferramentas e outros materiais de terceiros permanecem sujeitos às respectivas licenças e condições; eles não são redistribuídos aqui.