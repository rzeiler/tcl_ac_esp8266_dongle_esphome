# TCL AC ESP8266 Dongle (ESPHome)

[![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-blue.svg)](https://esphome.io/)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Integration-orange.svg)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Integration of TCL air conditioners into Home Assistant via ESPHome using an ESP8266 Wi-Fi dongle replacement / modification.

---

## 🚀 Features
- **Local Control:** No cloud dependency, fully local communication via ESPHome and Home Assistant (Native API / MQTT).
- **Full Climate Control:** Supports turning the AC on/off, changing target temperature, fan speed, swing modes, and operating modes (Cool, Heat, Dry, Fan, Auto).
- **Real-time Feedback:** Monitors current room temperature and AC operational status.
- **Easy Integration:** Seamless auto-discovery in Home Assistant.

---

## 🛠️ Hardware Requirements
- **ESP8266 Microcontroller** (e.g., NodeMCU, Wemos D1 Mini or a custom ESP8266-based board matching the dongle form factor).
- **TCL Air Conditioner** featuring a compatible serial/UART interface/dongle port.
- Jumper wires / Level Shifter (if required by your specific AC model logic levels).
- USB cable or direct power supply via the AC indoor unit connector.

---

## 🔌 Wiring / Pinout

| ESP8266 Pin | TCL AC Interface Pin | Description |
| :--- | :--- | :--- |
| **3V3 / 5V** | VCC | Power Supply |
| **GND** | GND | Ground |
| **GPIOX (TX)** | RX | Transmit Data (UART) |
| **GPIOY (RX)** | TX | Receive Data (UART) |

> ⚠️ **Warning:** Double-check your wiring and voltage levels (3.3V vs 5V) before connecting the device to your air conditioner to avoid hardware damage.

---

## 📦 Installation & Setup

### 1. Prerequisites
Make sure you have **ESPHome** installed (either as a Home Assistant Add-on or standalone CLI).

### 2. Configuration yaml
   ```yaml
        external_components:
            - source:
                type: git
                url: https://github.com/rzeiler/tcl_ac_esp8266_dongle_esphome.git
                ref: main
                components: [tclac]
                refresh: 10min       
        
        uart:
            id: uart_bus
            tx_pin: {tx_pin}
            rx_pin: {rx_pin}
            baud_rate: 9600
            parity: EVEN

        climate:
            - platform: tclac
                id: tcl_custom_climate
                uart_id: uart_bus
                name: "Klimaanlage"