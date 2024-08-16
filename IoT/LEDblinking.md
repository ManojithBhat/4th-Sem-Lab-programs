# Set up timer and delay for each of the LED lights using arduino 

###   Code 

``` c
const int led1 = 11;
const int led2 = 12;
const int led3 = 13;

void setup() {
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
}

void loop() {
  digitalWrite(led1, HIGH);
  delay(1000);
  digitalWrite(led1, LOW);
  digitalWrite(led2, HIGH);
  delay(2000);
  digitalWrite(led2, LOW);
  digitalWrite(led3, HIGH);
  delay(3000);
  digitalWrite(led3, LOW);
}


```
