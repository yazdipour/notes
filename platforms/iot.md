# IOT

## Resources

- http://marchisformakers.com/
- https://www.hackster.io/ThothLoki/play-video-with-python-and-gpio-a30c7a

## Shops

- http://yazdkit.com/

## Tools

- https://azure-samples.github.io/raspberry-pi-web-simulator/
- [Fritzing](http://fritzing.org/home/) is an open-source hardware initiative that makes electronics accessible as a creative material for anyone

## Sensors

### Ultrasonic

![hc-sr04](https://cdn-images-1.medium.com/max/1600/1*ODZShyJXz7Hi_J9VEbGa-Q.jpeg)

```cpp
const int anPin = 0;
long anVolt, cm;

void setup() {
   Serial.begin(9600);
}

void loop() {  
   anVolt = analogRead(anPin);
   cm = anVolt/2;
   delay(100);
}
```

or

```cpp
long readUltrasonicDistance(int triggerPin, int echoPin) // ex (7,7)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}
```

### Photoresistor

![Photoresistor](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/LDR_1480405_6_7_HDR_Enhancer_1.jpg/302px-LDR_1480405_6_7_HDR_Enhancer_1.jpg)

### Servo motor

![servo motor](https://cdn-learn.adafruit.com/assets/assets/000/002/304/large1024/learn_arduino_knob.jpg?1396781531)

```cpp
#include <Servo.h>
int servoPin = 9;
int angle = 0;   // servo position in degrees
Servo servo;  
void setup() {servo.attach(servoPin);}
void loop() {
    // scan from 0 to 180 degrees
    for(angle = 0; angle < 180; angle++){
        servo.write(angle);
        delay(15);
    }
    // now scan back from 180 to 0 degrees
    for(angle = 180; angle > 0; angle--){
        servo.write(angle);
        delay(15);
    }
}
```

### Potentiometers

A potentiometer is a three-terminal resistor with a sliding or rotating contact that forms an adjustable voltage divider. 

![Potentiometers](https://cdn.instructables.com/F20/QNR1/IQTTBQS1/F20QNR1IQTTBQS1.MEDIUM.jpg)