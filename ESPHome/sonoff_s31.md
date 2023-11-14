# Sonoff S31 smart plug

Offical ESPHOME link for s31: https://devices.esphome.io/devices/Sonoff-S31

## Device configs
Add the following to the bottom of your ESPHome config for the device.
```
# Device Specific Config
uart:
  rx_pin: RX
  baud_rate: 4800

binary_sensor:
  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: True
    name: "Sonoff S31 Button"
    on_press:
      - switch.toggle: relay
  - platform: status
    name: "Sonoff S31 Status"

sensor:
  - platform: wifi_signal
    name: "Sonoff S31 WiFi Signal"
    update_interval: 60s
  - platform: cse7766
    current:
      name: "Sonoff S31 Current"
      accuracy_decimals: 1
    voltage:
      name: "Sonoff S31 Voltage"
      accuracy_decimals: 1
    power:
      name: "Sonoff S31 Power"
      accuracy_decimals: 1
      id: my_power
  - platform: total_daily_energy
    name: "Sonoff S31 Daily Energy"
    power_id: my_power

switch:
  - platform: gpio
    name: "Sonoff S31 Relay"
    pin: GPIO12
    id: relay
    restore_mode: ALWAYS_ON

time:
  - platform: sntp
    id: my_time

status_led:
  pin:
    number: GPIO13
    inverted: True
```
