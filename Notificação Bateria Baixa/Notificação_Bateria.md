Como desenvolver notificação unificadas dos status de bateria

Card Battery: https://github.com/maxwroc/battery-state-card (Instalação via HACS)

Projeto para importação (Blueprint): Link para importar: https://gist.github.com/sbyx/1f6f434f0903b872b84c4302637d0890

Caminho: `` Configurações ``  ``Automações`` e ``Modelos Blueprints``

![image](https://github.com/estefanmarcolan/HomeAssistant/assets/153628041/7272ad6d-8233-477d-a6af-b20120d66e1a)


Vídeo explicativo: 

https://www.youtube.com/watch?si=3WQh7MWvurOQ3KsZ&embeds_referring_euri=http%3A%2F%2Fwww.patte.com.br%2F&source_ve_path=MTY0NTA2&feature=emb_share&v=46-AI6GV0CE

Para usar a automação, após instalar o projeto clicar em criar automação! 

Card (LoveLace) 

``` yaml
type: custom:battery-state-card
title: Fechaduras
sort_by_level: asc
secondary_info: last_updated
color_thresholds:
  - value: 20
    color: red
  - value: 50
    color: yellow
  - value: 100
    color: green
entities:
  - entity: sensor.fechadura_entrada_battery
  - entity: sensor.yrd226_battery
  - entity: sensor.tyeb144d0f4300eb4d5dycai
```

ymal em Automação

``` yaml
- id: '1631481683157'
  alias: Aviso de bateria baixa
  description: ''
  use_blueprint:
    path: sbyx/low-battery-level-detection-notification-for-all-battery-sensors.yaml
    input:
      threshold: 40
      actions:
      - service: notify.persistent_notification
        data:
          message: Os sensores {{sensors}} estão com bateria baixa!
```

![image](https://github.com/estefanmarcolan/HomeAssistant/assets/153628041/63f45aaf-d609-47ae-9dc1-9f130646080d)

``` yaml

service: notify.notify
metadata: {}
data:
  title: Nível Baterias Baixa
  message: Os Senssores {{ Sensores }} estão com baterial baixa.

```



