# IoT Air Quality Monitoring and Alert System

An undergraduate research project that uses an ESP32 sensor node to monitor indoor environmental conditions and send readings to a local Home Assistant server. The system combines sensor acquisition, MQTT messaging, dashboard visualization and mobile alerts for classroom and student-living environments.

**Award:** Second Prize, University-level Student Research Competition  
**My role:** Primary contributor within a five-member research team.
**Main contributions:**
- Developed the project concept.
- Drew circuit schematics and system block diagrams.
- Purchased electronic components.
- Assembled the prototype on a breadboard and connected the components through wiring.
**Current status:** Functional prototype with dashboard integration and documented alert tests.

## Project Overview

The system brings temperature, humidity and air-quality indicators into one interface so users can observe changes and receive threshold-based notifications. An initial Arduino UNO WiFi Rev2 and LM35 temperature-monitoring prototype was extended into an ESP32 system with multiple sensors and Home Assistant integration.

## Hardware and Monitored Parameters

| Component | Function | Interface |
| --- | --- | --- |
| ESP32 | Collect readings and send data over Wi-Fi | Wi-Fi / MQTT |
| DHT11 | Temperature and relative humidity | Digital single-bus |
| SGP30 | Equivalent CO2 (eCO2) and total volatile organic compounds (TVOC) | I2C |
| MQ135 | Relative gas-level indication | Analog / ADC |
| Buzzer / LED | Local threshold-based warning | GPIO |

The three sensors provide five monitored values. The SGP30's eCO2 is an estimated CO2-equivalent value, while MQ135 readings are used as a relative gas indicator.

## System Architecture

**Sensors → ESP32 firmware → JSON messages over Wi-Fi/MQTT → Mosquitto broker → Home Assistant dashboards and automations**

Home Assistant OS runs locally in Oracle VirtualBox. The ESP32 and server communicate over the local network, and the dashboard presents current readings alongside historical charts.

## Implemented Features

- **Embedded data acquisition:** C/C++ firmware reads the DHT11, SGP30 and MQ135, packages their values into JSON messages and publishes them through MQTT.
- **Dashboard monitoring:** Home Assistant displays the five monitored parameters and their history. HACS components, including Mushroom, Card-mod and chart cards, support the interface.
- **Air-quality status:** Jinja2-based scoring combines the monitored values into a dashboard status with changing colors and icons.
- **Mobile notifications:** Home Assistant automations send parameter-specific alerts when configured thresholds are exceeded.
- **Recovery confirmation:** A recovery trigger must remain below its configured threshold for 10 seconds. The automation also checks the remaining parameters before sending an all-clear notification, helping limit repeated alert/recovery messages near a threshold.
- **Local warning:** The firmware controls a buzzer/LED output for configured abnormal conditions.

## Testing and Results

The report compares ESP32 Serial Monitor readings with Home Assistant values to check the sensor-to-dashboard data path. It also documents changing sensor readings, dashboard warning states and mobile notifications during test scenarios.

Observed outcomes include:

- Matching sampled values between Serial Monitor and the dashboard.
- Historical charts showing changes in humidity, eCO2, TVOC and MQ135 readings.
- Dashboard color changes and mobile alerts when configured warning conditions were met.
- Recovery notifications after the configured delay and cross-check conditions were satisfied.

## Scope and Further Development

Validation focused on functional integration and alert behavior. Measurement accuracy against a calibrated reference instrument has not been established by the reported tests. Further work can include reference-based calibration and expansion from the prototype node to monitoring multiple rooms.

## Technology Stack

C/C++, ESP32, Arduino IDE, DHT11, SGP30, MQ135, GPIO, ADC, I2C, Wi-Fi, MQTT, JSON, Mosquitto, Home Assistant, Jinja2, HACS and VirtualBox.
## Technical Report

[Read the full technical report (PDF)](report.pdf)

## Home Assistant Dashboard

Scan the QR code below to open my Home Assistant dashboard.

<img src="TRAM%20NGHIEN%20CUU%20KHOA%20HOC%20-%20IOT.png"
     alt="QR code linking to the Home Assistant dashboard"
     width="220">
