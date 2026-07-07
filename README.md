# Esp32ScreenCYD
# Hardware Pin Mapping

## Overview
This document outlines the GPIO pin configuration for the ESP32-based hardware setup, including display, touch, storage, audio, and sensor interfaces.

---

## Signal Name Reference

SPI and peripheral signals often appear under different names across datasheets. This table helps cross-reference common alternatives:

| Original | Common Alternatives | Meaning |
|----------|---------------------|---------|
| **MISO** | SO, SDI, DI | Slave Out / Data In to Master |
| **MOSI** | SI, SDO, DO | Slave In / Data Out from Master |
| **SCK** | SCLK, CLK, SPI_CLK | Serial Clock |
| **CS** | SS, CE, NSS, SEL | Chip Select / Slave Select |
| **DC** | RS, D/C, CMD_DATA | Data/Command or Register Select |
| **RST** | RES, RESET | Reset |
| **IRQ** | INT, INT_PIN, IE | Interrupt Request |

---

## Core Function Pins

| Function | GPIO Pin |
|----------|----------|
| CLK      | 14       |

---

## ILI9341 LCD Display (HSPI)

| Signal | ESP32 Pin | Alternate Names | Notes                |
|--------|-----------|-----------------|----------------------|
| MISO   | 12        | SO, SDI, DI     |                      |
| MOSI   | 13        | SI, SDO, DO     |                      |
| SCK    | 14        | SCLK, CLK       |                      |
| CS     | 15        | SS, CE, NSS     |                      |
| DC     | 2         | RS, D/C         |                      |
| RST    | –         | RES, RESET      | Tied HIGH            |

---

## Touch Screen (VSPI)

| Signal | ESP32 Pin | Alternate Names |
|--------|-----------|-----------------|
| MISO   | 39        | SO, SDI         |
| MOSI   | 32        | SI, SDO         |
| SCK    | 25        | SCLK, CLK       |
| CS     | 33        | SS, CE          |
| IRQ    | 36        | INT, INT_PIN    |

---

## Micro-SD Card (Shared VSPI)

| Signal | ESP32 Pin | Alternate Names | Notes          |
|--------|-----------|-----------------|----------------|
| MISO   | 19        | SO, SDI         | Shared VSPI bus|
| MOSI   | 23        | SI, SDO         |                |
| SCK    | 18        | SCLK, CLK       |                |
| CS     | 5         | SS, CE          |                |

---

## Audio Output

| Component | Type    | Pin | Connector  |
|-----------|---------|-----|------------|
| Audio Out | DAC/PWM | 26  | 2-pin JST  |

---

## RGB LED

| Color | Pin | Active State |
|-------|-----|--------------|
| Red   | 4   | LOW          |
| Green | 16  | LOW          |
| Blue  | 17  | LOW          |

---

## Light Dependent Resistor (LDR)

| Component | Type       | Pin | Resolution  |
|-----------|------------|-----|-------------|
| LDR       | ADC Input  | 34  | 10-bit ADC1 |

---

## Exposed Headers

| Header Designation | Purpose              |
|--------------------|----------------------|
| P1                 | UART (JST connector) |
| P3                 | General I/O          |
| CN1                | General I/O          |

---

## Quick Reference Code Block

```cpp
// ILI9341 LCD (HSPI)
#define LCD_MISO  12  // SO, SDI
#define LCD_MOSI  13  // SI, SDO
#define LCD_SCK   14  // SCLK, CLK
#define LCD_CS    15  // SS, CE, NSS
#define LCD_DC    2   // RS, D/C

// Touch Screen (VSPI)
#define TOUCH_MISO 39  // SO
#define TOUCH_MOSI 32  // SI
#define TOUCH_SCK  25  // SCLK
#define TOUCH_CS   33  // SS
#define TOUCH_IRQ  36  // INT

// Micro-SD (VSPI)
#define SD_MISO  19
#define SD_MOSI  23
#define SD_SCK   18
#define SD_CS    5

// RGB LED (active-LOW)
#define LED_R 4
#define LED_G 16
#define LED_B 17

// Audio & Sensors
#define AUDIO_OUT 26   // DAC/PWM
#define LDR_PIN   34   // ADC1
