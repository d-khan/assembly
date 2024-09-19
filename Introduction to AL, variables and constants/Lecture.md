# Introduction to Assembly Language

Assembly language is a low-level programming language for a computer or other programmable device specific to a particular computer architecture, unlike most high-level programming languages, which are generally portable across multiple systems. Assembly language is converted into executable machine code by a utility program called an assembler like NASM, MASM, etc.

## Audience

This tutorial has been designed for those who want to learn the basics of assembly programming from scratch. This tutorial will give you enough understanding of assembly programming that you can take yourself to higher levels of expertise.

## Prerequisites

- Before proceeding with this tutorial, you should have a basic understanding of Computer Programming terminologies. Basic knowledge of any programming language will help you understand the Assembly programming concepts and move fast on the learning track.
- Conversion of numbering systems.

## What is an Assembly Language?

Each personal computer has a microprocessor that manages the computer's arithmetical, logical, and control activities.

Each family of processors has its own set of instructions for handling various operations, such as getting input from the keyboard, displaying information on the screen, and performing different other jobs. This set of instructions is called 'machine language instructions.

A processor understands only machine language instructions, which are strings of 1's and 0's. However, machine language needs to be more obscure and complex for software development. So, the low-level assembly language is designed for a specific family of processors representing various symbolic code instructions and a more understandable form.

## Advantages of Assembly Language

Having an understanding of assembly language makes one aware of 

- How programs interface with OS, processor, and BIOS;
- How data is represented in memory and other external devices;
- How the processor accesses and executes instructions;
- How instructions to access and process data;
- How a program accesses external devices.

Other advantages of using assembly language are −

- It requires less memory and execution time;
- It allows hardware-specific complex jobs more easily;
- It is suitable for time-critical jobs;
- It is most suitable for writing interrupt service routines and other memory resident programs.

## Essential Features of PC Hardware

The main internal hardware of a PC consists of processor, memory, and registers. Registers are processor components that hold data and addresses. To execute a program, the system copies it from the external device into the internal memory. Then, the processor executes the program instructions.

The fundamental unit of computer storage is a bit; it could be ON (1) or OFF (0), and a group of 8 related bits makes a byte on most modern computers.

So, the parity bit is used to make the number of bits in a byte odd. If the parity is even, the system assumes that there had been a parity error (though rare), which might have been caused due to hardware fault or electrical disturbance.

The processor supports the following data sizes −

- Word: a 2-byte data item
- Doubleword: a 4-byte (32-bit) data item
- Quadword: an 8-byte (64-bit) data item
- Paragraph: a 16-byte (128-bit) area
- Kilobyte: 1024 bytes
- Megabyte: 1,048,576 bytes

## Local Environment Setup

