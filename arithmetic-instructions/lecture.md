# Arithmetic Instructions

Let's explore some arithmetic instructions.

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

However, like other instructions, memory-to-memory operations are not possible using ADD/SUB instructions. An ADD or SUB operation sets or clears the overflow and carry flags.

The following example will ask for two digits from the user, store the digits in the EAX and EBX register, add the values, store the result in a memory location 'res', and finally display the result.

``` assembly
SYS_EXIT  equ 1
SYS_READ  equ 3
SYS_WRITE equ 4
STDIN     equ 0
STDOUT    equ 1

segment .data 

   msg1 db "Enter a digit ", 0xA,0xD 
   len1 equ $- msg1 

   msg2 db "Please enter a second digit", 0xA,0xD 
   len2 equ $- msg2 

   msg3 db "The sum is: "
   len3 equ $- msg3

segment .bss

   num1 resb 2 
   num2 resb 2 
   res resb 1    

section	.text
   global _start    ;must be declared for using gcc
	
_start:             ;tell linker entry point
   mov eax, SYS_WRITE         
   mov ebx, STDOUT         
   mov ecx, msg1         
   mov edx, len1 
   int 0x80                

   mov eax, SYS_READ 
   mov ebx, STDIN  
   mov ecx, num1 
   mov edx, 2
   int 0x80            

   mov eax, SYS_WRITE        
   mov ebx, STDOUT         
   mov ecx, msg2          
   mov edx, len2         
   int 0x80

   mov eax, SYS_READ  
   mov ebx, STDIN  
   mov ecx, num2 
   mov edx, 2
   int 0x80        

   mov eax, SYS_WRITE         
   mov ebx, STDOUT         
   mov ecx, msg3          
   mov edx, len3         
   int 0x80

   ; moving the first number to eax register and second number to ebx
   ; and subtracting ascii '0' to convert it into a decimal number
	
   mov eax, [num1]
   sub eax, '0'
	
   mov ebx, [num2]
   sub ebx, '0'

   ; add eax and ebx
   add eax, ebx
   ; add '0' to convert the sum from decimal to ASCII
   add eax, '0'

   ; storing the sum in memory location res
   mov [res], eax

   ; print the sum 
   mov eax, SYS_WRITE        
   mov ebx, STDOUT
   mov ecx, res         
   mov edx, 1        
   int 0x80

exit:    
   
   mov eax, SYS_EXIT   
   xor ebx, ebx 
   int 0x80
```

> **segment .bss** An assembly language code that contains statically allocated variables that are declared but have not been assigned a value yet. It is often called the "bss section" or "bss segment".

## The MUL/IMUL instruction

There are two instructions for multiplying binary data. The MUL (Multiply) instruction handles unsigned data and the IMUL (Integer Multiply) handles signed data. Both instructions affect the Carry and Overflow flag.

> **Depending upon the size of the multiplicand, the multiplier, and the generated product, the product is either stored in one register or two registers depending upon the size of the operands.**

When two bytes are multiplied, the multiplicand is in the AL register, and the multiplier is a byte in the memory or another register. The product is in the eax register, as shown in the debugger's output. However, this is not a restriction, and any size of the register can be used for operands. For efficiency purposes, I used AL and DL registers. The distinction between registers is shown in the figure below.

````assembly
section .text
		global _start
		
_start:
		mov al,10
		mov dl,25
		mul dl
		
		mov eax,1
		int 0x80
```
````



<img width="1250" alt="image" src="https://user-images.githubusercontent.com/11669149/223907405-4e765993-af50-469f-a77b-88b995a6f05d.png">

> **When referring to registers in assembly language, the names are not case-sensitive. For example, the names `EAX` and `eax` refer to the same register.**

The following figure shows the **x86 Registers**.

![image-20230308225733906](/Users/danish/Library/Application%20Support/typora-user-images/image-20230308225733906.png)


