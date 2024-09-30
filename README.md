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

## BQ24075 Overview
The BQ24075 is part of the BQ2407x series of integrated Li-Ion linear chargers and system power path management devices, specifically designed for space-limited portable applications.

This device features **Battery Disconnect Function** with a SYSOFF input, ensuring that the battery can be disconnected safely when needed.

<p align="center">
  <img src="https://github.com/user-attachments/assets/3c1be43d-2115-4970-a679-217d54297f0e" alt="BQ24075_Circuit" width="45%">
  <br>
  <em>BQ24075 - Typical Application Circuit</em>
</p>

### Key Features
- **Dynamic Power Path Management (DPPM):** Allows the system to power while simultaneously and independently charging the battery.
- **Up to 1.5-A Charge Current:** Supports a maximum charge current of 1.5 A with a current monitoring output (ISET).
- **Programmable Input Current Limit:** Configurable up to 1.5 A for wall adapters, providing flexibility in charging options.
- **Safety Features:** Includes reverse current, short-circuit, and thermal protection for enhanced reliability.
- **NTC Thermistor Input:** Integrates with NTC thermistors for temperature monitoring, ensuring safe operation during charging cycles.

## Analysis for Adapting the Thermoflagger

### Replacing PTC with NTC
Most PTC thermistors I found have a reference resistance (double of R25) at 80°C or higher. We need a significant difference in resistivity between a normal operating temperature of 25°C and 60°C. Therefore, PTC thermistors are ruled out, leaving us with NTC thermistors as the viable option.

<p align="center">
  <img src="https://github.com/user-attachments/assets/d20d8772-2c4a-4124-bb67-d352f92badf7" alt="double of R25" width="50%">
  <br>
  <em>PTC - Rref(Double of R25)</em>
</p>

**In theory, it is possible to replace PTC thermistors with NTC thermistors**, as the Thermoflagger operates based on a current source and a comparator with a reference of 0.5 V.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0c9cbea9-79ae-4ac6-84d5-5ea60e52d53b" alt="NTC and PTC curves" width="65%">
  <br>
  <em>NTC and PTC curves</em>
</p>

Using a current of 1 µA, the total resistance required is 500 kΩ. We can also place a resistor in series with the NTC to adjust the activation threshold to the desired temperature, in our case, 60°C.


<p align="center">
  <table>
    <tr>
      <td align="center">
        <em>Normal state</em>
        <br>
        <br>
        <img src="https://github.com/user-attachments/assets/7334bba1-d35f-40ae-a5e2-e861aebfc0cf" alt="Thermoflagger_WithNTC_25C" width="90%">
        <br>
        <em>Thermoflagger at 25°C</em>
      </td>
       <td align="center">
        <em>Over temperature state</em>
        <br>
         <br>
        <img src="https://github.com/user-attachments/assets/68b5112b-2c24-479b-a50c-300bfb70c391" alt="Thermoflagger_WithNTC_60C" width="90%">
        <br>
        <em>Thermoflagger at 60°C</em>
      </td>
    </tr>
  </table>
</p>










