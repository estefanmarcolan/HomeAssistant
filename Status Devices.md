Video de exemplo: https://www.youtube.com/watch?v=eYJMY0oDpd4&t=50s

Exemplo de Código ``Configuration.Yaml`` para status de ON e OFF de dispositivos:

``` yaml
- platform: template
  sensors:
    status_bomba_1:######
      friendly_name_template: name#######
      value_template: >-
        {% if is_state('#########################', 'off') %}
          Desligada
        {% elif states('##########################', on) %}
          Ligada
        {% else %}
          ligada
        {% endif %}
```

Exemplo de Código ``Configuration.Yaml``  para status por Whats (potencia), 

``` yaml
- platform: template
  sensors:
    status_secadora:
      friendly_name_template: Status Secadora 
      value_template: >-
        {% if is_state('switch.sonoff_1000fe4826', 'off') %}
          Desligada
        {% elif states('sensor.sonoff_1000fe4826_power')|float > 4 %}
          Ligada
        {% else %}
          Desligada
        {% endif %}
      icon_template: >-
        {% if is_state('switch.sonoff_1000fe4826', 'off') %}
          mdi:power-off
        {% elif states('sensor.sonoff_1000fe4826_power')|float > 4 %}
          mdi:power
        {% else %}
          mdi:power-cycle
        {% endif %}
          
```
