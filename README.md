## grblHAL driver for STM32F1xx processors

2021-08-08: Added support for F103RC variant that has more flash and RAM, added board map for [BTT SKR MINI E3 V2.0](https://www.bigtree-tech.com/products/bigtreetech-skr-mini-e3-v2-0-32-bit-control-board-integrated-tmc2209-uart-for-ender-3.html) which has this processor and uses TMC2209 drivers in UART mode.

__NOTE:__ [STM32F3xx Blackpill](../STM32F3xx/README.md) can often be used as a drop-in replacement of STM32F103 based *pills. It is likely that grblHAL support for F103 will be frozen at some point due to lack of memory.

Loosely based on code from robomechs [6-AXIS-USBCNC-GRBL](https://github.com/robomechs/6-AXIS-USBCNC-GRBL) port, updated for [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.htm) and the latest STM HAL drivers where appropriate.

See the Wiki-page for [compiling grblHAL](https://github.com/grblHAL/core/wiki/Compiling-GrblHAL) for instructions for how to import the project, configure the driver and compile.

Available driver options can be found [here](Inc/my_machine.h).

__NOTE:__ Non F103 variants must have 128KB of flash! The .ioc design file is not included as modifying the project via the designer requires a bit of cleanup after. The STM HAL is bypassed for all time critical code and to avoid bloat.  
__NOTE:__ The SD card plugin requires the SPI1 port to be remapped, disabling the JTAG/SWJ programming interfaces. This will be done on the first mount operation (via a `$FM` system command) causing the processor to hang. A power cycle is then required to get it working again.

To reenable programming a special system command, `$PGM`, can be used - issue this followed by a hard reset or power cycle to do so.

---
2021-08-08
