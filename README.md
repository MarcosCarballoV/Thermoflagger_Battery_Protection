# Thermoflagger Battery Protection Overheat
[![Altium Designer](https://img.shields.io/badge/Altium-24.0-blue.svg)](https://www.altium.com/)
[![Wolfram](https://img.shields.io/badge/Wolfram-12.0-red.svg)](https://www.wolfram.com/)
[![Proteus](https://img.shields.io/badge/Proteus-8.12-green.svg)](https://www.labcenter.com/)

## Overview

This design monitors battery temperature to protect LiPo and Li-ion batteries from overheating. It disconnects the battery at 60°C and automatically reconnects at 50°C, ensuring safety during charging and discharging cycles while consuming just 2.6 µA in overheat protection mode.

The Toshiba Thermoflagger (model TCTH011AE) is essential for automatic battery disconnection and reconnection, as non-latch models are unsuitable for this purpose. Additionally, the design incorporates the BQ24075 battery charger IC, which features a dedicated pin for battery disconnection, further enhancing safety with real-time

<p align="center">
  <img src="https://github.com/user-attachments/assets/10297e67-c70b-46b8-88ec-c31a11e35103" alt="Thermoflagger_Operating" width="30%">
  <br>
  <em>Thermoflagger - Automatic battery disconnection and reconnection </em>
</p>


## Thermoflagger

Toshiba’s Thermoflagger™ devices are designed for effective over-temperature monitoring and protection. These devices utilize a constant current source to detect temperature changes, ensuring high accuracy without the need for supply voltage stabilization.

### How the IC Operates
The Thermoflagger™ connects to a PTC thermistor via the PTCO pin. The built-in constant current source generates a low voltage across the PTC thermistor. As temperature increases, the resistance of the thermistor rises exponentially, causing a voltage increase at the PTCO pin. This voltage change is detected by the Thermoflagger™, which then generates a FLAG signal to the MCU for further actions. Multiple PTC thermistors can be connected in series for monitoring at various points within a system.

<p align="center">
  <img src="https://github.com/user-attachments/assets/63a7a22c-dd93-4368-9ddf-7ac18f51dbc4" alt="Thermoflagger_HowOperates" width="70%">
  <br>
  <em>How the Thermoflagger Operates</em>
</p>

### Features
- **High accuracy:** No supply voltage stabilization required.
- **Current source for temperature detection:** Efficient and reliable.

### Overheat Detection
The Thermoflagger™ provides a warning signal upon detecting a change in resistance in the PTC thermistor, indicating potential overheat conditions.
