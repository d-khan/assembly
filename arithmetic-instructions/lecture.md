# Arithmetic Instructions

Let's explore some arithmetic instructions.

## Pre-requisite

- Knowledge of how to run assembly code using nasm assembler in Linux OS. (see video)
- Knowledge of how to debug an assembly code using `gdb`. (see video)

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

The above code is dissected using the `gdb` application. See the value of the eax register. The decimal value is 11, and the corresponding hex value is 0xb.

<img width="1003" alt="image" src="https://user-images.githubusercontent.com/11669149/223891859-55ce3503-c862-4b08-ad99-7944fea82d4c.png">



## The ADD and SUB Instructions

The ADD and SUB instructions are used for performing simple addition/subtraction of binary data in byte, word, and doubleword size, i.e., for adding or subtracting 8-bit, 16-bit, or 32-bit operands, respectively.

The ADD/SUB instruction can take place between

- Register to register
- Memory to register
- Register to memory
- Register to constant data
- Memory to constant data

However, like other instructions, memory-to-memory operations are not possible using ADD/SUB instructions. An ADD or SUB operation sets or clears the overflow and carries flags.

### Example code

The following example adds two numbers, stores the digits in the EAX and EBX register, adds the values, and stores the result in a memory location, 'result'.

```{assembly .numberLines}
section .text
		global _start

_start:
		mov eax,10
		mov ebx,20
		add eax,ebx
		mov [result],eax
		
		mov eax,1
		int 0x80

segment .bss
		result resb 1
```
The following is the analysis of the assembly code.

> **segment .bss** An assembly language code that contains statically allocated variables that are declared but have not been assigned a value yet. It is often called the "bss section" or "bss segment". 

## The MUL/IMUL instruction

There are two instructions for multiplying binary data. The MUL (Multiply) instruction handles unsigned data and the IMUL (Integer Multiply) handles signed data. Both instructions affect the Carry and Overflow flag.

> **Depending upon the size of the multiplicand, the multiplier, and the generated product, the product is either stored in one register or two registers depending upon the size of the operands.**

**When two bytes are multiplied, the multiplicand is in the AL register, and the multiplier is a byte in the memory or another register. Finally, the product is in the eax register, as shown in the debugger's output.** 

**When two one-word values are multiplied −** The multiplicand should be in the AX register, and the multiplier is a word in memory or another register. For example, you must store the multiplier in DX and the multiplicand in AX for an instruction like MUL DX. The resultant product is a doubleword, which will need two registers. The high-order (leftmost) portion gets stored in DX and the lower-order (rightmost) portion gets stored in AX.

**When two doubleword values are multiplied −**When two doubleword values are multiplied, the multiplicand should be in EAX, and the multiplier is a doubleword value stored in memory or in another register. The product generated is stored in the EDX:EAX registers, i.e., the high order 32 bits get stored in the EDX register, and the low-order 32-bits are stored in the EAX register.

### Example code 1

The following code multiplies two numbers. The result is saved in the eax register.

```{assembly .numberLines}
section .text
		global _start
		
_start:
		mov al,10
		mov dl,25
		mul dl
		
		mov eax,1
		int 0x80
```

<img width="1250" alt="image" src="https://user-images.githubusercontent.com/11669149/223907405-4e765993-af50-469f-a77b-88b995a6f05d.png">

> **When referring to registers in assembly language, the names are not case-sensitive. For example, the names `EAX` and `eax` refer to the same register.**

The following figure shows the **x86 Registers**.

<img width="694" alt="image" src="https://user-images.githubusercontent.com/11669149/223949886-b2796233-aa52-4656-986d-0d0e77f32cba.png">

### Example code 2

The following code solves the equation $\ref{ref1}$, where $var1$, $var2$ and $var3$ are initialized variables, whereas $var4$ is an un-initialized variable. The output will be saved in $var4$ with a value of 21.
$$
var4 = (var1 + var2) * var3\label{ref1}
$$


```{assembly .numberLines}
section .text
		global _start

_start:
		mov eax,[var1]
		add ebx,[var2]
		mov dl,[var3]
		mul dl
		mov [var4],eax
		
		mov eax,1
		int 0x80

section .data
		var1 DD 5 ; var1 is assigned 5
		var2 DD 2 ; var2 is assigned 2
		var3 DD 3 ; var3 is assigned 3
		
segment .bss
		var4 resb 1
```

The following figure shows the value stored in $var4$, along with the register details. The `gdp` parameters are set accordingly to achieve the desired output. Before gdp, ensure the filename is assembled using a nasm assembler and must be error-free. Replace {filename} with the actual filename.

```
gdp {filename}
layout asm
layout regs
watch (int) var4
break _start
run
stepi {to move to the next instruction}
```

<img width="1130" alt="image" src="https://user-images.githubusercontent.com/11669149/224255090-a0559889-2d55-4819-8d4d-81d7087dc68d.png">

## The DIV/IDIV instruction

The division operation generates two elements - a quotient and a remainder. In multiplication, overflow does not occur because double-length registers are used to keep the product. However, in the case of division, overflow may occur. The processor generates an interrupt if overflow occurs.

The DIV (Divide) instruction is used for unsigned data, and the IDIV (Integer Divide) is used for signed data.

The following example divides 8 with 2. Therefore, dividend 8 is stored in the 16-bit AX register, and divisor 2 is stored in the 8-bit BL register.

```{assembly .numberLines}
section .text
		global _start

_start:
		mov ax,8
		mov bl,2
		div bl
	
		mov eax,1
		int 0x80
```

__When the divisor is 1 byte −__The dividend is assumed to be in the AX register (16 bits). After division, the quotient goes to the AL register, and the remainder goes to the AH register.

<img width="402" alt="image" src="https://user-images.githubusercontent.com/11669149/223963271-09306344-30f1-4859-bbb0-e7c76e71a8b6.png">

**When the divisor is 1 word −** The dividend is assumed to be 32 bits long and in the DX:AX registers. The high-order 16 bits are in DX and the low-order 16 bits are in AX. After division, the 16-bit quotient goes to the AX register and the 16-bit remainder goes to the DX register.

**When the divisor is doubleword −**The dividend is assumed to be 64 bits long and in the EDX:EAX registers. The high-order 32 bits are in EDX and the low-order 32 bits are in EAX. After division, the 32-bit quotient goes to the EAX register and the 32-bit remainder goes to the EDX register.

### Example code

The following debugged code shows the process of division (8/2); the AL register (quotient) value is 4, and the AH register (remainder) is 0.

<img width="795" alt="image" src="https://user-images.githubusercontent.com/11669149/223955017-7736aa43-8407-47ac-84de-cfcfb0df7fe6.png">

------

Last updated: Mar 2023
