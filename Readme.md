# 🌡️ IR Thermostat — CH32V003

A portable, compact, low-power infrared thermometer based on the **CH32V003** microcontroller, featuring contactless temperature reading via the **MLX90614** sensor and an **I²C OLED SSD1306** display.

Built with **100% custom firmware** — HAL and sensor libraries written from scratch, with no dependency on third-party frameworks.

---

## ✨ Features

- 📡 Contactless infrared temperature reading via **MLX90614**
- 🖥️ **128x64 SSD1306 OLED** display over I²C
- 🔘 Single tactile button to trigger a reading
- 🌗 **Automatic brightness control** via a 5mm LDR (adjusts to ambient light)
- 🔋 **250mAh LiPo battery (503020)** for portable use
- ⚡ Charging via **TP4056** with integrated battery protection (0.5C)
- 🔌 3-pin header (5V / GND / SWIO) for external power and programming

---

## 🧩 Hardware

| Component | Description |
|---|---|
| **MCU** | CH32V003 (RISC-V, low cost, low power) |
| **Temperature sensor** | MLX90614 (IR, I²C) |
| **Display** | SSD1306 OLED 128x64, I²C |
| **Light sensor** | 5mm LDR (automatic brightness control) |
| **Input** | 1x tactile button (start/reading) |
| **Power source** | 250mAh LiPo battery, 503020 |
| **Charger** | TP4056 with battery protection (over-charge/discharge/current) |
| **Charge rate** | 0.5C (~125mA) |
| **External connector** | 3-pin header — 5V, GND, SWIO |

---

## ⚠️ Important warnings

> **Read carefully before using or programming the device.**

### 🚫 Never flash the MCU while pressing the button
The **SWIO** pin (used for programming/debugging) shares the same **I/O line** as the tactile button. Pressing the button during flashing can cause a **bus conflict**, flashing failure, or undefined MCU behavior.

### 🚫 Never connect USB while powering via the external 5V header
The **TP4056** charger and the 3-pin header **have no isolation between power sources**. Powering the circuit simultaneously through **USB** and the **external header (5V)** can cause:
- Short circuit between power sources
- Unwanted reverse current
- Damage to the TP4056, the battery, or the MCU

**Use only one power source at a time.**

---

## 🌡️ Operating conditions

- **Maximum recommended ambient temperature:** ~40 °C
- Above this limit, the MLX90614 sensor accuracy and the LiPo battery lifespan may be affected.

---

## 🔋 Battery and charging

| Parameter | Value |
|---|---|
| Capacity | 250 mAh |
| Model | 503020 (LiPo) |
| Charge rate | 0.5C (~125 mA) |
| Charge controller | TP4056 |
| Protection | Over-charge, over-discharge, and over-current |

---

## 💻 Firmware

The firmware is **built entirely from scratch**, without relying on any third-party HAL (such as the official WCH HAL), including:

- **Custom HAL** for GPIO, I²C, ADC, and timing on the CH32V003
- **Custom library** for MLX90614 communication
- **Custom library** for SSD1306 display control
- LDR reading routine with a brightness adjustment curve (PWM/lookup table)
- Simple state machine: `standby → reading → display → standby`

### repository structure

```
/firmware
  /*COMING SOON*
/hardware
  /schematics
  /pcb
  /datasheets
/docs
README.md
LICENSE
```

---

## 🚀 Usage

1. Power the device via battery (or the external 5V header, **never both at the same time**).
2. Press the tactile button to start a temperature reading.
3. The temperature will be shown on the OLED display.
4. The display brightness adjusts automatically based on the ambient light detected by the LDR.

---

## 🛠️ Flashing

1. Connect the programmer (WCH-Link or compatible) to the 3-pin header (**5V / GND / SWIO**).
2. **Make sure the tactile button is not being pressed.**
3. Flash normally using your preferred tool (e.g., `wchisp`, MounRiver, OpenOCD with RISC-V support).

---

## 🤝 Contributing

Suggestions, fixes, and improvements are welcome via issues or pull requests.