Assembly language depends upon the instruction set architecture and the process. In this tutorial, we focus on Intel-32 processors like Pentium. To follow this tutorial, make sure you have watched the [video](https://youtu.be/4IZSh1WVyi8).


## Basic Syntax

An assembly program can be divided into three sections −

- The data section,

- The bss section, and

- The text section.

The __data section__ is used for declaring initialized data or constants. This data does not change at runtime. In this section, you can declare values, file names, buffer sizes, and various constant values.

The syntax for declaring the data section is −

```section.data```

The bss section is used for declaring variables. The syntax for declaring bss section is

```section.bss```

The text section is used for keeping the actual code. This section must begin with the declaration global _start, which tells the kernel where the program execution begins.

The syntax for declaring text section is −

```assembly
section.text
	global _start
_start:
```

Assembly language comment begins with a semicolon (;). It may contain any printable character, including blank. It can appear on a line by itself, like –

```assembly
;This program displays a message on the screen
```

or, on the same line along with an instruction, like –

```assembly
add eax, ebx   ; adds ebx to eax
```

## Assembly Language Statements

Assembly language programs consist of three types of statements −

- Executable instructions or instructions,
- Assembler directives or pseudo-ops, and
- Macros.

The executable instructions or instructions tell the processor what to do. Each instruction consists of an operation code (opcode). Each executable instruction generates one machine language instruction.

The assembler directives or pseudo-ops tell the assembler about the various aspects of the assembly process. Unfortunately, these are non-executable and do not generate machine language instructions.

Macros are a text substitution mechanism.

## Syntax of Assembly Language Statements

Assembly language statements are entered one statement per line. Each statement follows the following format. 

```
[label]   mnemonic   [operands]   [;comment]
```

The fields in the square brackets are optional. A basic instruction has two parts, the first is the name of the instruction (or the mnemonic), which is to be executed, and the second is the operands or the parameters of the command.

## The Hello World program in assembly

The following assembly language code displays the 'Hello World' string on the screen.

```{assembly .numberLines}
section	.text
   global _start		;must be declared for linker (ld)
   				;global is used to export the _start label. 
   				;This will be the entry point to the program. 

_start:	            ;tells linker entry point
   mov	eax,4       ;system call number (sys_write)
   mov	ebx,1       ;file descriptor (stdout)
   mov	ecx,msg     ;message to write, A pointer to the variable 'msg'
   mov	edx,len     ;message length
   int	0x80        ;call kernel
	
   mov	eax,1       ;system call number (sys_exit)
   int	0x80        ;call kernel

section	.data
msg db 'Hello, world!', 0xa  	;string to be printed
				;Declare a label "msg" which has 
                              	;our string we want to print. 
                              	;for reference: 0xa = "\n" (line feed) 
                              	;db = define byte
len equ $ - msg     		;length of the string
				;len" will calculate the current 
				;offset minus the "msg" offset. 
				;this should give us the size of "msg".
                    		;len equals current offset - msg
```

## Compiling and Linking an Assembly Program

[How to execute your first assembly language code](https://sdccd-edu.zoom.us/rec/share/h2iXYblKtPxTjeDgJ4086AW6H-73QlXUZJlskQ3_2Nkew7RqNNeaSwcxUrISrzk.zONixP8fPYoJkrgq?startTime=1687163989000)


## Making Syscalls on X86

Syscalls offer a method to invoke and use functionality in the operating system. For example, syscalls are launched on x86 Linux by invoking an interrupt instruction with the hex value of ```0x80``` (int 0x80).  Before invoking this interrupt, however, you need to set up everything for the syscall. This is because the calling convention for syscalls differs on other architectures, including x86_64, which uses the SYSCALL instruction instead of INT 0x80.  

> __This tutorial is focused on 32-bit x86.__

After the syscall number is set and the registers are loaded with the parameters needed, calling the instruction INT 0x80 will execute the syscall.  If the syscall returns a value, it will be placed in EAX.  For example, opening a file should return a file descriptor or error code in EAX. 

## Data Registers

Four 32-bit data registers are used for arithmetic, logical, and other operations. These 32-bit registers can be used in three ways −

- Complete 32-bit data registers: EAX, EBX, ECX, EDX.
- The lower halves of the 32-bit registers can be used as four 16-bit data registers: AX, BX, CX, and DX.
- Lower and higher halves of the abovementioned four 16-bit registers can be used as eight 8-bit data registers: AH, AL, BH, BL, CH, CL, DH, and DL.

Some of these data registers have a specific use in arithmetical operations.

**AX is the primary accumulator** for input/output and most arithmetic instructions. For example, in a multiplication operation, one operand is stored in EAX or AX, or AL register according to the size of the operand.

**BX is the base register**, which could be used in indexed addressing.

**CX is known as the count register**, as the ECX, CX registers to store the loop count in iterative operations.

**DX is known as the data register**. It is also used in input/output operations. It is also used with AX register and DX for multiply and divide operations involving large values.

## Code description

__Line 7:__ We will first set EAX to the syscall number we want to invoke.  As mentioned in our previous section, the syscall number on 32-bit x86 Linux for the write syscall was 4. Therefore, we use a MOV instruction (short for a move) to load the immediate value of 4 into the register EAX, containing the syscall number we want to run.  The syntax for the move instruction in NASM is “MOV <destination>, <source>”.  

__Lines 8-10:__ These instructions are set parameters for the write syscalls.  The register EBX  needs to contain the file descriptor integer that we want to write to, ECX needs to contain a pointer to the data buffer we want to write to the file descriptor, and EDX needs to contain the number of bytes from the data buffer we want to write out to the file descriptor.  It’s pretty straightforward using MOV instructions to do this. 

__Lines 13-14:__ Calling *sys_exit* at the end of all our programs will mean the kernel knows precisely when to terminate the process and return memory to the general pool, thus avoiding an error.

__Lines 16+__: We use the msg and len variables.  These variables enable us to update the message, and the message length should also be automatically updated. 

## Variables

NASM provides various **define directives** for reserving storage space for variables. The define assembler directive is used for the allocation of storage space. It can be used to reserve and initialize one or more bytes.

### Allocating Storage Space for Initialized Data

The syntax for storage allocation statement for initialized data is −

```[variable-name]    define-directive    initial-value   [,initial-value]...```

where *variable-name* is the identifier for each storage space. The assembler associates an offset value for each variable name defined in the data segment.

There are five basic forms of the define directive −

| Directive | Purpose            | Storage space      |
| --------- | ------------------ | ------------------ |
| DB        | Define Byte        | Allocates 1 byte   |
| DW        | Define Word        | Allocates 2 bytes  |
| DD        | Define Doubleword  | Allocates 4 bytes  |
| DQ        | Define Quadword    | Allocates 8 bytes  |
| DT        | Define Ten Bytes   | Allocates 10 bytes |

```
choice		DB	'y'
number		DW	12345
neg_number	DW	-12345
big_number	DQ	123456789
real_number1	DD	1.234
real_number2	DQ	123.456
```

Please note that −

- Each byte of character is stored in hexadecimal.
- Each decimal value is automatically converted to its 16-bit binary equivalent and stored as a hexadecimal number.
- Processor uses the little-endian byte ordering.
- Negative numbers are converted to its 2's complement representation.
- Short and long floating-point numbers are represented using 32 or 64 bits, respectively.

The following program shows the use of define directive −

```
section .text
   global _start          ;must be declared for linker (gcc)
	
_start:                   ;tell linker entry point
   mov	edx,1		  ;message length
   mov	ecx,choice        ;message to write
   mov	ebx,1		  ;file descriptor (stdout)
   mov	eax,4		  ;system call number (sys_write)
   int	0x80		  ;call kernel

   mov	eax,1		  ;system call number (sys_exit)
   int	0x80		  ;call kernel

section .data
choice DB 'y'
```

When the above code is compiled and executed, it produces the following result −

```
y
```

### Allocating Storage Space for Uninitialized Data

The reserve directives are used for reserving space for uninitialized data. The reserve directives take a single operand specifying the number of space units to be reserved. Each define directive has a related reserve directive.

There are five basic forms of the reserve directive −

| Directive | Purpose              |
| --------- | -------------------- |
| RESB      | Reserve a Byte       |
| RESW      | Reserve a Word       |
| RESD      | Reserve a Doubleword |
| RESQ      | Reserve a Quadword   |
| REST      | Reserve a Ten Bytes  |

The following example shows how uninitialized variables are used in AL.

```
section .text
        global _start

_start:
        mov eax,1					;assign eax register to 1
        mov [result],eax	;transfer eax content to the variable
        mov eax,1					;set eax register to 1
        int 0x80					;interrupt 0x80

segment .bss
        result resb 1			;uninitialized variable result

```

## Constants

There are several directives provided by NASM that define constants. There are three directives

- EQU
- %assign
- %define

### The EQU Directive

The **EQU** directive is used for defining constants. The syntax of the EQU directive is as follows −

```
CONSTANT_NAME EQU expression
```

For example:

```
TOTAL_STUDENTS equ 50
```

```
LENGTH equ 20
WIDTH  equ 10
AREA   equ length * width
```

Above code segment would define AREA as 200.

The following example illustrates the use of the EQU directive.

```
SYS_EXIT  equ 1
SYS_WRITE equ 4
STDIN     equ 0
STDOUT    equ 1
section	 .text
   global _start    ;must be declared for using gcc
	
_start:             ;tell linker entry point
   mov eax, SYS_WRITE         
   mov ebx, STDOUT         
   mov ecx, msg1         
   mov edx, len1 
   int 0x80                
	
   mov eax, SYS_WRITE         
   mov ebx, STDOUT         
   mov ecx, msg2         
   mov edx, len2 
   int 0x80 
	
   mov eax, SYS_WRITE         
   mov ebx, STDOUT         
   mov ecx, msg3         
   mov edx, len3 
   int 0x80
   
   mov eax,SYS_EXIT    ;system call number (sys_exit)
   int 0x80            ;call kernel

section	 .data
msg1 db	'Hello, programmers!',0xA,0xD 	
len1 equ $ - msg1			

msg2 db 'Welcome to the world of,', 0xA,0xD 
len2 equ $ - msg2 

msg3 db 'Linux assembly programming! '
len3 equ $- msg3
```

When the above code is compiled and executed, it produces the following result:

```
Hello, programmers!
Welcome to the world of,
Linux assembly programming!
```

### The %assign Directive

The **%assign** directive can be used to define numeric constants like the EQU directive. This directive allows redefinition. For example, you may define the constant TOTAL as −

```
%assign TOTAL 10
```

Later in the code, you can redefine it as −

```
%assign  TOTAL  20
```

This directive is case-sensitive.

### The %define Directive

The **%define** directive allows defining both numeric and string constants. This directive is similar to the #define in C. For example, you may define the constant PTR as −

```
%define PTR [EBP+4]
```

The above code replaces *PTR* by [EBP+4].

This directive also allows redefinition and it is case-sensitive.

---

Last updated: Feb 2023 by Dr. Danish Khan.
