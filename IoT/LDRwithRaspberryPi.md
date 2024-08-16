# Smart lighting application with LDR and buzzer 

### Code

``` python

import time
import RPi.GPIO as GPIO  
import urllib.parse
import http.client
BUZZER_PIN = 33
LDR_PIN = 3
LED= 11


key = ""   # add thingspeak key here

def setup_gpio():
    GPIO.setmode(GPIO.BOARD)
    GPIO.setup(BUZZER_PIN, GPIO.OUT)  
    GPIO.setup(LDR_PIN, GPIO.IN)
    GPIO.setup(LED,GPIO.OUT)

def ldr():
    while True:
        ldr_value = GPIO.input(LDR_PIN) 
       
        if ldr_value == 1:
            print("High: Switch on buzzer")
            print("led ON")
            GPIO.output(LED,True)
        else:
            print("Low: Don't switch on buzzer")
            GPIO.output(BUZZER_PIN, False)
            print("led OFF")
            GPIO.output(LED,False)
       
        time.sleep(0.3)
       
        LDRData = ldr_value
        BuzzerData = 1 if ldr_value == 1 else 0
       
        params = urllib.parse.urlencode({'field1': LDRData, 'field2': BuzzerData, 'key': key})
        headers = {"Content-type": "application/x-www-form-urlencoded", "Accept": "text/plain"}
        conn = http.client.HTTPConnection("api.thingspeak.com", 80)
        try:
            conn.request("POST", "/update", params, headers)
            response = conn.getresponse()
            print(LDRData)
            print(BuzzerData)
            print(response.status, response.reason)
            data = response.read()
            conn.close()
        except Exception as e:
            print("Connection failed:", e)

if __name__ == "__main__":
    setup_gpio()  # Initialize GPIO once
    try:
        ldr()  # Start the LDR monitoring loop
    except KeyboardInterrupt:
        print("Program interrupted")
    finally:
        GPIO.cleanup()  # Clean up GPIO settings

```
### Methodology 
* There are 3 components - LDR, LED and Buzzer.
* Connect that to the pins of Raspberry Pi, open thingspeak - channel - take the id
