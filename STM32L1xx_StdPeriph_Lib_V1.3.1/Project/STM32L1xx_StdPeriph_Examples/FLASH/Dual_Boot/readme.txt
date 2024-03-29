/**
  @page FLASH_DualBoot FLASH Dual Boot example
  
  @verbatim
  ******************** (C) COPYRIGHT 2015 STMicroelectronics *******************
  * @file    FLASH/Dual_Boot/readme.txt 
  * @author  MCD Application Team
  * @version V1.2.1
  * @date    20-April-2015
  * @brief   FLASH Dual Boot capability example.
  ******************************************************************************
  *
  * Licensed under MCD-ST Liberty SW License Agreement V2, (the "License");
  * You may not use this file except in compliance with the License.
  * You may obtain a copy of the License at:
  *
  *        http://www.st.com/software_license_agreement_liberty_v2
  *
  * Unless required by applicable law or agreed to in writing, software 
  * distributed under the License is distributed on an "AS IS" BASIS, 
  * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  * See the License for the specific language governing permissions and
  * limitations under the License.
  *
  ******************************************************************************
   @endverbatim

@par Example Description 

This example demonstrates the dual Flash boot capability of STM32L1xx High-density
devices: boot from Flash memory Bank1 or Bank2.

At startup, if BFB2 option bit is reset and the boot pins are in the boot from main
Flash memory configuration, the device boots from Flash memory Bank1 or Bank2,
depending on the activation of the bank. The active banks are checked in the following
order: Bank2, followed by Bank1.
The active bank is identified by the value programmed at the base address of the 
bank (corresponding to the initial stack pointer value in the interrupt vector table). 
For further details, please refer to AN2606 "STM32 microcontroller system memory boot mode."

To demonstrate this feature, this example provides two programs:
  - 1st program will be loaded in Flash Bank1 (starting from @ 0x08000000), for this
     you have to enable BOOT_FROM_BANK1 define in main.c 
  - 2nd program will be loaded in Flash Bank2 (starting from @ 0x08030000), for this
     you have to enable BOOT_FROM_BANK2 define in main.c 

Once these two programs are loaded and boot pins set in boot from Flash memory,
after reset the device will boot from Bank1 (default). Then you have to follow
the instructions provided on the LCD:
  - "Joystick-DOWN: reset BFB2 bit to Boot from Bank2" => when pushing the Joystick
     DOWN button, BFB2 option bit will be reset then a system (SW) reset will be
     generated. After startup from reset, the device will boot from Bank2. 
      - Note: when booting from Bank2 the same menu will be displayed
 
  - "Joystick-UP: set BFB2 bit to Boot from Bank1" => when pushing the Joystick
     UP button, BFB2 option bit will be set then a system (SW) reset will be
     generated. After startup from reset, the device will boot from Bank1.       
 
  - "Joystick-RIGHT: program to 0x0 the base @ of Bank2" => when pushing the Joystick
     RIGHT button, the content of the first page at address 0x08030000 will be copied 
     to the Bank1 at address 0x08020000 and then will be erased to 0x0. 
       - If the program was previously booting from Bank2 (i.e. BFB2 bit is reset), 
         in this case after reset no program is executed and the Bootloader code
         is executed instead. 
       - If the program was previously booting from Bank1 (i.e. BFB2 bit is set), 
         in this case after reset no program is executed.
       - You have to load again the two programs to Bank1 and Bank2.

  - "Joystick-LEFT: program to 0x0 the base @ of Bank1" => when pushing the Joystick
     LEFT button, the content of the first page at address 0x08000000 will be copied 
     to the Bank1 at address 0x08050000 and then will be erased to 0x0. 
       - If the program was previously booting from Bank2 (i.e. BFB2 bit is reset), 
         in this case after reset no program is executed and the Bootloader code
         is executed instead. 
       - If the program was previously booting from Bank1 (i.e. BFB2 bit is set), 
         in this case after reset no program is executed.
       - You have to load again the two programs to Bank1 and Bank2.

       
  - "Joystick-SEL: reprogram to default code the base @ of Bank1/2" => when pushing 
    the Joystick SEL button, the content of address 0x08030000 and 0x08000000 will
    be reprogrammed again to their default code (will be copied from BANK1<->BANK2).

@par Directory contents 

  - FLASH/Dual_Boot/stm32l1xx_conf.h    Library Configuration file
  - FLASH/Dual_Boot/stm32l1xx_it.h      Interrupt handlers header file
  - FLASH/Dual_Boot/stm32l1xx_it.c      Interrupt handlers
  - FLASH/Dual_Boot/main.h              Main header file
  - FLASH/Dual_Boot/main.c              Main program
  - FLASH/Dual_Boot/system_stm32l1xx.c  STM32L1xx system source file

@note The "system_stm32l1xx.c" is generated by an automatic clock configuration 
      system and can be easily customized to your own configuration. 
      To select different clock setup, use the "STM32L1xx_Clock_Configuration_V1.1.0.xls" 
      provided with the AN3309 package available on <a href="http://www.st.com/internet/mcu/family/141.jsp">  ST Microcontrollers </a>

@par Hardware and Software environment 

  - This example runs on STM32L1xx Ultra Low Power High-Density Devices.
  
  - This example has been tested with STMicroelectronics STM32L152D-EVAL (STM32L1xx 
    Ultra Low Power High-Density) evaluation board and can be easily tailored 
    to any other supported device and development board.

 
@par How to use it ? 
    
In order to load the IAP code, you have to do the following:
 - EWARM:
    - Open the Project.eww workspace
    - In the workspace toolbar select the project config:
        - STM32L1XX_HD_BANK1: to load the program in Flash bank1 (BOOT_FROM_BANK1
                              already defined in the project preprocessor)    
        - STM32L1XX_HD_BANK2: to load the program in Flash bank2 (BOOT_FROM_BANK2
                              already defined in the project preprocessor)
    - Rebuild all files: Project->Rebuild all
    - Load project image: Project->Debug
    - Run program: Debug->Go(F5)
    
 - MDK-ARM 
    - Open Project.uvproj project
    - In the build toolbar select the project config:
        - STM32L1XX_HD_BANK1: to load the program in Flash bank1 (BOOT_FROM_BANK1
                              already defined in the project preprocessor)    
        - STM32L1XX_HD_BANK2: to load the program in Flash bank2 (BOOT_FROM_BANK2
                              already defined in the project preprocessor)  
    - Rebuild all files: Project->Rebuild all target files
    - Load project image: Debug->Start/Stop Debug Session
    - Run program: Debug->Run (F5)

 - TrueSTUDIO 
    - Open the TrueSTUDIO toolchain.
    - Click on File->Switch Workspace->Other and browse to TrueSTUDIO workspace 
      directory.
    - Click on File->Import, select General->'Existing Projects into Workspace' 
      and then click "Next". 
    - Browse to the TrueSTUDIO workspace directory and select the project: 
        - STM32L1XX_HD_BANK1: to load the program in Flash bank1 (BOOT_FROM_BANK1
                              already defined in the project preprocessor)    
        - STM32L1XX_HD_BANK2: to load the program in Flash bank2 (BOOT_FROM_BANK2
                              already defined in the project preprocessor) 
    - Rebuild all project files: Select the project in the "Project explorer" 
      window then click on Project->build project menu.
    - Run program: Select the project in the "Project explorer" window then click 
      Run->Debug (F11)
        
@note
- Ultra Low Power Medium-density devices: - STM32L151x6xx, STM32L151x8xx, STM32L151xBxx, STM32L152x6xx,
                                            STM32L152x8xx, STM32L152xBxx, STM32L151x6xxA, STM32L151x8xxA,
                                            STM32L151xBxxA, STM32L152x6xxA, STM32L152x8xxA and STM32L152xBxxA
                                          - STM32L100x6xx, STM32L100x8xx and STM32L100xBxx
- Ultra Low Power Medium-density Plus devices: - STM32L151xCxx, STM32L152xCxx and STM32L162xCxx 
                                               - STM32L100xCxx
- Ultra Low Power High-density devices: STM32L151xDxx, STM32L152xDxx and STM32L162xDxx
- Ultra Low Power XL-density devices: STM32L151xExx, STM32L152xExx and STM32L162xExx
    
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */


