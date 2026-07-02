# Linux no BTV13

Documentação técnica comunitária sobre boot, instalação e testes de Linux no **BTV13** com SoC **Amlogic SC2**.

> **Status:** experimental. Revisões de hardware, memória e periféricos podem variar entre aparelhos. Leia tudo antes de alterar o armazenamento interno.

## Objetivo

Registrar, de forma reproduzível, o processo usado para iniciar e testar Linux no BTV13: preparação do pendrive, primeiro boot, diagnóstico do modo gráfico e recuperação em caso de erro.

Este repositório **não** distribui firmware original, dumps de eMMC, APKs, chaves, credenciais, instruções de ativação, nem qualquer conteúdo ou serviço da plataforma BTV.

## Comece por aqui

1. [Requisitos e coleta de informações](docs/01-requisitos.md)
2. [Boot pelo pendrive](docs/02-boot-pendrive.md)
3. [Primeiro boot e validações](docs/03-primeiro-boot.md)
4. [Tela cinza e diagnóstico do LightDM](docs/04-tela-cinza-lightdm.md)
5. [Recuperação e backup local](docs/05-recuperacao.md)
6. [Windows — SlimBOX H96 Max com AML Tools e DevFMC](docs/06-windows-aml-tools-devfmc.md)

## Resultado dos testes

- Dispositivo: **BTV13**
- Plataforma observada: **Amlogic SC2**
- Método em teste: inicialização de Linux por pendrive
- Método adicional documentado: gravação pelo Windows com AML Tools, usando imagem SlimBOX H96 Max somente após validação de compatibilidade
- Ponto de atenção atual: configuração do modo gráfico, especialmente quando o LightDM falha ou a tela permanece cinza

## Regras de segurança

- Faça backup local da eMMC antes de escrever nela.
- Primeiro valide o sistema pelo pendrive; não use instalação interna como primeira tentativa.
- Confirme o disco com `lsblk` antes de usar `dd`, formatar ou montar partições.
- Não publique imagens completas da eMMC, números de série, MAC address, tokens, senhas ou arquivos proprietários.
- Use fonte de alimentação estável durante qualquer gravação.
- Não considere uma imagem compatível apenas porque o nome comercial do aparelho é parecido; confirme placa e hardware antes de gravar.

## Como contribuir

Relatos de teste são bem-vindos. Ao abrir uma issue, informe:

- modelo/revisão do aparelho, quando disponível;
- distribuição e versão usada;
- método de boot utilizado;
- saída de `uname -a`, `lsblk -f` e trechos relevantes de `dmesg`;
- o que funcionou e o que não funcionou: vídeo, rede, áudio, Bluetooth, USB, controle remoto e armazenamento.

Remova dados pessoais e identificadores do equipamento antes de enviar logs.

## Contexto de testes

Parte dos testes foi realizada em ambiente da ESA. Isso não representa projeto oficial, suporte institucional ou vínculo com a ESA ou com a BTV.

## Licença

Este material está disponível sob a [MIT License](LICENSE).