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
        inc eax
        loop label

        mov eax,1
        int 0x80
```

