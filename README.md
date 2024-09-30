# Thermoflagger Battery Protection Overheat
[![Altium Designer](https://img.shields.io/badge/Altium-24.0-blue.svg)](https://www.altium.com/)
[![Wolfram](https://img.shields.io/badge/Wolfram-12.0-red.svg)](https://www.wolfram.com/)
[![Proteus](https://img.shields.io/badge/Proteus-8.12-green.svg)](https://www.labcenter.com/)

## Overview

This design monitors battery temperature to protect LiPo and Li-ion batteries from overheating. It disconnects the battery at 60°C and automatically reconnects at 50°C, ensuring safety during charging and discharging cycles while consuming just 2.6 µA in overheat protection mode.

The Toshiba Thermoflagger (model TCTH011AE) is essential for automatic battery disconnection and reconnection, as non-latch models are unsuitable for this purpose. Additionally, the design incorporates the BQ24075 battery charger IC, which features a dedicated pin for battery disconnection, further enhancing safety with real-time
