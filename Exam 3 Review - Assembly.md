Function Stack is Top to Bottom, with low addresses at the top, and high addresses at the bottom.

##### Slides Review
Size - how much memory we reserved
Length - how many characters are actually there. 

For example, if you reserved 20 bytes for a user string, their name, Jim. Imagine an array with first index J, second i, third m, fourth \n
```asm


```

##### Basic String Instructions
MOVS - Instruction moves 1 Byte, Word, or Doubleword of data from memory location to another. (MOVSB, MOVSW, MOVSD)
Direction flag, cld, effects how MOVS works, right to left or left to right depending on cld having a value of 0 or 1. 

##### Operand Sizes
star on MOVS and CMPS. (important)

### Example Implementation
```asm

mov esi,source_string
mov edi,dest_string
cld
```

##### Repetition Prefixes
CLD vs STD

# Stack Slides
Stack is a LIFO structure, only stores words and doublewords (only have to worry abt doublewords)
- The stack grows in the reserve direction, i.e, toward the lower
- High addresses at the bottom, low addresses at the top

##### PUSH and POP
Things are added to the stack with the PUSH
The POP instruction removes things from the stack, the operand you give it does NOT indicate what you are taking out of the stack but where it goes. 

##### Stack: ESP
- When a word value is pushed on to the stack, the memory address of ESP decreases by 2
- When popped, ESP increases by 2
- When it's a doubleword, values change by 4 instead of 2. 

##### Stack: EBP

##### Uses of the Stack: Saving Register Values
Ex. 

##### Uses of the Stack: Functions
