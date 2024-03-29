/**
  @page TIM_Parallel_Synchro TIM Parallel Synchro example
  
  @verbatim
  ******************** (C) COPYRIGHT 2015 STMicroelectronics *******************
  * @file    TIM/Parallel_Synchro/readme.txt 
  * @author  MCD Application Team
  * @version V1.2.1
  * @date    20-April-2015
  * @brief   Description of the TIM Parallel Synchro example.
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

This example shows how to synchronize TIM peripherals in parallel mode.
In this example three timers are used:

Timers synchronisation in parallel mode:

   1/TIM2 is configured as Master Timer:
     - PWM Mode is used
     - The TIM2 Update event is used as Trigger Output  

   2/TIM3 and TIM4 are slaves for TIM2,
     - PWM Mode is used
     - The ITR1(TIM2) is used as input trigger for both slaves 
     - Gated mode is used, so starts and stops of slaves counters are controlled 
       by the Master trigger output signal(update event).

       The TIMxCLK is fixed to 32 MHz, the TIM2 counter clock is 32 MHz.

       The Master Timer TIM2 is running at TIM2 frequency :
       TIM2 frequency = (TIM2 counter clock)/ (TIM2 period + 1) = 125 KHz 
       and the duty cycle = TIM2_CCR1/(TIM2_ARR + 1) = 25%.

       The TIM3 is running:
       - At (TIM2 frequency)/ (TIM3 period + 1) = 12.5 KHz and a duty cycle
         equal to TIM3_CCR1/(TIM3_ARR + 1) = 30%

        The TIM4 is running:
      - At (TIM3 frequency)/ (TIM4 period + 1) = 25 KHz and a duty cycle
        equal to TIM4_CCR1/(TIM4_ARR + 1) = 60%

@par Directory contents 

  - TIM/Parallel_Synchro/stm32l1xx_conf.h    Library Configuration file
  - TIM/Parallel_Synchro/stm32l1xx_it.c      Interrupt handlers
  - TIM/Parallel_Synchro/stm32l1xx_it.h      Interrupt handlers header file
  - TIM/Parallel_Synchro/main.c              Main program
  - TIM/Parallel_Synchro/system_stm32l1xx.c  STM32L1xx system source file
  
@note The "system_stm32l1xx.c" is generated by an automatic clock configuration 
      system and can be easily customized to your own configuration. 
      To select different clock setup, use the "STM32L1xx_Clock_Configuration_V1.1.0.xls" 
      provided with the AN3309 package available on <a href="http://www.st.com/internet/mcu/family/141.jsp">  ST Microcontrollers </a>
 
@par Hardware and Software environment 

  - This example runs on STM32L1xx Ultra Low Power High-, Medium-Density and Medium-Density Plus Devices.
  
  - This example has been tested with STMicroelectronics STM32L152D-EVAL (STM32L1xx 
    Ultra Low Power High-Density) and STM32L152-EVAL (STM32L1xx Ultra Low 
    Power Medium-Density) evaluation board and can be easily tailored to any 
    other supported device and development board.

  - STM32L152-EVAL Set-up 
    - Connect the following pins to an oscilloscope to monitor the different 
      waveforms:
        - TIM2 CH1 (PA.05) 
        - TIM3 CH1 (PA.06)
        - TIM4 CH1 (PD.12)  
    - Make sure that JP14 is open.        

  - STM32L152D-EVAL Set-up 
    - Connect the following pins to an oscilloscope to monitor the different 
      waveforms:
        - TIM2 CH1 (PA.05) 
        - TIM3 CH1 (PA.06)
        - TIM4 CH1 (PD.12)
        
@par How to use it ? 

In order to make the program work, you must do the following:
 - Copy all source files from this example folder to the template folder under
   Project\STM32L1xx_StdPeriph_Templates
 - Open your preferred toolchain
 - Rebuild all files and load your image into target memory
 - Run the example

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


