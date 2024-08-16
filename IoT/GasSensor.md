# Develope an USB powered gas detector with an LED display using arduino

### Code 

``` c
const int gasPin = A0;
const int ledPin = 13;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(gasPin,INPUT);
  Serial.begin(9600); 
}

void loop() {

  int gasValue = analogRead(gasPin);
  float voltage = gasValue * (5.0 / 1023.0); 

  Serial.print("Gas Value: ");
  Serial.print(gasValue);
  Serial.print("\tVoltage: ");
  Serial.println(voltage, 3); 


  if (voltage > 1.5) {
    digitalWrite(ledPin, HIGH);
    Serial.print("led on\n");
  } else {
    digitalWrite(ledPin, LOW); 
    Serial.print("led off\n");
  
  }

  delay(1000); 
}

```
