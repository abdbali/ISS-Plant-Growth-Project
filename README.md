# ISS Plant Growth Project

<img width="707" height="1000" alt="ABV" src="https://github.com/user-attachments/assets/097b8fb1-c523-48c7-a305-0fa4d965d4c6" />


### Project Description

This project simulates the concept of growing plants in the ISS (International Space Station) environment using an Arduino-based STEM project. Students will learn about photosynthesis and plant life cycles while developing basic electronics and robotics skills.

### Objectives

* Understand the plant life cycle
* Simulate the process of photosynthesis
* Use Arduino and robotic systems for sensor-based automation

### Required Materials

* Arduino Uno
* DHT11/DHT22 temperature and humidity sensor
* LDR (light sensor)
* Servo motor (watering simulation)
* LED (sunlight simulation)
* 220Ω resistors
* Jumper wires

### Circuit Diagram

* Arduino in the center
* LDR: 5V -> leg1, A0 -> leg2 and 10kΩ resistor -> GND
* DHT11: VCC -> 5V, DATA -> D2, GND -> GND
* LED: D9 -> long leg, short leg -> 220Ω resistor -> GND
* Servo: Signal -> D6, VCC -> 5V, GND -> GND

### Arduino Code

```cpp
#include <DHT.h>
#include <Servo.h>

#define DHTPIN 2
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

#define LIGHT_PIN A0
#define LED_PIN 9
#define SERVO_PIN 6

Servo waterPump;

void setup() {
  Serial.begin(9600);
  dht.begin();
  pinMode(LIGHT_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
  waterPump.attach(SERVO_PIN);
  waterPump.write(0);
}

void loop() {
  int lightValue = analogRead(LIGHT_PIN);
  Serial.print("Light: ");
  Serial.println(lightValue);

  float temp = dht.readTemperature();
  float hum = dht.readHumidity();
  Serial.print("Temperature: ");
  Serial.print(temp);
  Serial.print(" C, Humidity: ");
  Serial.print(hum);
  Serial.println(" %");

  if(lightValue < 500) {
    digitalWrite(LED_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
  }

  if(hum < 40) {
    waterPump.write(90);
    delay(2000);
    waterPump.write(0);
  }

  delay(2000);
}
```

### Science Connection

* **LED (Light)**: Simulates the sunlight needed for photosynthesis.
* **Temperature & Humidity**: Provides necessary environmental conditions for plant growth.
* **Servo (Watering)**: Simulates the water cycle for plants.

### Student Activity

Students observe sensor data to report which conditions support better plant growth, integrating both biology and STEM skills.

---

## File Structure

```
ISS-Plant-Project/
│
├─ README.md          # Project description and usage guide
├─ Arduino_Code/
│   └─ ISS_Plant.ino  # Arduino code
├─ Circuit/
│   └─ ISS_Plant_Circuit.png  # Wokwi circuit screenshot
└─ Docs/
    └─ Science_Notes.pdf  # Notes linking photosynthesis and plant life cycle
```

---

This project can be simulated in Wokwi and tested on an Arduino board.
