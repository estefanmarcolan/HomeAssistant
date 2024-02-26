``` ymal

      # Configuração para mostra o status por Whats (Potencia) Secadora
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
