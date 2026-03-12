# FlightPanel-01 — Technical Pin Reference

**Project:** FlightPanel-01
**MCU:** ATmega32U4-A (TQFP-44) — U1
**Multiplexer:** CD74HC4067M 16-ch Analog Mux/Demux (SOIC-24) — U2
**Schematic tool:** KiCad EDA 9.0.7
**Date:** 2026-03-12

---

## Bill of Materials (Summary)

| Ref | Qty | Type | Description |
|-----|-----|------|-------------|
| U1 | 1 | ATmega32U4-A | Microcontroller, TQFP-44 |
| U2 | 1 | CD74HC4067M | 16-Channel Analog Multiplexer, SOIC-24 |
| SW1–SW8 | 8 | SW_SPST | Toggle switches (Single Pole Single Throw), THT |
| SW9–SW19 | 11 | SW_Push | Tactile push buttons 6 mm, THT |
| SW20 | 1 | RotaryEncoder_Switch | Rotary encoder with push button, Alps EC11E |
| RV1 | 1 | R_Potentiometer | Potentiometer, THT tactile footprint |
| RV2, RV3 | 2 | R_Potentiometer | Potentiometers, SMD vertical |
| D1–D4 | 4 | LED | SMD 1206 reverse-mount LEDs |

---

## ATmega32U4-A (U1) — Pin Mapping

> Pin labels follow the **Arduino Pro Micro** numbering convention used in the schematic symbol.

### Digital I/O — Direct Connections

| Schematic Pin | ATmega Port | Connected To | Function |
|---------------|-------------|--------------|----------|
| `2` | PD1 (SDA/INT1) | SW20 pin 3 (SW) | Rotary encoder push button |
| `3` | PD0 (SCL/INT0) | SW20 pin 2 (DT) | Rotary encoder — data signal |
| `4` | PD4 (ICP1) | SW20 pin 1 (CLK) | Rotary encoder — clock signal |
| `5` | PC6 | D1 pin 1 (Kathode) | LED 1 — cathode drive |
| `6` | PD7 | D2 pin 1 (Kathode) | LED 2 — cathode drive |
| `7` | PE6 | D3 pin 1 (Kathode) | LED 3 — cathode drive |
| `8` | PB4 | D4 pin 1 (Kathode) | LED 4 — cathode drive |
| `9` | PB5 (OC1A) | U2 pin SCL/SCK | Multiplexer — clock / enable |
| `10` | PB6 (OC1B) | U2 pin SDA/SI | Multiplexer — common I/O signal |
| `14` | PB3 (MISO) | SW18 pin 2 | Push button 18 (direct) |
| `15` | PB1 (SCK) | SW17 pin 2 | Push button 17 (direct) |
| `16` | PB2 (MOSI) | SW16 pin 2 | Push button 16 (direct) |

### Analog Inputs (ADC)

| Schematic Pin | ATmega Port | Connected To | Function |
|---------------|-------------|--------------|----------|
| `A0` | PF7 (ADC7) | RV1 pin 2 (wiper) | Potentiometer 1 — analog read |
| `A1` | PF6 (ADC6) | RV2 pin 2 (wiper) | Potentiometer 2 — analog read |
| `A2` | PF5 (ADC5) | RV3 pin 2 (wiper) | Potentiometer 3 — analog read |
| `A3` | PF4 (ADC4) | — (no connect) | Not used |

### Power & Unused Pins

| Schematic Pin | Connected To | Note |
|---------------|--------------|------|
| `5V` / VCC | U2 VCC | Powers multiplexer |
| `GND_00` | Main GND rail | — |
| `GND_01` | SW20 GND, SW17 pin 1, RV1 pin 3 | Shared ground node |
| `GND_02` | U2 GND | Multiplexer ground |
| `TX0` | — (no connect) | UART TX, not used |
| `RX1` | — (no connect) | UART RX, not used |
| `RST` | — (no connect) | Reset, not used |
| `RAW` | — (no connect) | Raw power input, not used |

---

## Multiplexer CD74HC4067M (U2) — Pin Mapping

The CD74HC4067M is a **16-channel analog multiplexer/demultiplexer**.
Channel pins are labeled `A0–A7` (channels 0–7) and `B0–B7` (channels 8–15) in this schematic's Aliexpress-style symbol.

### Control Interface (to ATmega U1)

| U2 Pin | Connected To | Description |
|--------|--------------|-------------|
| `SDA/SI` | U1 pin 10 (PB6) | Common I/O signal (mux SIG/COM pin) |
| `SCL/SCK` | U1 pin 9 (PB5) | Enable / serial clock |
| `VCC` | U1 VCC | 5 V supply |
| `GND` | U1 GND_02 | Ground |

### Channel Pins — A-side (Channels 0–7)

