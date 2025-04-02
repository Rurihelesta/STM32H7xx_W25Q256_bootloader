# STM32H7xx_W25Q256_bootloader
 boot from W25Q256 QSPI flash
## How to install
set pins to match your board
flash it into stm32h7xx(only test on stm32h743iit6)
(if your chip is other maybe need to change something)

## Not H743?(maybe not work)
use cubeMX create a project
(need QUEDSPI,disable MPU)
(QSPI prescaler must change)
(size must change to 25)
copy main.c
modify some parameter
    

## Make app

in main.c

add #define APPLICATION_ADDRESS   0x90000000UL
add SCB->VTOR = APPLICATION_ADDRESS; in USER CODE BEGIN SysInit

change XXX_FLASH.id

    MEMORY
    {
    DTCMRAM (xrw)      : ORIGIN = 0x20000000, LENGTH = 128K
    RAM (xrw)      : ORIGIN = 0x24000000, LENGTH = 512K
    RAM_D2 (xrw)      : ORIGIN = 0x30000000, LENGTH = 288K
    RAM_D3 (xrw)      : ORIGIN = 0x38000000, LENGTH = 64K
    ITCMRAM (xrw)      : ORIGIN = 0x00000000, LENGTH = 64K
    FLASH (rx)      : ORIGIN = 0x90000000, LENGTH = 32M
    }

## flash your app
download external loader from https://github.com/cturvey/stm32extldr
put it into C:\Program Files\STMicroelectronics\STM32Cube\STM32CubeProgrammer\bin\ExternalLoader(if yuo use stm32cubeprogramer)
or C:\ST\STM32CubeCLT_1.18.0\STM32CubeProgrammer\bin\ExternalLoader(if you use vscode)

(vscode only)
add in launch.json

    "serverArgs": [
                "-m","0","-el (put your loader name here)"
            ],

flash and enjoy