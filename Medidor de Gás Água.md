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

      watermete:
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

Codigo de reset dentro da pasta customize: 

Em ``sensor`` colocar a entidade criada em endidades ajudantes

```yaml
sensor.gasmeter:
  state_class: measurement
  last_reset: '2021-08-20T06:43:36.740703+00:00'
```