| U2 Channel Pin | Connected To | Component Type | Notes |
|----------------|--------------|----------------|-------|
| `A0` | SW15 pin 1 | SW_Push | Push button 15 |
| `A1` | SW12 pin 2 | SW_Push | Push button 12 |
| `A2` | SW9 pin 2 | SW_Push | Push button 9 |
| `A3` | SW13 pin 2 | SW_Push | Push button 13 |
| `A4` | SW7 pin 1 | SW_SPST | Toggle switch 7 |
| `A5` | SW5 pin 1 | SW_SPST | Toggle switch 5 |
| `A6` | SW2 pin 1 | SW_SPST | Toggle switch 2 |
| `A7` | SW4 pin 1 | SW_SPST | Toggle switch 4 |

### Channel Pins — B-side (Channels 8–15)

| U2 Channel Pin | Connected To | Component Type | Notes |
|----------------|--------------|----------------|-------|
| `B0` | SW19 pin 2 | SW_Push | Push button 19 |
| `B1` | SW10 pin 2 | SW_Push | Push button 10 |
| `B2` | SW14 pin 2 | SW_Push | Push button 14 |
| `B3` | SW11 pin 2 | SW_Push | Push button 11 |
| `B4` | SW8 pin 1 | SW_SPST | Toggle switch 8 |
| `B5` | SW6 pin 1 | SW_SPST | Toggle switch 6 |
| `B6` | SW1 pin 1 | SW_SPST | Toggle switch 1 |
| `B7` | SW3 pin 1 | SW_SPST | Toggle switch 3 |

### Unconnected / Floating U2 Pins

| U2 Pin | Status | Note |
|--------|--------|------|
| `A0` (left-side address) | Shorted to A2 address pin | Address select pin — not driven by MCU |
| `A1` (left-side address) | No-connect marker | Address select pin — not driven by MCU |
| `A2` (left-side address) | Shorted to A0 address pin | Address select pin — not driven by MCU |
| `RST` | Floating | Address select S3 or reset — unconnected |
| `NC/S0` | No-connect marker | Not connected |
| `NC/CS` | No-connect marker | Not connected |
| `TA`, `TB` | No-connect marker | Test pins |

> **Note:** The address select pins (S0–S3 equivalent) of U2 are not connected to the ATmega in this schematic. Channel selection is handled via `SDA/SI` and `SCL/SCK` only (likely via the serial/SPI interface of the Aliexpress module variant).

---

## Rotary Encoder (SW20)

| SW20 Pin | Connected To | Description |
|----------|--------------|-------------|
| `CLK` (pin 1) | U1 pin 4 (PD4) | Encoder clock pulse A |
| `DT` (pin 2) | U1 pin 3 (PD0) | Encoder data pulse B |
| `SW` (pin 3) | U1 pin 2 (PD1) | Encoder push button |
| `GND` | U1 GND_01 | Ground reference |
| `VCC-3.3V` | No connect | 3.3 V pin — not used |

---

## Push Buttons — Direct (SW16, SW17, SW18)

These three buttons connect directly to ATmega I/O pins without the multiplexer.

| Switch | Pin 1 | Pin 2 | ATmega Pin | Notes |
|--------|-------|-------|------------|-------|
| SW16 | — (unconnected) | U1 pin 16 (PB2/MOSI) | `16` | One side floating in schematic |
| SW17 | GND (via GND_01 net) | U1 pin 15 (PB1/SCK) | `15` | Correctly grounded |
| SW18 | — (unconnected) | U1 pin 14 (PB3/MISO) | `14` | One side floating in schematic |

---

## Push Buttons — via Multiplexer (SW9–SW15, SW19)

These 8 push buttons are read via the CD74HC4067M multiplexer.

| Switch | MUX Pin | MUX Channel | Connected Pin | Other Pin |
|--------|---------|-------------|---------------|-----------|
| SW9 | U2 A2 | Channel 2 | pin 2 | pin 1 — unconnected |
| SW10 | U2 B1 | Channel 9 | pin 2 | pin 1 — shared with SW13/SW14 |
| SW11 | U2 B3 | Channel 11 | pin 2 | pin 1 — unconnected |
| SW12 | U2 A1 | Channel 1 | pin 2 | pin 1 — unconnected |
| SW13 | U2 A3 | Channel 3 | pin 2 | pin 1 — shared with SW10/SW14 |
| SW14 | U2 B2 | Channel 10 | pin 2 | pin 1 — shared with SW10/SW13 |
| SW15 | U2 A0 | Channel 0 | pin 1 | pin 2 — unconnected |
| SW19 | U2 B0 | Channel 8 | pin 2 | pin 1 — unconnected |

> SW10, SW13, and SW14 share pin 1 (common input side).

---

## Toggle Switches — via Multiplexer (SW1–SW8)

All 8 SPST toggle switches are read via the CD74HC4067M multiplexer.

