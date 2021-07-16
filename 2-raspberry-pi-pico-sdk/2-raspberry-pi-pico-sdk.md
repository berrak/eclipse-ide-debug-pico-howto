# Raspberry Pi Pico C/C++ SDK

![Pico C/C++ SDK](./images/source-code.png)

## Install dependencies

    sudo apt install cmake build-essential gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib git

## Download and install

The Raspberry Pi Pico SDK is required to write programs for the RP2040-based boards.
Install the SDK and additional code examples.

Clone the RPI SDK and the examples repositories:

    cd /opt/bekr
    git clone -b master https://github.com/raspberrypi/pico-sdk.git
    cd pico-sdk
    git submodule update --init
        Submodule 'tinyusb' (https://github.com/hathach/tinyusb.git) registered for path 'lib/tinyusb'
        Cloning into '/opt/bekr/pico-sdk/lib/tinyusb'...
        Submodule path 'lib/tinyusb': checked out 'd49938d0f5052bce70e55c652b657c0a6a7e84fe'
    cd ..
    git clone -b master https://github.com/raspberrypi/pico-examples.git

## Updating the SDK

Raspberry PI Foundation will release updates for the SDK.

First, set a default update strategy for `git`. Before the pull, set the local merge configuration preference in .git/config. Here we select fast-forward for our local repo. 

    git config pull.ff only

Now when it's configured, update the SDK with:

    cd pico-sdk
    git pull
    git submodule update

## Define the environment variables

Setup the environment for SDK at the end in ~/.bashrc file.

    # Add paths to RPI SDK and examples directories
    export PICO_SDK_PATH=/opt/bekr/pico-sdk
    export PICO_EXAMPLES_PATH=/opt/bekr/pico-examples

Save the file and source it to load into running environment.

    source ~/.bashrc

## Verify that the tool-chain works

Build all examples files.

    cd pico-examples
    mkdir build
    cd build 
    cmake ..

## Load and run the 'blink.uf2' program on the pico board.

Lets compile the `blink.c` program, with all available CPU cores (the j-option) for efficient compile speed.

    cd blink
    make -j$(nproc)
        ...
        [100%] Linking CXX executable blink.elf
        [100%] Built target blink

Connect a `RPI pico board` (press the boot-button and release after insert) to the USB port. Open the file manager (eg Thunar on XFCE), and open the `RPI-RP2` disk to mount it. Copy over the `blink.uf2` file from the blink/build folder and the pico board LED should start blinking.


## Verify functionality with Sparkfun's Pro Micro - RP2040.

Connect `Sparkfun's Pro Micro - Rp2040` board to the USB port (press the boot-button and release after insert). Yes, the very small one, on the same side as the red power LED on the board.

First install some terminal programs `minicom` and/or `putty` to see the hello message.

    sudo install minicom putty

Compile the `hello_usb.c` program

    cd /opt/bekr/pico-examples/build/hello_world/usb/
    make -j$(nproc)

With the file manager, copy the `hello_usb.uf2` to the `RPI-RP2` disk.
To see the message, find which device USB is connected to as a serial terminal.

    sudo dmesg | tail
        ...
        [10754.228734] usb 1-1.2: New USB device found, idVendor=2e8a, idProduct=000a, bcdDevice= 1.00
        [10754.228741] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
        [10754.228744] usb 1-1.2: Product: Pico
        [10754.228746] usb 1-1.2: Manufacturer: Raspberry Pi
        [10754.228748] usb 1-1.2: SerialNumber: E46990D80B4D1E24
        [10754.231794] cdc_acm 1-1.2:1.0: ttyACM3: USB ACM device

Connect to `minicom` for device `ttyACM3`with:

    minicom -b 115200 -o -D /dev/ttyACM3

or use the GUI `PuTTY SSH Client`. In the Putty configuration window, set `Speed` to 115200. Select `Connection type` to `serial`, set `Serial line` to `/dev/ttyACM3` and press open.

We should now see the hello messages scrolling in the terminal window.

    ...
    Hello, world!
    Hello, world!
    Hello, world!
    Hello, world!
    Hello, world!
    ...

Now, the tool-chain and the USB-to-board connections works. Ready for next step!

