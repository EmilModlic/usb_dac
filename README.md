# USB Audio DAC

Custom USB audio DACs made for headphone audio output.
Two versions were made using different microcontrollers.

Main goal:
- Audio output with USB as input
- MCU as USB to I2S translator
- Ultra low noise design

## Version 1 - RP2040 + PCM5102A

First prototype USB DAC using RP2040 as MCU and PCM5102A as DAC.

Features:
- Custom 4-layer PCB
- Separate analog and digital power supplies
- USB-C interface
- MAX97220A headphone and line output stage

Status:
- PCB fully functional
- Power and I2S verified
- USB audio firmware partially implemented

Images:

![20260221_174848](https://github.com/user-attachments/assets/93b93d57-93fd-4c22-ba05-cfe05b4396aa)
![20250221_111041](https://github.com/user-attachments/assets/6078515b-f250-4ef9-a482-49d4fb89edb4)

## Version 2 - STM32G431 + TAC5112

Second version using the STM32G431 as MCU and TAC5112 as the CODEC.

Improvements:
- Cleaner layout
- Better analog routing
- Microphone input
- Better clocking solution

Status:
- PCB fully functional
- All circuits verified
- Firmware not completed

Images:

![20260221_174907](https://github.com/user-attachments/assets/8c45a4dc-276b-4a93-a355-0564618459a9)

Both boards were designed in KiCad.
