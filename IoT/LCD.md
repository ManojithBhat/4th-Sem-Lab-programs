# Interface Arduino Uno to show network utilisation, cpu and disk usage on LCD

``` c
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("System Monitor");
  lcd.setCursor(0, 1);
  lcd.print("Initializing....");
  delay(2000);
}

void loop() {
  float networkUtilization = getNetworkUtilization();
  float cpuLoad = getCPULoad();
  float diskSpace = getDiskSpace();

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Network : ");
  lcd.print(networkUtilization);
  lcd.print("%");

  lcd.setCursor(0, 1);
  lcd.print("CPU : ");
  lcd.print(cpuLoad);
  lcd.print("% Disk: ");
  lcd.print(diskSpace);
  lcd.print("GB");

  delay(5000);
}

float getNetworkUtilization() {
  return 50.5;
}

float getCPULoad() {
  return 30.2;
}

float getDiskSpace() {
  return 25.7;
}


```


### Methodology

* Install LiquidCrystall library from the library manager for using the above header .
