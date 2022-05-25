AT89S8252
=========

Interrupts:
-----------
interrupt | asm addr. | c
----------|-----------|---
ext0:     | 0003h     | 0
timer0:   | 000Bh     | 1
ext1:     | 0013h     | 2
timer1:   | 001Bh     | 3
serial:   | 0023h     | 4
timer2:   | 002Bh     | 5

-------------------------------------------------------------------------------
Assembler:
----------
```
$NOMOD51
$include (AT898252.h)
org 0000h
LJMP start

; vvvv Interrupt sprungbefehle
org 0003h
LJMP int0_isr

; vvvv Main Program
start:
; ...

; vvvv Interrupt Service Routines
int0_isr:
    ; ...
    RETI

; Programmende
END
```

Ports: `P2.3`  
Konstanten:
`#0A1h` entspr. `0xA1`  
`#1d` entspr. `0d1`
Kommentare: `; Kommentar`

-------------------------------------------------------------------------------
C:
---
```
#include<AT898252.h>

// data type aliases for convenience
#define u8  unsigned char
#define i8  char
#define u16 unsigned int
#define i16 int
#define u32 unsigned long int
#define i32 long int

void main() {
    init();
    // ...
}

// vvvv Setup the interrupts
void init() {
    IT0 = 1; // falling edge triggered
             // state triggered: 0
    EX0 = 1; // Enable EXT1
    EA  = 1; // Enable Interrupts
}

// vvvv Interrupt Service Routine
void int0() interrupt 0 {
    // ...
}
```
Ports: `P2_3`  
Kommentare:  
```
// Kommentar
/*
  Kommentar
 */
```

### memory types:
type    | ort
--------|-------------------------------------
`data`  | direkt adressierbarer interner RAM
`pdata` | bitwise adressierbarer interner RAM
`idata` | indirekt adressierbarer interner RAM
`pdata` | 'paged' externer Datenspeicher
`xdata` | externer Datenspeicher
`code`  | Programmspeicher

### data types:
type     | size
---------|------
`sbit`   | 1 Bit
`sfr`    | 1 Byte
`sfr 16` | 2 Byte

-------------------------------------------------------------------------------
Anderes Hilfreiches:
--------------------

∧ : AND  
∨ : OR
¬ : NOT

b   |x|d |o 
----|-|--|--
0000|0| 0| 0
0001|1| 1| 1
0010|2| 2| 2
0011|3| 3| 3
0100|4| 4| 4
0101|5| 5| 5
0110|6| 6| 6
0111|7| 7| 7
1000|8| 8|10
1001|9| 9|11
1010|A|10|12
1011|B|11|13
1100|C|12|14
1101|D|13|15
1110|E|14|16
1111|F|15|17