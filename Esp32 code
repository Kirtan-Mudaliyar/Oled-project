#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include "BluetoothSerial.h"

BluetoothSerial SerialBT;

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

// ---------- Custom 16x16 Icons ----------
const unsigned char bell_bitmap [] PROGMEM = {
  0x00, 0x00, 0x0C, 0x00, 0x12, 0x00, 0x21, 0x00,
  0x21, 0x00, 0x21, 0x00, 0x21, 0x00, 0x12, 0x00,
  0x1E, 0x00, 0x0C, 0x00, 0x0C, 0x00, 0x3F, 0xC0,
  0x3F, 0xC0, 0x00, 0x00, 0x0C, 0x00, 0x0C, 0x00
};

const unsigned char battery_bitmap [] PROGMEM = {
  0xFF, 0xFC, 0x80, 0x04, 0xBE, 0xF4, 0xBE, 0xF4,
  0xBE, 0xF4, 0xBE, 0xF4, 0xBE, 0xF4, 0xBE, 0xF4,
  0xBE, 0xF4, 0xBE, 0xF4, 0xBE, 0xF4, 0x80, 0x04,
  0xFF, 0xFC, 0x3C, 0xF0, 0x3C, 0xF0, 0x00, 0x00
};

const unsigned char alarm_bitmap [] PROGMEM = {
  0x3C, 0x3C, 0x42, 0x42, 0x81, 0x81, 0x95, 0xA5,
  0xA5, 0x95, 0x81, 0x81, 0x42, 0x42, 0x3C, 0x3C,
  0x18, 0x18, 0x24, 0x24, 0x42, 0x42, 0x81, 0x81,
  0x81, 0x81, 0x42, 0x42, 0x3C, 0x3C, 0x00, 0x00
};

// New 16x16 "Waiting" icon (Hourglass)
const unsigned char waiting_bitmap [] PROGMEM = {
  0x7E, 0x7E, 0x42, 0x42, 0x24, 0x24, 0x18, 0x18,
  0x18, 0x18, 0x24, 0x24, 0x42, 0x42, 0x7E, 0x7E,
  0x7E, 0x7E, 0x42, 0x42, 0x24, 0x24, 0x18, 0x18,
  0x18, 0x18, 0x24, 0x24, 0x42, 0x42, 0x7E, 0x7E
};
// ----------------------------------------

bool dataReceived = false;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("SmartGlass");  // Bluetooth name
  Wire.begin(21, 22);

  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println(F("SSD1306 allocation failed"));
    for (;;);
  }

  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(32, 10);
  display.println("Waiting...");
  display.drawBitmap(56, 30, waiting_bitmap, 16, 16, SSD1306_WHITE);
  display.display();
}

void loop() {
  if (SerialBT.available()) {
    dataReceived = true;

    String incoming = "";
    while (SerialBT.available()) {
      char c = SerialBT.read();
      incoming += c;
      delay(5);
    }

    incoming.trim();
    Serial.println("Received:\n" + incoming);

    display.clearDisplay();

    int firstBreak = incoming.indexOf('\n');
    int secondBreak = incoming.indexOf('\n', firstBreak + 1);

    if (firstBreak > 0 && secondBreak > 0) {
      String timePart = incoming.substring(0, firstBreak);
      String batteryPart = incoming.substring(firstBreak + 1, secondBreak);
      String notifPart = incoming.substring(secondBreak + 1);

      display.setTextSize(1);
      display.setCursor(0, 0);
      display.println(timePart);

      display.setCursor(0, 16);
      display.println(batteryPart);

      display.setCursor(0, 32);
      display.println(notifPart);

      // Draw Emoji Icons (bottom center)
      int iconY = 48;
      display.drawBitmap(16, iconY, bell_bitmap, 16, 16, SSD1306_WHITE);
      display.drawBitmap(56, iconY, battery_bitmap, 16, 16, SSD1306_WHITE);
      display.drawBitmap(96, iconY, alarm_bitmap, 16, 16, SSD1306_WHITE);
    } else {
      display.setTextSize(1);
      display.setCursor(0, 0);
      display.println("Invalid Data Format");
    }

    display.display();
  } else if (!dataReceived) {
    // Show "Waiting" screen only until first valid data received
    display.clearDisplay();
    display.setTextSize(1);
    display.setCursor(32, 10);
    display.println("Waiting...");
    display.drawBitmap(56, 30, waiting_bitmap, 16, 16, SSD1306_WHITE);
    display.display();
  }
}
