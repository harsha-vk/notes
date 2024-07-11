# Project Setup

## Hardware

- STM32 NUCLEO-F302R8
    - [User Manual](assets/um1724.pdf), [Datasheet](assets/stm32f302r8.pdf), [Reference Manual](assets/rm0365.pdf)
- STM32 XNUCLEO-IHM08M1
    - [User Manual](assets/um1996.pdf)
- BLDC Motor
    - [Datasheet](assets/A700000007588698.pdf)

**Hardware Modifications:**
- STM32 XNUCLEO-IHM08M1
    - For FOC control, set jumpers: JP1 and JP2 closed, J5 & J6 on the 3-Sh side. Remove capacitors C3, C5 and C7.
    - By default the potentiometer is connected on PA4. For DAC usage remove resistor R181.

## STM32 NUCLEO-F302R8 Pin Configuration

| Pin                  | Function                                                                |
| -------------------- | ----------------------------------------------------------------------- |
| PA0 (M1_CURR_FDBK_A) | ADC1_IN1 Single-ended                                                   |
| PA1 (M1_V_BUS)       | ADC1_IN2 Single-ended                                                   |
| PA2 (USART_TX)       | USART2_TX                                                               |
| PA3 (USART_RX)       | USART2_RX                                                               |
| PA4 (USR_POT)        | ADC1_IN5 Single-ended                                                   |
| PA7 (M1_PWM_A_L)     | TIM1_CH1N PWM Generation                                                |
| PA8 (M1_PWM_A_H)     | TIM1_CH1 PWM Generation                                                 |
| PA9 (M1_PWM_B_H)     | TIM1_CH2 PWM Generation                                                 |
| PA10 (M1_PWM_C_H)    | TIM1_CH3 PWM Generation                                                 |
| PA15 (M1_HALL_A)     | TIM2_CH1 Input Capture direct mode                                      |
| PB0 (M1_PWM_B_L)     | TIM1_CH2N PWM Generation                                                |
| PB1 (M1_PWM_C_L)     | TIM1_CH3N PWM Generation                                                |
| PB2 (USR_LED)        | GPIO_Output                                                             |
| PB3 (M1_HALL_B)      | TIM2_CH2 Input Capture direct mode                                      |
| PB10 (M1_HALL_C)     | TIM2_CH3 Input Capture direct mode                                      |
| PB11 (M1_BEMF_B)     | ADC1_IN14 Single-ended                                                  |
| PB13 (M1_BEMF_C)     | ADC1_IN13 Single-ended                                                  |
| PC0 (M1_CURR_FDBK_C) | ADC1_IN6 Single-ended                                                   |
| PC1 (M1_CURR_FDBK_B) | ADC1_IN7 Single-ended                                                   |
| PC3 (M1_BEMF_A)      | ADC1_IN9 Single-ended                                                   |
| PC9 (M1_BEMF_GPIO)   | GPIO_Output Pullup                                                      |
| PC13 (USR_BTN)       | GPIO_EXTI13 External Interrupt mode with Falling edge trigger detection |
| PF0 (RCC_OSC_IN)     | RCC_OSC_IN                                                              |

## STM32 NUCLEO-F302R8 Peripheral Configuration

`The clock speed for all peripherals is 72MHz, except for PCLK1, which has a maximum frequency of 36MHz.`

| Peripheral | Parameters                                                              |
| ---------- | ----------------------------------------------------------------------- |
| DMA        | DMA Request = ADC1                                                      |
|            | Mode = Circular                                                         |
|            | Data Width = Word                                                       |
| RCC        | HSE = BYPASS Clock Source                                               |
| NVIC       | TIM2 global interrupt                                                   |
| ADC1       | Scan Conversion Mode = Enabled                                          |
|            | DMA Continous Requests = Enabled                                        |
|            | End of Conversion Selection = End of sequence of conversion             |
|            | ADC_Regular_ConversionMode:                                             |
|            | Number Of Conversions = 8                                               |
|            | External Trigger Conversion Source = Timer 1 TRGO event                 |
|            | External Trigger Conversion Edge = Trigger detection on the rising edge |
|            | Sampling time = 7.5 Cycles                                              |
| TIM1       | Counter Mode = Center Aligned mode1                                     |
|            | Counter Period = 1999                                                   |
|            | Trigger Event Selection TRGO = Update Event                             |
|            | CH Polarity = High                                                      |
|            | CHN Polarity = Low                                                      |
|            | CH Ideal State = Set                                                    |
|            | CHN Ideal State = Reset                                                 |
| TIM2       | Prescaler = 71                                                          |
|            | Counter Period = 65535                                                  |
|            | Trigger Event Selection TRGO = Update Event                             |
| USART2     | Mode=Asynchronous                                                       |
|            | Baud Rate = 115200                                                      |
|            | Data Direction = Receive and Transmit                                   |

## Additional Resources

- [Motor Control Part1 - 2 How to Measure Motor Parameters](https://www.youtube.com/watch?v=XnGHpT96Ri4)
- [Motor Control MOOC Part 1](https://www.st.com/content/st_com/en/support/learning/stm32-education/stm32-moocs/Motor_Control_Part_1_Theory_and_Motion_Profiles.html)
- [MC_WorkShop_1.6.exe](https://drive.google.com/open?id=1nYOO5LvTunM-96PAugcxo_3V53JvqJe_)
