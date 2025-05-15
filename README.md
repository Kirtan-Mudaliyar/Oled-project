# 👓 Smart Glasses — ESP32-Based Wearable Display

## 🚀 Hands-Free Notifications | Real-Time Data | Bluetooth Control

Smart Glasses is a compact wearable device built on the **ESP32 microcontroller**, featuring an **OLED display** that receives and shows real-time **time**, **battery status**, and **mobile notifications** via **Bluetooth**.

This project is the result of a **collaborative effort across colleges**, combining hardware engineering and mobile app development to build a functional prototype for hands-free information display.

<br>
<hr>
<br>

## 💡 Key Features

- ✅ **Bluetooth SPP Data Transfer** (via Android App)
- ⏱️ Displays **real-time time**, **battery**, and **notifications**
- 📟 **128x64 OLED Display UI** with custom icons
- 👨‍🔧 Designed for low power and mobile use
- 🤝 Built collaboratively by students from multiple institutions

<br>
<hr>
<br>

## 🔧 Hardware Components

| Component           | Specification                     |
|---------------------|-----------------------------------|
| Microcontroller     | ESP32 Dev Board                   |
| Display             | OLED 128x64 I2C (Address: `0x3C`) |
| Communication       | Bluetooth Serial (SPP)            |
| Power Supply        | Rechargeable Battery or USB       |

<br>

### 🔌 Wiring Connections (ESP32 ↔ OLED)

| OLED Pin | ESP32 GPIO |
|----------|------------|
| VCC      | 3.3V       |
| GND      | GND        |
| SDA      | GPIO 21    |
| SCL      | GPIO 22    |

<br>
<hr>
<br>

## 📱 Mobile App Details

- 🔧 Built using **MIT App Inventor** *(alternatively Android Studio)*
- Sends data in the format:
  
```cpp
 10:45 AM
 Battery: 82%
 You have 2 new messages!
```

- Transmits over Bluetooth SPP to `SmartGlass` device name


## 📥 Download Mobile App Project (MIT App Inventor)

> 🔗 **[SmartGlassApp.aia](app/SmartGlassApp.aia)** — MIT App Inventor Source File  
Open at: [ai2.appinventor.mit.edu](https://ai2.appinventor.mit.edu/)

You can import this `.aia` file into MIT App Inventor to view or modify the app source.


<br>

### 🔋 Displayed Data (OLED Sections)

- **Top:** Time
- **Middle:** Battery Percentage
- **Bottom:** Notification Text
- **Footer Icons:**
- 🔔 Notification Bell
- 🔋 Battery Icon
- ⏰ Alarm Symbol

<br>
<hr>
<br>

## 💻 ESP32 Arduino Code Summary

- Uses `Adafruit_SSD1306`, `Adafruit_GFX`, and `BluetoothSerial` libraries
- Initializes OLED and waits for Bluetooth data
- Parses input into `Time`, `Battery`, and `Message` segments
- Displays icons and text using custom 16x16 bitmaps

```cpp
display.setCursor(0, 0);
display.println(timePart);
display.setCursor(0, 16);
display.println(batteryPart);
display.setCursor(0, 32);
display.println(notifPart);
```

<br>
🧠 "Waiting..." Mode
Before first Bluetooth message is received, the screen displays:

```cpp
Waiting...
[hourglass icon]
```

📜 License
Licensed under the MIT License — feel free to use, modify, and improve.

<br>

## 🙌 Contributors
- 👨‍💻 Developer : Mudaliyar Kirtan
- 🎓 Collaborator : Asmita Mudaliyar

