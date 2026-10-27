# UGV Control Board

Custom 2-layer controller board and bare-metal firmware for an unmanned ground vehicle (UGV), built around an STM32F103RET6 (ARM Cortex-M3).


## Overview

The board reads RC PWM commands and talks to a Pixhawk/Cube autopilot, then controls throttle, direction, brake and drive motors, with fail-safes for lost or invalid signals.



## Hardware

| Block | Implementation |
|---|---|
| MCU | STM32F103RET6 (Cortex-M3) |
| Power | Power distribution on board 12V input |
| I/O protection | Optocoupler isolation stages against noise |
| Relay drive | Darlington arrays driving high-current direction and brake relays |
| Motor drive | BTS7960 H-bridge drivers, OEM BLDC Drivers |
| Throttle output | 12-bit I2C DAC |
| Communication | CAN bus transceiver; headers for Pixhawk/Cube autopilot and SBUS |
| PCB | 2 layers, designed in Altium Designer |

Schematic: [`docs/schematic.pdf`](docs/schematic.pdf) · PCB views: [`docs/pcb_top.png`]`docs/pcb_top.png`, [`docs/pcb_bottom.png`]`docs/pcb_bottom.png`

## Firmware

Bare-metal C. Main parts:

- **RC PWM decoding:** 4-channel timer input capture interrupts decode standard RC PWM signals with microsecond timing accuracy.
- **Control logic:** non-blocking state machine for relay sequencing, throttle deadbands and safety fail-safes.
- **I2C bus recovery:** automatic recovery routine for I2C bus lockups, using SCL/SDA bit-banging.




## Repository layout

```
docs/       photos, schematic PDF, PCB renders
hardware/   Altium project, libraries, Gerbers, BOM
firmware/   STM32CubeIDE project and source code
```



