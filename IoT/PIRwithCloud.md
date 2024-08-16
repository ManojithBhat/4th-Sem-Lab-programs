## 5 Object Detection using PIR sensor and LED interfacing with RaspberryPi

### Code without cloud
This is the one that is there for lab test 

```python
import time
import RPi.GPIO as GPIO

pir_pin = 12
led = 11
GPIO.setmode(GPIO.BOARD)
GPIO.setup(pir_pin,GPIO.IN)
GPIO.setup(led,GPIO.OUT)

try:
    print("PIR sensor test (ctrl +c to exit ")
    time.sleep(2)
    print("Ready")
   
    while True:
        if GPIO.input(pir_pin):
            print("Motion detected")
            GPIO.output(led,GPIO.HIGH)
            time.sleep(2)
            GPIO.output(led,GPIO.LOW)
        time.sleep(1)
except KeyboardInterrupt:
    print("Exit..")
       
finally :
    GPIO.cleanup()
```

### Code 

``` python
import http.client     #uses classes  for http client side
import urllib.parse    #parses URL string and uses http url scheme  
import time
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
GPIO.setup(7, GPIO.IN)
GPIO.setup(18, GPIO.OUT)
GPIO.setwarnings(False)
key = "76I4VO9R18ABOURD"  # Put your API Key here
def PIR():
    while True:
        if GPIO.input(7):         #If there is a movement, PIR sensor gives input to GPIO 16
             GPIO.output(18, True)
             print("object detected")
           #Output given to Buzzer through GPIO 18  
             time.sleep(5)           #Buzzer turns on for 1 second
        else:
             GPIO.output(18, False)
             print("no detection")
             time.sleep(5)
      #  time.sleep(0.1)
        Intrusion = (GPIO.input(7))
        params = urllib.parse.urlencode({'field1':Intrusion, 'key':key })
        headers = {"Content-typZZe": "application/x-www-form-urlencoded","Accept": "text/plain"}
        #create instances that connect to the HTTP server at the same host and port
        conn = http.client.HTTPConnection("api.thingspeak.com:80")
        try:
            conn.request("POST", "/update", params, headers)
            response = conn.getresponse()
            print(Intrusion)
            print(response.status, response.reason)
            data = response.read()
            conn.close()
        except:
            print("connection failed")
        break
if __name__ == "__main__":
        while True:
                PIR()

```

### methodolgy 
* Connect the two pins of LED and PIR to the pins of Raspberry Pi. 
