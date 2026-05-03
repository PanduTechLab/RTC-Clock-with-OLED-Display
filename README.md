
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


}
