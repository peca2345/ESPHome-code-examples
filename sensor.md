# Sensors

[**TEMPERATURE - Dallas DS18B20**](https://esphome.io/components/sensor/dallas.html)

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

[**POWER SENSOR - PZEM-004T AC 100A**](https://esphome.io/components/sensor/pzemac.html)

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

[**POWER SENSOR - CSE7766**](https://esphome.io/components/sensor/cse7766.html)

```
sensor:
  - platform: cse7766
    current:
      name: "test_current"
    voltage:
      name: "test_voltage"
    power:
      name: "test_power"
      id: power

  - platform: total_daily_energy
    name: "test_daily_energy"
    power_id: power 
    filters:
      - multiply: 0.001
    unit_of_measurement: kWh
    accuracy_decimals: 1 
```   

[**TIMEUP**](https://esphome.io/components/sensor/uptime.html)

```
sensor:  
  - platform: uptime
    id: uptime
    name: "test_uptime"
    update_interval: 60s
    filters:
      - lambda: return x / 3600;
    unit_of_measurement: "h"
```

[**WIFI SIGNAL**](https://esphome.io/components/sensor/wifi_signal.html)

```
sensor:  
  - platform: wifi_signal #sensor
    name: "test_wifi_signal"
    update_interval: 60s     
```

[**TEMPLATE**](https://esphome.io/components/sensor/template.html)

```
sensor:  
  - platform: template 
    id: "fan_speed"
    name: test_fan_speed
    update_interval: 1s
    accuracy_decimals: 0
    lambda: |-
      return id(fan_pwm).speed; #get value from fan_pwm
```



[**ADC**](https://esphome.io/components/sensor/adc.html)

```
sensor:
  - platform: adc
    pin: A0 # 0-3.3V
    name: "test_car_voltage"
    id: adc_voltage
    update_interval: 1s
    filters:
      - multiply: 64.68 #
      - median:
          window_size: 10
          send_every: 5
          send_first_at: 1
      - calibrate_polynomial:
          degree: 2
          datapoints:
            - 10.04309 -> 10
            - 10.61156 -> 10.50
            - 11.05371 -> 11
            - 11.55902 -> 11.5
```   

