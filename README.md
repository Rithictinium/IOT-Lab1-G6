# IOT-Lab1-G6

# ESP32 Telegram Bot – Temperature Monitor & Relay Control

This project implements a Telegram bot running on ESP32/ESP8266 to monitor a **DHT22 sensor** (temperature/humidity) and control a **relay module**.  
It supports bot commands, automatic alerts, and Wi-Fi auto-reconnect.  

---

## Features (Tasks)

- **Task 1 – Sensor Read & Print (10 pts)**
  - Reads DHT22 sensor every 5 seconds.
  - Prints temperature and humidity with 2 decimals in the serial monitor.

- **Task 2 – Telegram Send (15 pts)**
  - Implements `send_message()` to send messages to a Telegram group.

- **Task 3 – Bot Commands (15 pts)**
  - `/status` → reports current temperature, humidity, and relay state.
  - `/on` → turns relay ON.
  - `/off` → turns relay OFF.

- **Task 4 – Auto Behavior (20 pts)**
  - No automatic messages while **T < 30 °C**.
  - If **T ≥ 30 °C and relay is OFF**, sends alert every 5 s until `/on` is received.
  - After `/on`, alerts stop.
  - If **T drops < 30 °C**, relay turns OFF automatically and one-time **“auto-OFF”** notice is sent.

- **Task 5 – Robustness (10 pts)**
  - Auto-reconnects to Wi-Fi if dropped.
  - Handles Telegram HTTP errors gracefully (skips cycle instead of crashing).
  - Avoids crashing on DHT `OSError` (skips bad reading).

- **Task 6 – Documentation (30 pts)**
  - This README + wiring diagram + screenshots/video.

---

## Hardware & Wiring

### Components
- ESP32 (or ESP8266)
- DHT22 sensor
- Relay module (to control external load, e.g. fan)
- Breadboard + jumper wires
- Wi-Fi network

### Wiring Diagram

| ESP32 Pin | Connected To      |
|-----------|------------------|
| 3.3V      | DHT22 VCC        |
| GND       | DHT22 GND + Relay GND |
| GPIO4     | DHT22 Data       |
| GPIO2     | Relay IN         |
| 5V        | Relay VCC        |

*Insert your wiring photo here*  

---

## Configuration

Edit the following in the Python script before flashing:

```python
WIFI_SSID     = "your-wifi-ssid"
WIFI_PASSWORD = "your-wifi-password"

BOT_TOKEN     = "your-telegram-bot-token"
ALLOWED_CHAT_IDS = {-1001234567890}  # replace with your group or user chat ID