| Switch | MUX Pin | MUX Channel | Pin A (connected) | Pin B (other side) |
|--------|---------|-------------|-------------------|---------------------|
| SW1 | U2 B6 | Channel 14 | pin 1 | pin 2 — shared with SW8 pin 2 |
| SW2 | U2 A6 | Channel 6 | pin 1 | pin 2 — unconnected |
| SW3 | U2 B7 | Channel 15 | pin 1 | pin 2 — unconnected |
| SW4 | U2 A7 | Channel 7 | pin 1 | pin 2 — unconnected |
| SW5 | U2 A5 | Channel 5 | pin 1 | pin 2 — unconnected |
| SW6 | U2 B5 | Channel 13 | pin 1 | pin 2 — unconnected |
| SW7 | U2 A4 | Channel 4 | pin 1 | pin 2 — unconnected |
| SW8 | U2 B4 | Channel 12 | pin 1 | pin 2 — shared with SW1 pin 2 |

> SW1 pin 2 and SW8 pin 2 are tied together (common return path).

---

## Potentiometers (RV1, RV2, RV3)

| Ref | Pin 1 | Pin 2 (wiper) | Pin 3 | ATmega Analog Pin |
|-----|-------|---------------|-------|-------------------|
| RV1 | Unconnected | U1 A0 (PF7/ADC7) | GND (via GND_01 net) | `A0` |
| RV2 | Unconnected | U1 A1 (PF6/ADC6) | Unconnected | `A1` |
| RV3 | Unconnected | U1 A2 (PF5/ADC5) | Unconnected | `A2` |

> RV1 pin 3 is connected to GND via the shared `Net-(SW20-GND)` net.
> RV2 and RV3 have both end pins unconnected in the schematic — likely intended as wiper-only (single-ended) reads or to be connected on PCB.

---

## LEDs (D1–D4)

LEDs are **cathode-driven** (active LOW) from the ATmega. The anode (pin 2) is not connected in the schematic — must be connected to VCC (with series resistor) via PCB layout.

| Ref | Cathode (pin 1 / K) | Anode (pin 2 / A) | ATmega Pin | Drive Logic |
|-----|---------------------|-------------------|------------|-------------|
| D1 | U1 pin 5 (PC6) | Not in schematic net | `5` | LOW = LED on |
| D2 | U1 pin 6 (PD7) | Not in schematic net | `6` | LOW = LED on |
| D3 | U1 pin 7 (PE6) | Not in schematic net | `7` | LOW = LED on |
| D4 | U1 pin 8 (PB4) | Not in schematic net | `8` | LOW = LED on |

---

## Complete ATmega32U4 Used-Pin Overview

| Arduino Pin | ATmega Port | Connected To | Category |
|-------------|-------------|--------------|----------|
| `2` | PD1 | SW20 SW (encoder button) | Rotary Encoder |
| `3` | PD0 | SW20 DT | Rotary Encoder |
| `4` | PD4 | SW20 CLK | Rotary Encoder |
| `5` | PC6 | D1 cathode | LED |
| `6` | PD7 | D2 cathode | LED |
| `7` | PE6 | D3 cathode | LED |
| `8` | PB4 | D4 cathode | LED |
| `9` | PB5 | U2 SCL/SCK | Multiplexer CLK/EN |
| `10` | PB6 | U2 SDA/SI | Multiplexer SIG/DATA |
| `14` | PB3 (MISO) | SW18 pin 2 | Direct Button |
| `15` | PB1 (SCK) | SW17 pin 2 | Direct Button |
| `16` | PB2 (MOSI) | SW16 pin 2 | Direct Button |
| `A0` | PF7 (ADC7) | RV1 wiper | Potentiometer |
| `A1` | PF6 (ADC6) | RV2 wiper | Potentiometer |
| `A2` | PF5 (ADC5) | RV3 wiper | Potentiometer |
| `A3` | PF4 (ADC4) | — | Unused |
| `TX0` | PD3 | — | Unused |
| `RX1` | PD2 | — | Unused |
| `RST` | — | — | Unused |

**Total used I/O pins:** 15
**Total unused digital I/O pins:** TX0, RX1, RST, A3

---

## Net Summary

| Net Name | Nodes |
|----------|-------|
| `+5V` | U1 5V |
| `GND` | U1 GND_00 |
| `Net-(U1-GND-PadGND_02)` | U1 GND_02, U2 GND |
| `Net-(U1-PadVCC)` | U1 VCC, U2 VCC |
| `Net-(SW20-GND)` | U1 GND_01, SW17 pin 1, SW20 GND, RV1 pin 3 |
| `Net-(SW1-B)` | SW1 pin 2, SW8 pin 2 |
| `Net-(SW10-Pad1)` | SW10 pin 1, SW13 pin 1, SW14 pin 1 |
| `Net-(U1-Pad9)` | U1 pin 9, U2 SCL/SCK |
| `Net-(U1-Pad10)` | U1 pin 10, U2 SDA/SI |

---

*Generated from KiCad schematic FlightPanel-01.kicad_sch and FlightPanel-01.net*
