# Logical operations

The following logical operations are as follows:

| Instruction |         Format          |
| :---------: | :---------------------: |
|     AND     | AND operand1, operand2  |
|     OR      |  OR operand1, operand2  |
|     XOR     | XOR operand1, operand2  |
|    TEST     | TEST operand1, operand2 |
|     NOT     |      NOT operand1       |

The first operand, in all cases, could be either in the register or in memory. The second operand could be either in register/memory or an immediate (constant) value. However, memory-to-memory operations are not possible. These instructions compare or match bits of the operands and set the CF, OF, PF, SF, and ZF flags.

## The AND Instruction

The AND instruction supports logical expressions by performing bitwise AND operations. The bitwise AND operation returns 1 if the matching bits from both operands are 1; otherwise, it returns 0. 

Let's take up another example. If you want to check whether a given number is odd or even, a simple test would be to check the least significant bit of the number. If this is 1, the number is odd, else, the number is even.

### Example code

The following code performs AND operation between 8 and 1. If the result is 0, then jump to `evnn` block, else continue. Experiment the code. **Change eax to odd number and see what happens.**

``` assembly
section .text
        global _start

_start:
        mov eax,8
        and eax,1
        jz evnn                 ;jump to evnn block when 0
                                ;if jump not 0, then continue
        mov eax,'n      '       
        mov [result],eax        ;this will print 'n', ascii 110
        mov eax,1
        int 0x80

evnn:
        mov eax,'y'     
        mov [result],eax ; this will print 'y', ascii 121
        mov eax,1
        int 0x80

segment .bss
        result resb 1
```

## The OR Instruction

The OR instruction supports logical expression by performing bitwise OR operations. The bitwise OR operator returns 1, if the matching bits from either or both operands are one. It returns 0 if both the bits are zero.

### Exercise

> Modify the above code and use OR, XOR, and NOT operation. Note that **XORing** an operand with itself changes the operand to **0**. This is used to clear a register.

## The TEST Instruction

The TEST instruction works the same as the AND operation, but unlike AND instruction, it does not change the first operand. If we need to check whether a number in a register is even or odd, we can do this using the TEST instruction without changing the original number.