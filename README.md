# JustAnotherCartridgeReader (JACR)
### An Open Source Cartridge Reader Derivative

JACR uses modified Firmware based on the OSCR Firmware - 
[Original OSCR Project](https://github.com/sanni/cartreader)

## What makes the JACR different from OSCR?
- JACR is designed with a dedicated power circuity allowing both 5V and 3.3V at the same time.  
- JACR uses a different design for adapaters, the pins back to the microcontroller remain the same but the pin pitch is altered and more power pins were added.  
- [JACR Adapters](https://github.com/Diplomatic-Entertainment/JACR-Adapters) are currently designed with logic level converters.   
- **JACR is not directly compatible with OSCR adapers and JACR Adapters are not directly compatible with the OSCR**

## What is the same as the OSCR?
- JACR uses the MEGA2560 microconroller  
- JACR has the RTC and ClockGEN built into the main board  
- Support for all the same Systems as the OSCR  
- JACR complies with Open Source Licensing with source code available for viewing and modifying  

### Open Source Licenses:
Software(everything in Firmware folder) = GPL v3  
Hardware(everything in hardware folder) = CC BY 4.0  
Complies with the original license of the OSCR where applicable  
