# 8051 Registers

## 8051
<a href="https://imgbb.com/"><img src="https://i.ibb.co/72MxW2g/image.png" alt="image" border="0"></a>

|Pin|Description|
|---|---|
|1-8|`Port 1` from `P0.0` to `P1.7` |
|9 |`RST` Upon applying a high pulse to this pin, the microcontroller will reset and terminate all activities|
|10-17|`Port 3` from `P3.0` to `P3.7` |
|18|`XTAL2` We can observe the frequency on the XTAL2 pin using the oscilloscope|
|19|`XTAL1` If you use a frequency source other than a crystal oscillator, such as a TTL oscillator, It will be connected to XTAL1 |
|20|`GND` |
|21-28|`Port2` from `P2.0` to `P2.7` to be used with `P0` to access 16 bits-address memory. |
|29|`PSEN` 8031-based systems `Program Store Enable`, is an output pin (ROM)|
|30|`ALE` 8031-based systems `Address Latch Enable`, is an output pin, ALE pin is used for demultiplexing the address and data|
|31|`EA` an input pin and must be connected to Vcc (8051) or GND (8031) |
|32-39|`Port 0` from `P0.7` to `P0.0`|
|40|`VCC`|


## PSW (Program Status Word) ==> Bit-Addressable

|CY   `PSW.7`|   AC `PSW.6`|   F0 `PSW.5`|  RS1 `PSW.4`|  RS0 `PSW.3`|   OV `PSW.2`|   -- `PSW.1`| P `PSW.0`|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Carry Flag   |    Auxiliary carry flag.|    Available to the user for general purpose| Register Bank selector bit 1.| Register Bank selector bit 0.| Overflow flag.|User definable bit.|Parity flag. |

## Port 3 ==> Bit-Addressable
' = Bar

|RD'   `P3.7`|   WD' `P3.6`|   T1 `P3.5`|  T0 `P3.4`|  INT1' `P3.3`|   INT0' `P3.2`|   TxD `P3.1`| RxD `P3.0`|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Reading   |   Writing|    Timer 1| Timer 0| External interrupt 1| External interrupt 0|Serial  communications|Serial  communications |

## Timers 0/1

The low byte register is called TL0/TL1 and The high byte register is called TH0/TH1

|`TH`|`TH`|`TH`|`TH`|`TH`|`TH`|`TH`|`TH`|`TL`|`TL`|`TL`|`TL`|`TL`|`TL`|`TL`|`TL`|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|

## TMOD

The lower 4 bits are for Timer 0 The upper 4 bits are for Timer 1

|GATE (T1) |   C/T (T1)|   M1 (T1)|  M0 (T1)|GATE (T0) |   C/T (T0)|   M1 (T0)|  M0 (T0)|
|:---:                                          |:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|0 `Software` 1 `External Hardware`| 0 `Timer` 1 `Counter`|    Modes 0 => `(13-bit)` 1 => `(16-bit)` 2 => `(8-bits)` 3 => `(split-timer)`| Modes 0 => `(13-bit)` 1 => `(16-bit)` 2 => `(8-bits)` 3 => `(split-timer)`|0 `Software` 1 `External Hardware`| 0 `Timer` 1 `Counter`|Modes 0 => `(13-bit)` 1 => `(16-bit)` 2 => `(8-bits)` 3 => `(split-timer)`|Modes 0 => `(13-bit)` 1 => `(16-bit)` 2 => `(8-bits)` 3 => `(split-timer)`|


## TCON ==> Bit Addressable
|TF1   `TCON.7`|   TR1 `TCON.6`|   TF0 `TCON.5`|  TR0 `TCON.4`|  IE1 `TCON.3`|   IT1 `TCON.2`|   IE0 `TCON.1`| IT0 `TCON.0`|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| raised when overflow.   |   start timer 1.|    raised when overflow.| start timer 0.| External interrupt 1 edge flag.| Interrupt 1 type control bit. Set/cleared by software to specify falling edge/low level triggered external interrupt|External interrupt 0 edge flag.|Interrupt 0 type control bit. Set/cleared by software to specify falling edge/low level triggered external interrupt |


## SCON ==> Bit Addressable

|SM0   `SCON.7`|   SM1 `SCON.6`|   SM2 `SCON.5`|  REN `SCON.4`|  TB8 `SCON.3`|   RB8 `SCON.2`|   TI `SCON.1`| RI `SCON.0`|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Serial port mode specifier (MODE 1 ONLY)|   Serial port mode specifier (MODE 1 ONLY)|   Used for multiprocessor communication| Set/cleared by software to enable/disable reception| Not widely used| Not widely used|Transmit interrupt flag Set by HW at the begin of the stop bit mode 1.|Recieve interrupt flag Set by HW at the begin of the stop bit mode 1. |

## PCON 

|SMOD |   --|   --|  -- |   GF1 |GF0 |PD |IDL|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|We can set it `1` to high by software and thereby double the baud rate|-|-|-|-|-|-|-|

## Interrupt Vector Table

<a href="https://imgbb.com/"><img src="https://i.ibb.co/4TwdJ6Q/image.png" alt="image" border="0"></a>

## IE (Interrupt Enable) Register ==> Bit Addressable

|EA   `IE.7`|   -- `IE.6`|   ET `IE.5`|  ES `IE.4`|  ET1 `IE.3`|   EX1 `IE.2`|   ET0 `IE.1`| EX0 `IE.0`|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Enables/Disables all interrupts   |   Not implemented|    Enables or disables timer 2| Enables or disables the serial port interrupt| Enables or disables timer 1 overflow interrupt| Enables or disables external interrupt 1|Enables or disables timer 0 overflow interrupt|Enables or disables external interrupt 0|

## Interrupt Priority

<a href="https://imgbb.com/"><img src="https://i.ibb.co/42vrw9w/image.png" alt="image" border="0"></a>

## Interrupt Priority Register

<a href="https://imgbb.com/"><img src="https://i.ibb.co/ZWQR1vv/image.png" alt="image" border="0"></a>

## LCD

<a href="https://ibb.co/m42sjjB"><img src="https://i.ibb.co/w4PHkkL/image.png" alt="image" border="0"></a>
