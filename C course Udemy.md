## Nucleo F401RE notes
-   User LED: PA5, D13 (Arduino pin)

### 2.12
Clean project → delete binaries

### 2.14
New → stm32 project
Don’t delete files from project

### 3.17
Online gdb
`#include` is preprocessor directive that instructs preprocessor to include file into source file
Compiler flag: -save-temps
.s file is assembly of .c file
.o file is machine code/object file

### 4.25
'short' always 2 bytes.
'char' always 1 byte → possible to store numeric integer in char

### 4.28
Signed data stored in 2's complement: first bit is sign.
-   → invert bits and add 1 at LSB.
-   Adding is same as decimal.

### 4.32
- Variable is label to memory location of data.
- Variable names are not stored inside memory, they are replaced with memory location address during data manipulation.
- Variable declaration lets compiler know it needs data for variable. "I declare this variable!!"
- Variable definition/initialization puts data in variable. "I define this variable as xxx!!"

Variable naming:
-   Uppercare, lowercase, digits, underscore
-   First cannot be digit
-   No reserved keywords

### 4.33
'extern' keyword tells compiler that variable is declared outside scope of file. → wont allocate storage for the variable!

### 4.34
-   Local: only exist in function (also 'int main()'), die after function is done.
-   Global: declared before 'main'. Accessible from anywhere in program. Can be overwritten!

### 4.37
`%var_example` gives address of `var_example` in hex → returns pointer data type.
To store pointer value in int it must be casted: int address = (int)%var;

### 6.39
Storage class:
-   Scope
-   Visibility
-   Lifetime
    → modified using storage class specifiers.

-   'static': global variable private to function in which it is defined, does not die out of scope. Static function is only callable from main.
-   'extern': access global variable or function outside scope of file.

### 8.50
-   Printf over SWO
-   SWD: serial wire debug
-   Alternative to JTAG
-   Instrumentation Trace Macrocell Unit
-   To use printf: put bits in FIFO (in ITM unit) which will then go to SWO pin.
-   Use code from course to use printf over SWO
-   In syscalls.c: after includes paste code,
-   in function 'write' on line 136: change '__io_putchar(*ptr++);' to 'ITM_SendChar(*ptr++);'
-   'printf' will call write function to send over SWO

### 8.51
-   '.elf': type of executable, executable and linkable format, for debugging → will be used here
-   '.bin' & '.hex' binaries only for executing
-   After compiling: debug → debug configurations → dbc STM32 MCU debugging → debugger → select ST-link GDB server, SWD, SWV, 16 MHz, 2000 kHz
-   Debug as 'STM32 …' → project will be loaded to STM32 and paused at first instruction
-   Window → show view → SWV → SWV ITM Data Console → configure trace → select port 0
-   Start trace
-   Reset chip and restart debug session

### 8.53
-   for(;;); is an infinite loop

### 9.56
**Build process**:
1.  Preprocessing
2.  Parsing
3.  Produce object files
4.  Link object files
5.  Produce final executable
6.  Post process final executable

**Preprocessing:** `#includes` & `#defines` are resolved

**Parsing:** Syntax of code is checked for errors.

.s file is assembly mnemonic file

### 10.57
Code memory → flash/ROM/EEPROOM/OTP/FRAM (non-volatile)
Data memory → SRAM

### 10.58
Code/program memory stores instructions & constant data.

### 10.59

Examine program memory: window show memory browser view

Look for base address in reference manual

Bootloader in system memory

Base address: 0x0800 0000

Code will be put from this address onwards

Put this in memory browser

Change columns & cell size for better readability

Check base address for SRAM1: 0x2000 0000 - 0x2001 7FFF

The bytes are coded in memory in little endian format. The lowest numbered byte in a word

is considered the word’s least significant byte and the highest numbered byte, the word’s

most significant.

### 10.60

How does data end up in SRAM memory from flash memory?

### 11.63

Floating point → IEEE 754

-   Very small
-   Very big
-   Fraction

### 11.65

Float: up to 6 decimal places

Double: 15 decimal places

### 12.66

### 13.74

Pointer data type will always reserve 4 bytes (32bit)

Pointer data type decides behavior of operations on pointer → increment and decrement will be size of type

### 13.75

Dereference pointer to read data:

`char data = *address1;`

1 byte of data if read from address1 and stored in `data` variable.
Dereference pointer to write data:
`*address1 = 0x89;`

### 16.90
-   'scanf' return total number of successfully scanned inputs

### 95
-   Use 'break' with switch statements

### 102
**Bit manipulation**:
- Testing: &
- Setting: |
- Clearing: ~ and &
- Toggling: ^

### 119
**Set a bit**:
```c
BYTE |= (1 << i);

PORTB |= (1 << PINB0)|(1 << PINB2)|(1 << PINB4);
```
**Clear a bit**:
```c
BYTE &= ~(1 << i);
```
**Toggle a bit**:
```c
BYTE ^= (1 << i);
```

### 145
`Volatile` tells compiler not to optimize read-write operations on variable.

`uint8_t volatile *pPointer // non-volatile pointer pointing to volatile data`

### 156
```c
struct example{
    ...
}__attribute__((packed));

```
### 158
```c
typedef struct
{
    ...
} typedefName_t;
```

`_t` used for typedefs, `_e` used for enums. 

### 159
```c
Struct Example *pExample;

pExample = %ExampleStruct

pExample → FirstElement = …;
```