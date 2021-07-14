# Debug RPi Pico boards with Eclipse IDE

This project aims to create a step-by-step process for setting up latest Eclipse IDE for debugging with Raspberry Pi Pico boards, and other manufactures that use the RPI RP2040 mcu. There are no automation or scripts in this procedure, simply because its not that complicated. The devil sits in the details, thus its outmost important that each steps are verified to work before continue to next step. 

There is no meaning to start with the Eclipse IDE and then face unnecessary configuration problems at the final setup. A second advantage with this approach is that a lot of good knowledge accumulates about the used tool-chain. 

Although Raspberry Pi Pico documentation is excellent, on Linux it's written for RPI4 development much in mind. However I guess, that the majority of users interested in the C/C++ SDK will setup their development on [Windows](https://github.com/ndabas/pico-setup-windows) or any `free operating systems`. Here we target the latest releases of [Debian](https://www.debian.org/distrib/) (v.11 aka Bullseye) or later and [Ubuntu](https://ubuntu.com/#download) 21.04 or later, current as of this writeup.

This project use as examples, two genuine [RPI pico](https://www.raspberrypi.org/products/raspberry-pi-pico/) boards or one [Sparkfuns Pro Micro](https://www.sparkfun.com/products/17717) - RP2040, a smaller board without SWD pins. 

## Major software used in this setup project

- Raspberry Pi Pico C/C++ SDK
- OpenOCD (Raspberry Pi fork for RP2040)
- OpenOCD (authentic)
- picoprobe, by Raspberry Pi
- pico-debug, by `majbthrd` (github)
- GDB, The GNU Project Debugger
- Eclipse IDE 2021-06 (which includes Eclipse Embedded C/C++)

Then there are various dependencies as well.

## About debugging micro controllers

Read a quick intro by `majbthrd`: [What is a debugger](https://github.com/majbthrd/pico-debug/blob/master/howto/about.md) which is the author of `pico-debug`.


## Start the journey!

- [1. Eclipse IDE](1-eclipse-ide/1-eclipse-ide.md)
  * 1.1 Download and installation
  * 1.2 Configuration

- [2. Raspberry Pi Pico C/C++ SDK](2-raspberry-pi-pico-sdk/2-raspberry-pi-pico-sdk.md)
  * 1.1 Download and installation
  * 1.2 Configuration

- [3. Code samples and templates]()
  * 3.1 CMakeLists-templates
  * 3.2 Setup the projects file structure
  * 3.3 Example code
    + blink
    + adc

- [4. Converting the project for Eclipse]()
  * 4.1 Eclipse CDT4 Makefiles

- [5. Hardware wiring]()
  * 5.1 Debug with two Raspberry Pi Pico boards, via SWD and picoprobe
  * 5.2 Debug with one Sparkfun Pro Micro RP2040, via USB and pico-debug
  * 5.3 Use FTDI/serial converter
  * 5.4 Udev rules for picoprobe

- [6a. Use picoprobe and two picoboards]()
  * 6a.1 Install picoprobe
  * 6a.2 Install OpenOCD built for RP2040
  * 6a.3 Install The GNU Project Debugger (GDB)
  * 6a.4 Verify upload via openocd and SWD
  * 6a.5 Verify GDB is working

- [6b. Use pico-debug and one Sparkfun Pro Micro RP2040]()
  * 6b.1 Install pico-debug
  * 6b.2 Install OpenOCD (authentic)
  * 6b.3 Install The GNU Project Debugger (GDB)
  * 6b.4 Verify upload via openocd and USB
  * 6b.5 Verify GDB is working

  [7. Debians update-alternatives]()
    * 7.1 Manage multiple versions of OpenOCD

- [8. Debug blink in Eclipse]()
  * 8.1 Load project blink as an Eclipse project
  * 8.2 Build project
  * 8.3 Configure debug settings for picoprobe/pico-debug
  * 8.4 Debug session with UART-serial output

- [9. Debug adc in Eclipse]()
  * 9.1 Load project adc as an Eclipse project
  * 9.2 Build project
  * 9.3 Use previous debug configuration
  * 9.4 Debug session with UART-serial output 

- [10. Help utilities]()
  * 10.1 The uf2 shell script
  * 10.2 The elf shell script

## Contribute to project

Feel free to file any issues found, pull requests or help with support for other Linux distributions.

## Credits

This project gather and structure existing and some own material in a step-by-step process, but fundamentally builds on all authors mentioned, who have done all the heavy lifting. I'm thankful for their valuable work. This writeup hopes to bring new users of Raspberry Pi Pico up to speed with debugging in Eclipse IDE (or other capable IDE), with either `picoprobe` or `pico-debug`.

## Additional documentation

- [1] Download pdf: [Getting started with Raspberry Pi Pico](https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf) by `Raspberry Pi Foundation`.
- [2] GitHub: [pico-debug](https://github.com/majbthrd/pico-debug) by `majbthrd`.
- [3] GitHub: [picoprobe](https://github.com/raspberrypi/picoprobe) by `Raspberry Pi Foundation`.

