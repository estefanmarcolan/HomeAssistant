Como desenvolver notificação unificadas dos status de bateria

Card Battery: https://github.com/maxwroc/battery-state-card (Instalação via HACS)

Projeto para importação (Blueprint): Clique para importar

Vídeo explicativo: 

https://www.youtube.com/watch?si=3WQh7MWvurOQ3KsZ&embeds_referring_euri=http%3A%2F%2Fwww.patte.com.br%2F&source_ve_path=MTY0NTA2&feature=emb_share&v=46-AI6GV0CE

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
