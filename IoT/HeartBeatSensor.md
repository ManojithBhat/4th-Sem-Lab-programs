## 2. Heart Beat Sensor

### Code 

``` 
#include <PulseSensorPlayground.h>

// Create an instance of the PulseSensorPlayground class
PulseSensorPlayground pulseSensor;

const int pulsePin = A0; // Analog pin where the pulse sensor is connected

void setup() {
  Serial.begin(9600);

  // Initialize the PulseSensorPlayground library
  pulseSensor.analogInput(pulsePin);
  pulseSensor.setThreshold(550); 
  pulseSensor.begin();
}

void loop() {
  // Read the value from the sensor
  int signal = pulseSensor.getBeatsPerMinute();
 
  // Print the heart rate if it is valid
  if (signal > 0) {
    Serial.print("Heart Rate: ");
    Serial.print(signal);
    Serial.println(" bpm");
  } else {
    Serial.println("No pulse detected.");
  }

  // Delay for 1 second
  delay(1000);
}

```

### method

* Install PulseSensor Playground library from the library manager.

### Connections 
* Heart beat sensor has 3 pins, analog pin, ground and vcc, connect the analog pin to A0
