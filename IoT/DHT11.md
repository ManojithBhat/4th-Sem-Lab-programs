# Measuring Temperature and Humidity of weather using the DHT11 Sensor with the raspberryPi

### Pre - work

* create virtual environment in new folder
* within the virtual environment execute following commands:
  * "pip install Adafruit-Blinka" (in order to use board)
  * "pip install adafruit-circuitpython-dht" (to use adafruit_dht)
* create python file (eg dht11.py) within the virtual environment folder
* open thonny, paste the below code in that python file and save
* run the code on the terminal within the virtual environment using python3 dht11.py

### Code 
``` python
import time
import board
import adafruit_dht

# Initialize the sensor
sensor = adafruit_dht.DHT11(board.D4, use_pulseio=False)

while True:
    try:
        temperature_c = sensor.temperature
        temperature_f = temperature_c * (9 / 5) + 32
        humidity = sensor.humidity

        print(f"Temp={temperature_c:0.1f}C, Temp={temperature_f:0.1f}F, Humidity={humidity:0.1f}%")

    except RuntimeError as error:
        print(f"Runtime error: {error.args[0]}")
        time.sleep(2.0)  # Delay before retrying

    except Exception as error:
        print(f"Unhandled exception: {error}")
        sensor.exit()
        break  # Exit the loop if there's a critical error

    time.sleep(1)

```

### Methodology 

* Make the required connections and run the python file.
