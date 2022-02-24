# Sensors

## Temperature

[**Dallas DS18B20**](https://esphome.io/components/sensor/dallas.html)

<img align="right" src="https://github.com/peca2345/ESPHome-code-examples/blob/main/images/sensors/DA18B20.png?raw=true">

```
dallas: 
  - pin: GPIO12 # You can use any input pin
    update_interval: 60s
sensor:    
  - platform: dallas 
    name: "test_dallas"
    address: 0xC106219415E16428 # get from log
    id: test_dallas
    unit_of_measurement: "°C" 
```


## WATTMETER

[**PZEM-004T AC 100A**](https://esphome.io/components/sensor/pzemac.html)

ESP8266 has only one uart and it uses a logger.
If you want to use uart for pzem, disable the logger.

<img align="right" src="https://github.com/peca2345/ESPHome-code-examples/blob/main/images/sensors/pzem-004t-100A.png?raw=true">

```
logger:
  level: NONE
  hardware_uart: UART1
uart: # 
  rx_pin: GPIO3
  tx_pin: GPIO1
  baud_rate: 9600
sensor:
  - platform: pzemac # PZEM-004T uart
    update_interval: 60s
    current:
      name: "test_current"
    voltage:
      name: "test_voltage"
    energy:
      name: "test_energy"
    power:
      name: "test_power"
     # id: pzem_energy
    frequency:
      name: "test_frequency"
    power_factor:
      name: "test_power_factor"
  
```

[**Dallas DS18B20**](https://esphome.io/components/sensor/uptime.html)

```
sensor:
  - platform: uptime #sensor
    id: test_uptime
    name: "test_uptime"
    update_interval: 60s
    filters:
      - lambda: return x / 3600;
    unit_of_measurement: "h"
```
