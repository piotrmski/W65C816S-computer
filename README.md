# W65C816S single-board computer

The following repository documents my novice attempt at designing a microprocessor single-board computer. I had fun putting this design together, however without any prior experience it's left with many flaws which should be addressed if anyone would want to implement it again.

It's a KiCad project, however a single-page PDF of the schematic and gerber files are included, so KiCad is not required to preview it.

### Specs

- W65C816S processor clocked at 10 MHz
- 504 KiB RAM
- 7.75 KiB ROM at half clock speed
- W65C22S peripheral device controller (VIA)
- Dual PS/2 input
- MicroSD input via SPI
- W65C22S's PA6, PA7, PB0-7, CB1, CB2 exposed as general purpose output, intended to drive a character display

### Address space

- 00000-0DFFF - 56 KiB of RAM intended for stack and direct page
- 0E000-0E0FF - I/O (4 least significant bits address VIA, bits 5-7 are unused)
- 0E100-0FFFF - 7.75 KiB of ROM
- 10000-7FFFF - 448 KiB of RAM

### What I think I did right

- It's simple.
- It's compact.
- It's fast.

### Quirks of the design

- In the PCB design many of the components are in DIP packages, my choice of DIP was motivated by the ability to prototype on breadboards.
- In the PCB design capacitors are relatively large to allow hand soldering; resistors are DIP because that's what I had on hand.
- 256 B of ROM (1/32) and 8 KiB of RAM (1/64) are wasted, however I consider it not a big deal.
- Not all SD cards support SPI interface.

### What I did wrong

- The ATF16V8Cs consume unreasonable amounts of energy, glue logic should have been designed with discrete logic gate components.
- Removing and replugging the entire ROM chip to flash it is too fiddly, a programming connector would make programming this device simpler.
- ROM is read only, however it would be simple enough to add a physical switch allowing the processor to write to ROM.
