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

[**TEMPERATURE/HUMIDITY - DHT**](https://esphome.io/components/sensor/dht.html)

DHT sensor do not have good measurement accuracy!

Supported device: DHT11, DHT22, AM2302, RHT03, SI7021 

<img align="right" src="https://github.com/peca2345/ESPHome-code-examples/blob/main/images/sensors/DHT.png?raw=true">

```
sensor:
  - platform: dht
    pin: GPIO2
    temperature:
      name: "test_DHT_temperature"
      filters:
        - calibrate_linear:
            # Map 0.0 (from sensor) to 0.0 (true value)
            - 6.5 -> 0.0
            - 19.5 -> 13
    humidity:
      name: "test_DHT_humidity"
    update_interval: 60s
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

[**ADC VOLTAGE METER**](https://esphome.io/components/sensor/adc.html)

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

[**PULSE METER**](https://esphome.io/components/sensor/pulse_meter.html)

This configuration was used to measure pulses from the reed contact of the water flow meter.

TUTORIAL: [github](https://esphome.io/components/sensor/pulse_meter.html)

```
sensor:
  - platform: pulse_meter
    pin:
      number: GPIO5
      mode: INPUT_PULLUP
    unit_of_measurement: 'pulse'
    name: 'test_water_pulse_meter'
    icon: 'mdi:water'
    internal_filter: 100ms
    filters:
      - multiply: 0.5
    total:
      name: 'test_water_total'
      icon: 'mdi:water'
      unit_of_measurement: 'l'
      id: total
      filters:
      - multiply: 0.5

  - platform: total_daily_energy
    name: "test_water_total_daily"
    power_id: total  
    unit_of_measurement: l
```   
