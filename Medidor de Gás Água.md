Configurando Sensor Red magnético para medir consumo de água e gás. 

Após cadastra o sensor no Tuya App o device vai aparecer no HA como um sensor Red de porta (abre e fecha), assim vamos realizar as configurações para converter esse dado:

![image](https://github.com/estefanmarcolan/HomeAssistant/assets/153628041/1cf49277-c79b-4a40-9514-af3e3188e0b9)

1 - Passo criar um entidades ajudante em ``Configurações`` ``Dispositivos`` no menu superior em ``Entidades ajudantes`` criaremos um ajudante, selecionando a opção de ``contador``

![image](https://github.com/estefanmarcolan/HomeAssistant/assets/153628041/ccc65f4e-fa80-4deb-91fb-1128f4ba695e)

No contador defina o nome Water Meter ou Gas Meter e um ícone conforme necessidade. 

2 - Passo criar uma Automação para realizar a medição! 

Codigo YAML exemplo: 

``` YAML
alias: Água Counter
description: Automação que faz a medição de águga
trigger:
  - type: opened
    platform: device
    device_id: f11c18355ccb2e6a66ffe407cd29a350
    entity_id: 018e2cb27ee36c8141e0250f2d9353af
    domain: binary_sensor
condition: []
action:
  - service: counter.increment
    metadata: {}
    data: {}
    target:
      entity_id: counter.agua_counter
mode: single
````

![image](https://github.com/estefanmarcolan/HomeAssistant/assets/153628041/27ffae65-d6c4-4a68-883a-0738d5e72396)

3 - Passo configurações no file Editor: 

Configurações necessárias em  ``File Editor`` e ``Configuration.yaml``

``` yaml
sensor:
  - platform: template
    sensors:
      gasmeter:
        friendly_name: Gas_Meter
        value_template: "{{ states ('counter.gas_counter') | float * 0.01}}"
        unit_of_measurement: "m³"
        icon_template: "mdi:fire"
        device_class: gas

      watermeter:
        friendly_name: Agua_Meter
        value_template: "{{ states ('counter.agua_counter') | float * 1}}"
        unit_of_measurement: "L"
        icon_template: "mdi:water"
        device_class: water
```

Em seguida precisamos criar uma pasta com o nome: ``customize.yaml`` e colocar um include na pasta ``Configuration.yaml``

include:
``` yaml
homeassistant:
  customize: !include customize.yaml
```

Código de reset dentro da pasta customize: 

Em ``sensor`` colocar a entidade criada em entidades ajudantes

```yaml
sensor.gasmeter:
  state_class: total_increasing
  last_reset: '2021-08-20T06:43:36.740703+00:00'
  
sensor.watermete:
  state_class: total_increasing
  last_reset: '2021-08-20T06:43:36.740703+00:00'
```
