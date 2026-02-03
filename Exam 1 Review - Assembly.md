Assembly is a symbolic language, architecture specific, eventually gets turned into machine code
takes up less memory, runs faster

know what a bit and a byte are

know how to convert, add, and subtract, decimal, hexadecimal, binary. Use 2's complement in a subtraction of two binary numbers, etc.

Know how to represent integers, the range of integers stored in a particular size, and using 2's complement. 

know how values aer stored in RAM in little-endian machines

# Assembly basics
.data - Is initialized, will remain static, essentially read only permission
.bss - where we reserve memory, size will remain static, read and write

.text - (code segment) execute, read

know what GLOBAL is 

macro is a text substitution

Label -> instruction -> destination -> source

Will have to finish code, not write a while program

nasm - compiling, ld - linking

outside of a few macros nasm is not case sensitive 

### Memory segments and registers
Know what a memory segment is and know how one relates to the SECTION directive. 

classifications of general registers

registers vs ram, registers don't have to traverse because it is on the processor, super easy, super fast.  The trade off with memory is the closer to processor, the smaller. Most are 32 bit registers. 

EAX - full 32 bit, AX - half (16 bits lower half), AH + AL = AX but divided. 

EFLAGS - overflow, carry, 

**you as the programmer do not directly interact with the EFLAGS register**
- true/false that involves moving into EFALGS register, this will be FALSE

Other than CS, DS, and SS 
unless you are making an OS, you wont care abt CS, DS, and SS

### Linux sys calls
- Know sys_write(), sys_read(), and know how to use them and how they work, call the specific one.  

Does not get called until the interrupt is 

### Addressing and Instructions
- Know how to change an instruction such as ```
  ```
  ADD [BYTE_VALUE], 65
  ``` 
so that it is correct. Be able to describe why the assembler will give and error if such an  
instruction is not fixed.
``` Assembly
MOV DX 2 <- immediate
[msg] = 

[msg+1] - equivalent
msg.[1] - ^ equivalent

add msg,1 | - ^ equivalent
[msg]     |

mov[num],2
mov Byte[num],2

```

Know what an instruction such as MOV DX, [TAX_RATE] means. Know what an  
instruction such as MOV DX, TAX_RATE means.
- If done without brackets, then


# studying slides
1. What is Assembly?
	- What is assembly language slide
		- Processor understands only machine language
		- Machine language is too obscure and complex
		- symbolic
		- fine grained control
	- More advantages of using assembly language
		- less memory and (possibly) execution time
	- Basic Features of PC Hardware
		- A bit is the most basic unit of information in a computer
		- A byte is a group of 8 bits
	- Processor Data Sizes
		- Word - 2 byte 
		- Doubleword - a 4 byte (32 bit) data item
		- Quadword - an 8 byte (64 bit) data item
		- etc
		- **Kilobyte: 1024 bytes**
	- Number representation
		- ${10111_2} = 23_{10}$
		- ^ base 2        ^ base 10
		- MSB - most significant bit = leftmost bit
		- LSB - least significant bit = rightmost bit
	- Translating Unsigned Decimal to Binary
		- 33 /2 = 18 R 1 
		- 18/2   = 9 R 0
		- 9/2     = 4 R 1
		- 4/2     = 2 R 0 
		- 2/2     = 2 R 0
	- Hexadecimal Numbers
		- Base 16
		- Digits
			- 0- 9 same as decimal
			- 10 - A
			- 11 - B
			- 12  - C
			- 13 - D
			- 14 - E 
			- 15 - F
	- Hexadecimal to Decimal
		- $5CB_{16} = 1483_{10}$ 
		- ^ same as $11 * 1 + 12 * 16 + 5 * 16^2$
	- Decimal to Hex
		- 422/16 = 26 R 6
		- 26/16   = 1    R A
		- 1/16      = 0    R 1
		-  decimal 422 = 1A6 hexadecimal
2. 