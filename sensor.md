# Sensor

## Temperature

**Dallas:**

<img align="right" src="https://github.com/peca2345/ESPHome-code-examples/blob/main/images/dallas.png?raw=true">

```
dallas: 
  - pin: GPIO12
    update_interval: 5s
sensor:    
  - platform: dallas 
    name: "test_dallas"
    address: 0xC106219415E16428 # get from log
    id: test_dallas
    unit_of_measurement: "°C" 
```

