---
title: "Microcontroller-Free Smart Toll Collection System"
excerpt: "An automated toll gate built entirely from digital logic ICs, with no microcontroller: vehicle-type detection, configurable toll rates, gate light control, and live counters. Submitted to ICECE 2026.<br/><img src='/images/toll-hardware-full.jpg' width='300'>"
collection: portfolio
---

**Course:** EEE 304 Digital Electronics Laboratory, BUET (team project)  
**Tools:** Proteus (simulation), breadboard hardware with 74-series and CMOS logic ICs  
**Publication:** Submitted to the 14th International Conference on Electrical and Computer Engineering (ICECE 2026), Dhaka, Bangladesh *(under review)*

## Overview

An automated toll collection system implemented entirely in hardware logic, without a microcontroller or any software. The system controls the entry and exit gate lights, identifies the vehicle type (car, bus, or truck), applies a configurable toll rate for each type, keeps a separate count of each vehicle type, and displays the total toll collected. A vehicle cannot exit until its toll is paid.

## Architecture

The design is split into four independent blocks:

1. **Entry-exit light control:** 74LS279 SR latches hold the gate states, driven by the entry, toll, exit, and reset buttons.
2. **Vehicle counters:** CD4026 counter/decoders drive a 7-segment display for each vehicle type.
3. **Toll rate selection:** four 74HC153 multiplexers select the 8-bit toll rate for the detected vehicle type. Rates are set with DIP switches.
4. **Toll accumulation:** a 555 timer generates clock pulses into an 8-bit counter (74LS590). Two cascaded 74HC85 comparators stop the pulses when the count equals the selected toll rate, so the total-toll display advances by exactly that vehicle's toll.

![Block diagram of the toll collection module](/images/toll-block-diagram.jpg)

![Entry-exit light state control](/images/toll-entry-exit-block.jpg)

### Gate Light States

| Condition | Entry gate | Exit gate | Meaning |
|---|---|---|---|
| Initial | Green | Red | Vehicles can enter; none can exit |
| Vehicle entered | Red | Red | No other vehicle can enter or exit |
| Toll paid | Green | Green | The vehicle can exit; the next can enter |
| Vehicle exited | Green | Red | Ready for the next vehicle |

## Outputs

### Simulation

All four modules were first designed and verified in Proteus.

![Toll collection module simulated in Proteus](/images/toll-proteus-collection.jpg)

### Hardware

The complete system was built on four breadboards, one per block, so each block could be tested on its own before integration. In final testing, every light state and display value matched the expected behavior.

![Complete hardware implementation](/images/toll-hardware-full.jpg)

![Vehicle count displays for each vehicle type](/images/toll-hardware-vehicle-displays.jpg)

![Total toll collection display](/images/toll-hardware-total-display.jpg)

### Demonstration

[Watch the project demonstration videos on YouTube](https://www.youtube.com/playlist?list=PLygjJRLYTUTYRLC3O1THAWv5ThgeSF4wu)
