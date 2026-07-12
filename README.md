# sample_CAN_303
## 概要

| 項目         | 仕様             |
| ------------ | ---------------- |
| 使用マイコン | NUCLEO_F303k8    |
| 使用IDE      | CubeIDE,VSCode   |
| 使用言語等   | C++,STM32CubeHAL |

## ピン設定
| ピン | 設定        | ラベル   | 備考 |
| ---- | ----------- | -------- | ---- |
| PB3  | GPIO_Output | DebugLED |      |
| PA12 | CAN_TX      |          |      |
| PA11 | CAN_RX      |          |      |

## クロック設定
| 項目 | 内容 | 備考 |
| ---- | ---- | ---- |

## 変更した設定
### Project Manager
Code Generator, Generated files\
✅Generate peripheral initialization as a pair of '.c/.h' files per peripheral

### CAN
MODE: ✅Activated\
CANで通信する．
#### Parameter Settings

| 項目                       | 内容  |
| -------------------------- | ----- |
| 転送速度 Baud Rate         | 1Mbps |
| サンプリングポイント       | 75%   |
| Bit Time(Time for one Bit) | 1μs   |
| CANのクロック源            | 8MHz  |
| Prescaler                  | 1     |
| Time Quantum               | 125ns |
| TSeg1                      | 5     |
| TSeg2                      | 2     |
| SJW                        | 1     |

$$
\begin{aligned}
    \text{time quantum}
        &= \frac 1 {\text{APB1 clock}} \times \text{Prescaler} \\
        &= \frac 1 {8[\mathrm{MHz}]} \times 1 \\
        &= 125[\mathrm{ns}] \\
    \text{NominalBitTime}
        &= (1 + \text{TSeg1} + \text{TSeg2}) \times \text{TimeQuantum} \\
        &= 8 \times 125[\mathrm{ns}] \\
        &= 1[\mu\mathrm{s}] \\
    \text{BaudRate}
        &= \frac 1 {\text{NominalBitTime}} \\
        &= \frac 1 {1[\mu\mathrm{s}]} \\
        &= 1[\mathrm{Mbps}] \\
    \text{sample point}
        &= \frac {1 + \text{TSeg1}} {1 + \text{TSeg1} + \text{TSeg2}} \\
        &= \frac {6} {8} \\
        &= 75[\%]
\end{aligned}
$$
参考:
- [STM32F303xx リファレンスマニュアル - STMicroelectronics](https://www.stmcu.jp/download/?dlid=51492_jp)
- [STM32マイコンでCAN通信 - ヒトミソフト開発](https://hsdev.co.jp/stm32-can/)
- [CAN Bit Time Calculation](http://www.bittiming.can-wiki.info/)
- [STM32F446_CAN/bitrate.c neo-Thrcot - GitHub](https://github.com/neo-Thrcot/STM32F446_CAN/blob/main/bitrate.c)
- [過去の議論 - esa](https://gifukosen-robot.esa.io/posts/367#%E5%88%B6%E5%BE%A1%E7%8F%AD%E3%81%A7%E8%A9%B1%E3%81%97%E5%90%88%E3%81%84%E3%81%99%E3%82%8B)
#### NVIC Settings
✅ CAN TX interrupt
✅ CAN RX0 interrupt

### USART2
#### NVIC Settings
USART2 global interrupt ✅
#### Parameter Settings
| 項目      | 内容   |
| --------- | ------ |
| Baud Rate | 115200 |
### memo
538文字
```
This is a test no meaningful content.Please paste me to your serial monitor to check if the serial communication is working properly.Check that this message is printed correctly and that the characters are not garbled.SUCCESS!!Congratulations! You have successfully set up the serial communication using InterruptBufferedUART.I like curry and rice. I also like pizza and pasta. I enjoy programming and learning new things. I hope you enjoy using this library and find it useful for your projects.Thank you for using InterruptBufferedUART!
```