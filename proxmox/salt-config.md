---
title: Salt Config
description: 
published: 1
date: 2023-11-10T17:09:27.444Z
tags: 
editor: markdown
dateCreated: 2023-11-10T17:09:27.444Z
---

# Salt

Just an example for creating a custom component in config.yml. Salt used as an example since it's moved to ESPHome

```
sensor:
  - platform: rest
    name: salt_lamp_level
    unique_id: sensor.salt_lamp_level
    resource: http://10.0.0.187/getBrightness
  - platform: rest
    name: salt_lamp_value
    unique_id: sensor.salt_lamp_value
    resource: http://10.0.0.187/status
    
light:
  - platform: template
    lights:
      salt_lamp:
        friendly_name: "Salt"
        unique_id: light.salt_lamp
        level_template: "{{ states('sensor.salt_lamp_level') }}"
        value_template: "{{ is_state('sensor.salt_lamp_value', '1') }}"
        turn_on:
          service: rest_command.salt_lamp_on
        turn_off:
          service: rest_command.salt_lamp_off
        set_level:
          service: rest_command.salt_lamp_brightness
          data:
            brightness: "{{ brightness }}"
            
rest_command:
    salt_lamp_on:
        url: http://10.0.0.187/on
        method: GET
    salt_lamp_off:
        url: http://10.0.0.187/off
        method: GET
    salt_lamp_brightness:
        url: 'http://10.0.0.187/setBrightness?brightness={{ int(brightness / 255 * 100) }}'
        method: GET
```