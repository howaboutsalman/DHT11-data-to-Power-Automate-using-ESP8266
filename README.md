# 🌡️ ESP8266 DHT11 Webserver + Microsoft Flow Integration

Dies ist ein Arduino-Projekt, das Temperatur- und Luftfeuchtigkeitsdaten von einem **DHT11-Sensor** liest, sie auf einer lokalen Website anzeigt **und bei bestimmten Bedingungen an einen Microsoft Logic Flow (Webhook)** sendet.

## 📦 Features

- Live Temperatur- & Luftfeuchtigkeitsanzeige im Browser
- ESP8266 AsyncWebServer für ultraschnelles Webinterface
- Wenn Temperatur > 30°C → automatischer HTTP POST an Microsoft Flow / Power Automate
- Minimaler Stromverbrauch & Autonomer Betrieb

## 🧠 Voraussetzungen

- NodeMCU ESP8266 (z. B. LOLIN D1 Mini oder ähnliches)
- DHT11 (oder DHT22, musst nur `#define DHTTYPE` ändern)
- Jumper Kabel
- Micro-USB-Kabel

## 🔧 Arduino IDE Setup

1. **ESP8266 Board installieren:**
   - File > Preferences > Additional Board URLs:
     ```
     http://arduino.esp8266.com/stable/package_esp8266com_index.json
     ```
   - Tools > Board > Board Manager > "ESP8266" suchen & installieren.

2. **Folgende Libraries installieren:**
   - `ESPAsyncWebServer`
   - `ESPAsyncTCP`
   - `DHT sensor library` von Adafruit
   - `Adafruit Unified Sensor`
   - `ESP8266WiFi`, `ESP8266HTTPClient`, `WiFiClientSecureBearSSL` (meist schon vorhanden)

## ⚙️ Verkabelung

| DHT11-Pin | NodeMCU (ESP8266) |
|----------:|------------------:|
| VCC       | 3.3V              |
| GND       | G                 |
| DATA      | D1 (GPIO5)        |

## 🛠️ Code Setup

1. Öffne den Sketch in der Arduino IDE.
2. Ändere folgende Variablen mit deinen Daten:

```cpp
const char* ssid = "your SSID";
const char* password = "your Password";
String FlowUrl = "https://<dein_logic_app_url>";
```

3. Wähle unter *Tools > Board*: dein ESP8266-Modell (z. B. "NodeMCU 1.0").
4. Hochladen & starten.

## 🌍 Webserver

Nach erfolgreicher Verbindung mit dem WLAN kannst du im **Serial Monitor** (115200 Baud) die lokale IP-Adresse sehen.  
Öffne diese IP in deinem Browser → du siehst eine Live-Webseite mit Temperatur und Luftfeuchtigkeit.

## 🔄 Webhook-Trigger (Microsoft Flow)

Wenn die Temperatur über **30°C** geht, wird ein JSON-Request wie folgt gesendet:

```json
{
  "temperature": 32.5
}
```

Du musst deinen Flow auf "manuellen HTTP Trigger" setzen und die URL inkl. Token in `FlowUrl` eintragen.

## 🧠 Tipp

Wenn du `DHT22` oder `DHT21` nutzt, einfach in diesem Abschnitt ändern:

```cpp
#define DHTTYPE    DHT11
// zu z. B.
// #define DHTTYPE    DHT22
```

## 💬 Kontakt

Wenn du Fragen hast, slide gerne in die DMs – oder tweak den Code nach deinem Style 🛠️🔥
