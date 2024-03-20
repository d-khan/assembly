# Conditions Instructions

Conditional execution in assembly language is accomplished by several looping and branching instructions. These instructions can change the flow of control in a program. Conditional execution is observed in two scenarios 

**Unconditional jump**

This is performed by the JMP instruction. Conditional execution often involves transferring control to the address of an instruction that does not follow the currently executing instruction. Transfer of control may be forward to execute a new set of instructions or backward to re-execute the same steps.

**Conditional jump**

This is performed by a set of jump instructions j<condition> depending upon the condition. The conditional instructions transfer the control by breaking the sequential flow, and they do it by changing the offset value in IP.

## CMP Instruction

CMP compares two numeric data fields. The destination operand could be either in register or in memory. The source operand could be a constant (immediate) data, register or memory.

### Example code

The following code compares two registers, jumps, and runs the instructions under the equal block.  The character 'y' is moved to the ECX register and then to the result variable in the memory. Run and debug the following code.

```assembly
section .text
        global _start

_start:
        mov eax,10
        mov ebx,10
        cmp eax,ebx
        je equal 		;jump when equal and run the equal block
        jmp exit		;unconditional jump

equal:
        mov ecx,'y'
        mov [result],ecx
        jmp exit

exit:
        mov eax,1
        int 0x80

segment .bss
        result resb 1
```

### Debug parameters

After successfully compiling and running the code, use gdb to debug the code.

```
layout asm
layout regs
watch (char) result
b _start
r
stepi
```

## Conditional jumps

| Instruction |             Description             | Flags tested |
| :---------: | :---------------------------------: | :----------: |
|    JE/JZ    |       Jump Equal or Jump Zero       |      ZF      |
|   JNE/JNZ   |   Jump not Equal or Jump Not Zero   |      ZF      |
|   JG/JNLE   | Jump Greater or Jump Not Less/Equal |  OF, SF, ZF  |
|   JGE/JNL   | Jump Greater/Equal or Jump Not Less |    OF, SF    |
|   JL/JNGE   | Jump Less or Jump Not Greater/Equal |    OF, SF    |
|   JLE/JNG   | Jump Less/Equal or Jump Not Greater |  OF, SF, ZF  |
|    JE/JZ    |       Jump Equal or Jump Zero       |      ZF      |
|   JNE/JNZ   |   Jump not Equal or Jump Not Zero   |      ZF      |
|   JA/JNBE   | Jump Above or Jump Not Below/Equal  |    CF, ZF    |
|   JAE/JNB   | Jump Above/Equal or Jump Not Below  |      CF      |
|   JB/JNAE   | Jump Below or Jump Not Above/Equal  |      CF      |
|   JBE/JNA   | Jump Below/Equal or Jump Not Above  |    AF, CF    |
|    JXCZ     |         Jump if CX is Zero          |     none     |
|     JC      |            Jump If Carry            |      CF      |
|     JNC     |          Jump If No Carry           |      CF      |
|     JO      |          Jump If Overflow           |      OF      |
|     JNO     |         Jump If No Overflow         |      OF      |
|   JP/JPE    |   Jump Parity or Jump Parity Even   |      PF      |
|   JNP/JPO   |  Jump No Parity or Jump Parity Odd  |      PF      |
|     JS      |     Jump Sign (negative value)      |      SF      |
|     JNS     |    Jump No Sign (positive value)    |      SF      |
|             |                                     |              |

### Example code - counter

The following code generates a counter 0 to 9. Use gdb to debug the code.

``` assembly
section .text
        global _start

_start:
        mov eax,0       ; reset eax to 0
label:
        inc eax
        cmp eax,10
        jl label        ;jump if less

        mov eax,1
        int 0x80
```

### Generate integer numbers using a condition instruction and print the corresponding ASCII character on the screen (from 0 - 127)
```assembly
section .text
        global _start

_start:
        mov eax, 0        ;starting from 0

increase:
        mov [tmp], 0
        push eax        ;push eax value

        mov eax, 4
        mov ebx, 1
        mov ecx, tmp
        mov edx, 1
        int 0x80

        ;the following code add extra line
        mov eax, 4
        mov ebx, 1
        mov ecx, space
        mov edx, 1
        int 0x80

        pop eax        ;restore eax value
        inc eax
        cmp eax, 127        ;end number
        jl increase

        mov eax, 1
        int 0x80

segment .bss
        tmp resb 1

section .data
        space dd 10        ;in ASCII, the new line is decimal 10
```
 

### Example code - largest number

The following code finds the largest number.

```assemly
section .text
        global _start

_start:
        mov eax,[num1]
        cmp eax,[num2]  ; compare the first operand with the second operand
        jg label1
        mov eax,[num2]
        jmp label1

label1:
        cmp eax,[num3]
        jg exit
        mov eax,[num3]

exit:
        mov [largest],eax
        mov eax,1
        int 0x80

section .data
        num1 dd 30
        num2 dd 20
        num3 dd 10

segment .bss
        largest resb 2
```

____

Last updated: Mar 2023

