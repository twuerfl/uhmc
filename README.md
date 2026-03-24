# UHMC – Underfloor Heating Manifold Controller

**UHMC** (Underfloor Heating Manifold Controller) is a modular, ESP32-based controller designed for precise regulation of underfloor heating circuits. It integrates advanced control features while remaining cost-efficient and flexible for home automation setups.

---

## Features

- **Microcontroller:** ESP32-WROOM-32E
- **Connectivity:**
  - Ethernet via LAN8720A **OR** WIFI
  - Optional USB via CP2102N (default not populated to reduce cost)
- **Heating Circuit Control:**
  - 12 heating circuits (loops) total
  - Circuits 11 and 12 share two outputs for double current capacity
- **Driver Hardware:**
  - 2 × TPL7407LAPW motor drivers
  - Each driven via a SN74HC595PWR shift register
- **I²C Expansion:**
  - TCA9548AMRGER I²C multiplexer
  - Supports 8 separate I²C inputs
- **Firmware:** ESPHome

---

## Hardware Overview

| Component | Purpose |
|-----------|---------|
| ESP32-WROOM-32E | Main controller |
| LAN8720A | Ethernet interface |
| CP2102N | Optional USB for programming/debugging |
| TPL7407LAPW | 7-channel motor drivers for valve actuation |
| SN74HC595PWR | Shift registers to extend GPIOs for TPL7407LAPW |
| TCA9548AMRGER | I²C multiplexer for up to 8 I²C inputs |

---

## System Architecture
ESP32
└─> SN74HC595 ──> TPL7407LAPW ──> Heating Circuits 1-12
    TCA9548AM ──> I²C Sensors
    LAN8720A ──> Ethernet
    CP2102N ──> Optional USB


- Heating circuits 11 and 12 are paralleled for higher current capacity.
- ESPHome handles PID control, sensor input, and automation integration.

---

## Features in ESPHome

- Supports up to 12 heating circuits with PWM control
- I²C sensor integration via TCA9548 multiplexer
- Optional integration with Home Assistant
- Ethernet connectivity for remote monitoring and updates
- Modular configuration allowing flexible re-assignment of heating circuits

---

## License

CC BY-NC-SA 4.0
https://creativecommons.org/licenses/by-nc-sa/4.0/

---

## Notes

- USB interface is optional to save cost; populated only if needed.
- Firmware is configured via ESPHome YAML files for easy customization.
