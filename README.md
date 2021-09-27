# Raspberry Pi Pico

Raspberry Pi Pico microcontroller SDK installacion and first use with VScode(C++).

*Raspberry Pi Pico 
*Ubuntu 20.04 SO
*Micro usb Cable


## Install SDK and tools

```
 wget https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh
 chmod +x pico_setup.sh
 $ ./pico_setup.sh
```


## Create a first proyect

make a directory and main.c file, open with VSCode.

```
mkdir RPIP
cd RPIP
touch main.c
code main.c
```

## Example Blink



### Blink Code
```
#include "pico/stdlib.h"

int main(){
    const uint led_pin = 25;
    gpio_init(led_pin);
    gpio_set_dir(led_pin,GPIO_OUT);

    while(true){
        gpio_put(led_pin, true);
        sleep_ms(1000);
        gpio_put(led_pin, false);
        sleep_ms(1000);
    }
}
```

### Create Cmakelist


create a .vscode directory un RPIP
and create a CMakeLists.txt file


```
cd RPIP
mkdir .vscode
touch CMakeLists.txt
gedit CMakeLists.txt
```

CMakeList.txt

```
# Set minimum required version of CMake
cmake_minimum_required(VERSION 3.12)

# Include build functions from Pico SDK
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

# Set name of project (as PROJECT_NAME) and C/C++ standards
project(blink C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Creates a pico-sdk subdirectory in our project for the libraries
pico_sdk_init()

# Tell CMake where to find the executable source file
add_executable(${PROJECT_NAME} 
    main.c
)

# Create map/bin/hex/uf2 files
pico_add_extra_outputs(${PROJECT_NAME})

# Link to pico_stdlib (gpio, time, etc. functions)
target_link_libraries(${PROJECT_NAME} 
    pico_stdlib
)

# Enable usb output, disable uart output
pico_enable_stdio_usb(${PROJECT_NAME} 1)
pico_enable_stdio_uart(${PROJECT_NAME} 0)

```

### Build

create build directory and do cmake in previous directory

```
mkdir build
cd build
cmake ..
```
when the process is complete
```
make
```

### Files

the file are created in build directory.

```
~/RPIP/build$ ls
blink.bin  blink.elf.map  CMakeCache.txt       elf2uf2    pico-sdk
blink.dis  blink.hex      CMakeFiles           generated
blink.elf  blink.uf2      cmake_install.cmake  Makefile
```

### Connect Raspberry PI Pico 

press and hold the BOOTSEL button, plug the RPI Pico to micro usb port on the computer.

RPI-RP2

copy blink.uf2 file to root directory RPI-RP2

Raspberry Pi Pico will reset and blink the onboard green led.






