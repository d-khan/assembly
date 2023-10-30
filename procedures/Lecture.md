# Procedures

Procedures or subroutines are very important in assembly language, as the assembly language programs tend to be large. Procedures are identified by name. Following this name, the procedure's body is described, which performs a well-defined job. A return statement indicates the end of the procedure.

**Syntax**

``` assembly
proc_name:
	procedure body
	...
	ret
```

**Difference between a procedure and a function**  
A function that returns no value or returns a null value is sometimes called a procedure. Procedures usually modify their arguments and are a core part of procedural programming.

## Example code 1

``` assembly
section .text
	global _start

_start:
	mov eax,10
	mov ebx,20
	call sum		;calling sum procedure
	mov eax,1
	int 0x80

sum:
	add eax,ebx
	ret
```

Run the above code and use gdb to debug the code. Assume the filename is `example.asm`. Use `run.sh` script to run the code. [Click here to get the details of how to run the code](https://sdccd-edu.zoom.us/rec/share/Heesw_hE-h9W58AAEX5HiNeiK4EsemWVhI5Vo7bCgeaG_ZrgPhmz-fUk2-tOmvFS.KVW8wyIHQqL2A2dd?startTime=1678767400000) 

```
gdb example
layout asm
layout regs
run _start
stepi
```

**Move the subprocedure below the _start: and verify if the code runs. Discuss the outcome with your classmates**

## Example code 2

In this example, two procedures are defined. The eax register takes an integer number and displays the result on the terminal. The eax register takes integer 65, save the result in the memory, move the res variable memory address to the ecx register, and then sends the output to the screen. Before sending the output to the screen, the ecx register contains the memory address of the res variable. Since eax, ebx, and edx registers are reserved for displaying data, only the ecx register contains the data to be displayed. As discussed before, when the numbers are displayed on the screen or entered from the keyboard, they are in ASCII form. The following example will print **A** on the terminal.

``` assembly
section .text
        global _start

_start:
        mov eax,65
        mov [res],eax
        mov ecx,res
        call output
        call exit

output:
        mov edx,1       ;output length
        mov ebx,1       ;stdout
        mov eax,4       ;system call (sys_write)
        int 0x80        ;interrupt kernel
        ret

exit:
        mov eax,1
        int 0x80

segment .bss
        res resb 1
```

**Note: Run the code and see the results on the terminal. No need to run gdb**

# Stacks

A stack is an array-like data structure in the memory in which data can be stored and removed from a location called the 'top' of the stack. The data that needs to be stored is 'pushed' into the stack and data to be retrieved is 'popped' out from the stack. Stack is a LIFO data structure, i.e., the data stored first is retrieved last.

Assembly language provides two instructions for stack operations: PUSH and POP. These instructions have syntaxes like −

```assembly
push	operand
pop	address/register
```

The memory space reserved in the stack segment is used for implementing stack. The registers SS and ESP (or SP) are used for implementing the stack. The top of the stack, which points to the last data item inserted into the stack is pointed to by the SS:ESP register, where the SS register points to the beginning of the stack segment and the SP (or ESP) gives the offset into the stack segment.

The stack implementation has the following characteristics −

- Only **words** or **doublewords** could be saved into the stack, not a byte.
- The stack grows in the reverse direction, i.e., toward the lower memory address
- The top of the stack points to the last item inserted in the stack; it points to the lower byte of the last word inserted.

## Example code 1

Run the code below and observe the results. Use gdb to debug.

``` assembly
section .text
        global _start

_start:
	mov eax,10
	push eax		;10 is saved in the stack
	mov eax,20
	pop eax			;10 is removed from the stack and saved in the eax

	mov eax,1
	int 0x80
```
Run the above code and use gdb to debug the code. Assume the filename is `example.asm`. Use `run.sh` script to run the code. [Click here to get the details of how to run the code](https://sdccd-edu.zoom.us/rec/share/Heesw_hE-h9W58AAEX5HiNeiK4EsemWVhI5Vo7bCgeaG_ZrgPhmz-fUk2-tOmvFS.KVW8wyIHQqL2A2dd?startTime=1678767400000) 
```
gdb example
layout asm
layout regs
run _start
stepi
```

