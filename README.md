
# ⏰ ESP8266 DS3231 RTC Clock with OLED Display

This project demonstrates how to interface a DS3231 RTC module with an ESP8266 and display real-time clock data on an SSD1306 OLED display.

---

## 🚀 Features

- Real-time clock using DS3231 (high accuracy)
- OLED display output (SSD1306)
- Double-sized text for better readability
- Top 10% display margin for clean UI
- I2C communication (shared bus)

---

## 🧰 Components Required

- ESP8266 NodeMCU
- DS3231 RTC Module
- SSD1306 OLED Display (128x64, I2C)
- Jumper wires
- Breadboard

---

## 🔌 Circuit Connections

### DS3231 → ESP8266

| DS3231 | ESP8266 |
|--------|--------|
| VCC    | 3.3V   |
| GND    | GND    |
| SDA    | D2     |
| SCL    | D1     |

### OLED → ESP8266

| OLED | ESP8266 |
|------|--------|
| VCC  | 3.3V   |
| GND  | GND    |
| SDA  | D2     |
| SCL  | D1     |

> Both devices share the same I2C bus.

---

## 📦 Libraries Required

Install the following libraries via Arduino IDE:

- RTClib (by Adafruit)
- Adafruit SSD1306
- Adafruit GFX

---

## 💻 Code

```cpp
#include <Wire.h>
#include <RTClib.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);
RTC_DS3231 rtc;

#define TOP_MARGIN 7

void setup() {
  Serial.begin(115200);
  Wire.begin(D2, D1);

  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println("OLED not found");
    while (1);
  }

  if (!rtc.begin()) {
    Serial.println("RTC not found");
    while (1);
  }

  // Run once, then comment this line
  rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));

  display.clearDisplay();
  display.setTextSize(2);
  display.setTextColor(WHITE);
  display.setCursor(0, TOP_MARGIN);
  display.println("RTC OK");
  display.display();
  delay(2000);
}

void loop() {
  DateTime now = rtc.now();

  display.clearDisplay();
  display.setTextSize(2);

  display.setCursor(0, TOP_MARGIN);

  if (now.hour() < 10) display.print("0");
  display.print(now.hour());
  display.print(":");

  if (now.minute() < 10) display.print("0");
  display.print(now.minute());

  display.setCursor(0, TOP_MARGIN + 20);
  display.print("Sec:");

  if (now.second() < 10) display.print("0");
  display.print(now.second());

  display.display();

  delay(1000);
}
