# Arithmetic Instructions

Lets explore some arithmetic instructions.

## The INC/DEC instruction
The INC instruction is used for incrementing an operand by one. It works on a single operand that can be either in a register or in memory. The DEC instruction is used for decrementing an operand by one.

``` assembly
section .text
    global _start

_start:
    mov eax,10
    inc eax
  
    mov eax,1
    int 0x80
```

<img width="1003" alt="image" src="https://user-images.githubusercontent.com/11669149/223891859-55ce3503-c862-4b08-ad99-7944fea82d4c.png">

## The ADD and SUB Instructions
The ADD and SUB instructions are used for performing simple addition/subtraction of binary data in byte, word and doubleword size, i.e., for adding or subtracting 8-bit, 16-bit or 32-bit operands, respectively.




