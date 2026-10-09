---
title: "Class-A Common-Emitter RF Power Amplifier (433 MHz ISM Band)"
excerpt: "RF power amplifier for the 433 MHz ISM band, designed in Cadence Virtuoso: 14.14 dB gain, 20.21 dBm saturated output power, and 5.375% peak PAE, meeting every target.<br/><img src='/images/rf-pa-sparams-db.jpg' width='300'>"
collection: portfolio
---

**Course:** EEE 466 Analog Integrated Circuits and Design Laboratory, BUET (team project)  
**Tools:** Cadence Virtuoso (gpdk090), S-parameter and harmonic balance analysis

## Overview

A Class-A common-emitter RF power amplifier for the 433 MHz ISM band, used in short-range wireless devices such as remote keyless entry, wireless sensors, and home automation. The design had to balance competing requirements: Class-A operation gives high linearity but low efficiency, and pushing output power higher tends to reduce efficiency further.

| Parameter | Target | Achieved |
|---|---|---|
| Center frequency | 433 MHz | 433 MHz |
| Gain (S21) | ≥ 10 dB | **14.14 dB** |
| Saturated output power (Psat) | ≥ 17 dBm | **20.21 dBm** |
| Power-added efficiency (PAE) | ≥ 5% | **5.375%** |
| Output current | Continuous | Continuous (Class-A confirmed) |

## Design

1. **DC biasing:** a voltage-feedback bias network sets the Q-point at V<sub>CE</sub> ≈ 4.14 V and I<sub>C</sub> ≈ 152 mA, in the middle of the active region, from an 8 V supply. The Q-point was found iteratively through simulation and checked against the transistor's I-V curves.
2. **S-parameter analysis** of the unmatched amplifier to characterize its input and output impedances at 433 MHz.
3. **Impedance matching:** L-C networks at the input and output transform the amplifier's impedances to 50 Ω at 433 MHz for maximum power transfer.

![Final amplifier schematic with matching networks](/images/rf-pa-schematic.jpg)

![Transistor I-V curves used to verify the Q-point](/images/rf-pa-iv-curves.jpg)

## Outputs

### S-Parameters

After matching, the amplifier shows a gain peak exactly at 433 MHz, with deep notches in both reflection coefficients:

- **S21 = 14.14 dB** (gain)
- **S11 = −74.26 dB** (input reflection)
- **S22 = −32.08 dB** (output reflection)
- **S12 = −69.13 dB** (reverse isolation)

The input and output port impedances were confirmed at approximately 50 Ω.

![S-parameters in dB after matching](/images/rf-pa-sparams-db.jpg)

### Output Power and Efficiency

Harmonic balance analysis gave a saturated output power of **20.21 dBm** and a peak PAE of **5.375%**. Since Psat and PAE trade off against each other, the bias resistor was tuned iteratively until both targets were met at the same time.

![Saturated output power](/images/rf-pa-psat.jpg)

![Power-added efficiency vs input power](/images/rf-pa-pae.jpg)
