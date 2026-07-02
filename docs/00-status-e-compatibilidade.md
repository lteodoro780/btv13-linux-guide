# Status e compatibilidade

## Estado atual

- Hardware-alvo: BTV13 com plataforma Amlogic SC2.
- Linux pelo pendrive: em validação.
- Sessão gráfica: há relato de tela cinza e falha do LightDM.
- Gravação pelo Windows: teste registrado com AML Tools, cabo USB-A × USB-A e reset pressionado durante a detecção.
- Imagem do teste: SlimBOX para X96Max Plus Ultra. Não é uma imagem oficial para BTV13 nem compatibilidade genérica.
- Gravação da eMMC: alto risco; mantenha backups privados.

Veja o procedimento completo em [Windows — SlimBOX X96Max Plus Ultra com AML Tools](06-windows-aml-tools-x96max-plus-ultra.md).

Uma imagem ARM64 não é automaticamente compatível. Confirme SoC, RAM, eMMC, bootloader, `dtb`/device tree, periféricos, origem e SHA-256 antes de gravar.