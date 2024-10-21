# Loops 

Previously I wrote a code that generates a number from 0 to 9. The code uses several instructions to perform the task. 

```assembly
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

Now I am going to write the same above command but this time using less number of instructions.

## Example code - counter (optimized version)

The ECX is a counter register, and when the loop instruction is executed, the ECX register is decremented, and the control jumps to the target label until the ECX register value, i.e., the counter reaches the value zero. The ECX register decrements by itself, and you don't have to decrement it. The line 7, "inc eac" increments the EAX register to check whether the code inside the label block is working.

```assembly
section .text
        global _start

_start:
        mov ecx,10	;ecx is a counter register
        label:
        dec ecx
        loop label

        mov eax,1
        int 0x80
```

# Arrays

The arrays use consecutive memory space with the same data type. The arrays can be declared as:

__number DD 1,2,3,4,5,6__

The number array has 6 elements, each 4 bytes long. Each element in the array has an address that holds the element's content. Lets explore this further using the example code.

## Example code - adding arrays

```assembly
section .text
        global _start

_start:
        mov eax,3       ;array length (0-2)
        mov ebx,0       ;initializing  ebx 0
        mov ecx,array   ;move array's address from the memory to the register
        								;the array address is equal to the address of 
        								;the first element

top:
        add ebx,[ecx]   ;add content of the array's first element with the ebx
        add ecx,4       ;fetch the next element in the array which is 4 bytes away
        dec eax         ;eax will work as a counter which is equal to the 
                        ;array length
        jnz top         ;jump not zero to the label top

        mov eax,1       
        int 0x80

section .data
        array dd 5,10,15        ;size double data 4 bytes
```

<img width="883" alt="image" src="https://user-images.githubusercontent.com/11669149/226088015-01ea0938-0dd8-4653-ba1e-99a2bfdc13df.png">

The above figure shows the debugging information of the 'counting arrays' code. The arrays are defined with three elements (5,10,15). The memory address of the variable `array` in the code is the same as the memory address of the first element (0x804a000). The second element is 4 bytes away, because the size of each element is declared as DD (define double - 4 bytes). The data in the register is saved in hexadecimal format. Declaring an array means getting consecutive space in the memory. The array is originally declared in the memory.

________

Last updated: Mar 2023
