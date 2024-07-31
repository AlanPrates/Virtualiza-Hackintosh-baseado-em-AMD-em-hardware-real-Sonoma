# Virtualização em Hackintosh baseado em AMD em hardware real Sonoma

## Instruções para Configuração do VirtualBox com SIP Parcialmente Desabilitado

### Passos:

1. No arquivo `config.plist` (veja a imagem) dentro do seu EFI de boot, adicione os números `csr-active-config = 03080000` (veja a imagem) na seção NVRAM do `config.plist` (para contornar problemas de assinatura de kext com segurança e privacidade no Oracle Box com essa desativação parcial do SIP).

2. Adicione os detalhes do `AMFIPass.kext` (veja a imagem) na seção de kernel do `config.plist`. Salve o `config.plist` de volta na pasta EFI /OC.

3. Baixe a versão 1.40 do `AMFIPass.kext` e copie-o para a pasta Kext do seu drive EFI.

4. Certifique-se de que você pode resetar o NVRAM no Opencore ao reiniciar.

5. Reinicie, pressione espaço e selecione o número para resetar o seu NVRAM.

6. Agora deve iniciar com o SIP desativado e usar o AMFIPass para permitir o kernel do box.

7. Baixe e instale o VirtualBox v.6.1.48 ou 6.1.50.

8. Durante o processo de instalação, ele deve pedir para você assinar / permitir o Oracle Virtual Box. Permita isso dentro da seção "Segurança e Privacidade" nas Configurações do Sistema.

9. Após a instalação e a assinatura do kernel do box, ele pedirá para reiniciar. Vá em frente e reinicie.

10. Após reiniciar, localize e baixe/instale o `Oracle_VM_VirtualBox_Extension_Pack-6.1.50.vbox-extpack` (se estiver usando a versão 6.1.50).

11. Agora, obtenha uma ISO da Microsoft e instale o seu sistema operacional convidado - no meu caso, foi o Windows 10 32 bits ISO.

12. Siga os passos para instalar o sistema operacional convidado como faria normalmente.

13. Localize e baixe o `VBoxGuestAdditions_6.1.50.iso` ou `VBoxGuestAdditions_6.1.48.iso` e instale-os a partir de uma unidade de armazenamento ISO do convidado. Isso fornecerá vários recursos adicionais de hardware e funcionalidades.

14. Finalmente, ajuste seu sistema operacional convidado para exibir dispositivos apontadores USB, etc.

15. Se você tiver problemas ao executar o VirtualBox, feche completamente o Vbox (pare qualquer VM convidada em execução primeiro, se puder) e depois execute-o novamente a partir da pasta Aplicativos e não como um alias, pois às vezes os aliases se corrompem ou perdem a referência do software.

16. Eu tentei então reativar o SIP e desativar o `AMFIPass.kext` na seção Kernel do `config.plist`, reiniciar, resetar o NVRAM e iniciar o Sonoma, mas os erros do Kernel reapareceram e descobri que eles não eram mais "Permitidos" pelo sistema operacional. Consequentemente, as VMs convidadas do VirtualBox falharam ao iniciar. 😞

17. Então voltei a desativar parcialmente o SIP (`csr-active-config = 03080000`), mas não precisei mais do `AMFIPass` ativado agora que instalei o VirtualBox.

Mais informações em breve...

### Links Úteis:
- Virtual Box Old Builds:  https://www.virtualbox.org/wiki/Download_Old_Builds_6_1
e  https://download.virtualbox.org/virtualbox/6.1.50/  para encontrar os Guest Additions etc...
- AMFIPass kext:https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Acidanthera/AMFIPass-v1.4.0-RELEASE.zip
