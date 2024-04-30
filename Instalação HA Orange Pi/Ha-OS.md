# Agente para Home Assistant OS

Este é o Agente do OS para Assistente Doméstico. Ele é usado para Home Assistant
OS e Home Assistant Tipos de instalação supervisionados e permite o
Home Assistant Supervisor para se comunicar com o sistema operacional host.

## Instalação & Atualização

### Usando o sistema operacional Home Assistant

O Agente do OS é pré-instalado com o Sistema Operacional Home Assistant.

As atualizações fazem parte das atualizações do Sistema Operacional Home Assistant, que
a interface do usuário do Home Assistant oferecerá para atualizar quando houver uma nova versão
disponível.

### Usando o Home Assistant Supervisionado no Debian

Faça o download do pacote Debian mais recente da página de lançamento do OS Agent GitHub em:

Referencia:
<https://github.com/home-assistant/os-agent/releases/latest>

Em seguida, instale (ou atualize) o pacote Debian baixado usando:

'''Concha
sudo dpkg -i os-agent_1.0.0_linux_x86_64.deb
'''
Nota: Substitua o arquivo 'deb' no exemplo acima pelo arquivo que você
ter baixado da página de lançamentos.

Você pode testar se a instalação foi bem-sucedida executando:

''Bash
gdbus introspect --system --dest io.hass.os --object-path /io/hass/os
'''

Isso deve **não** retornar um erro. Se você tiver uma introspecção de objeto
com 'interface' etc. OS Agent está funcionando conforme o esperado.

Talvez seja necessário instalar 'libglib2.0-bin' para obter o comando 'gdbus'.

## Desinstalar

Para remover o OS Agent do seu sistema use o sistema de empacotamento Debian:

```shell
sudo dpkg -r os-agent
```
## Desenvolvimento

### Compilar

```shell
go build -ldflags "-X main.version="
```

### Tests

```shell
gdbus introspect --system --dest io.hass.os --object-path /io/hass/os
gdbus call --system --dest io.hass.os --object-path /io/hass/os/Boards/Yellow --method org.freedesktop.DBus.Properties.Set io.hass.os.Boards.Yellow PowerLED "<false>"
```