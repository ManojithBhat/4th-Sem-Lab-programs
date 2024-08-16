## 7. Water Level Sensor

### Code 

``` python
import RPi.GPIO as GPIO
import smtplib
from email.mime.text import MIMEText
import time

# Email settings
EMAIL_ADDRESS = 'xyz@gmail.com'  # Your email address
EMAIL_PASSWORD = ' '   # Your email password
TO_EMAIL = ''    # Recipient's email address

# Set up GPIO
WPIN = 4  # GPIO pin for PIR sensor
BUZZERPIN=17
GPIO.setmode(GPIO.BCM)
GPIO.setup(WPIN, GPIO.IN)
GPIO.setup(BUZZERPIN, GPIO.OUT)

# Function to send email notification
def send_email():
    msg = MIMEText('Motion detected!')
    msg['Subject'] = 'Alert: Motion Detected'
    msg['From'] = EMAIL_ADDRESS
    msg['To'] = TO_EMAIL

    try:
        with smtplib.SMTP_SSL('smtp.gmail.com', 465) as server:
            server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
            server.send_message(msg)
            print("Email sent successfully")
    except Exception as e:
        print(f"Failed to send email: {e}")

# Main loop
try:
    print("Water Sensor with email (CTRL+C to exit)")
    time.sleep(2)  # Warm-up time for PIR sensor
    print("Ready")

    while True:
        if GPIO.input(WPIN):  # If motion is detected
            print("Water sensor is wet!")
            GPIO.output(BUZZERPIN,True)
            send_email()
            time.sleep(5)  # Delay to avoid multiple detections
            GPIO.output(BUZZERPIN,False)
           
except KeyboardInterrupt:
    print("Program terminated")
finally:
    GPIO.cleanup()  # Clean up GPIO on exit

```

### methodolgy 
* The connections are asusual for any other sensor.
* In order to get ```EMAIL_PASSWORD``` we need to enable two factor authentication in your account.
* Go to settings > app password > generate app password and use it.
