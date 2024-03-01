# Lab: Assembly language (ARM processors)

## Objectives
Writing a code in assembly language on ARM processors

## Tasks
Perform the following tasks:  
1. Research and find out how different assembly language is for ARM processors compared to Intel processors.
2. The following assembly code is written for an Intel 32-bit processor. Convert the code for the ARM processor, and execute it.

## What do you think I should submit?
1. Share the source code and write down the commands used to make the source code executable.  
2. Create and share a video that explains the process of assembling, linking, running, and debugging the source code.

$var4 = (var1+var2)*var3$

```assembly
section .text
    global _start

_start:
    mov eax,[var1]
    add eax,[var2]
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


  
## How to submit it?
Upload your code in Git Hub and share the repository on Canvas.

## Deadline
The deadlines are posted on the Canvas.

## Rubric
- The code is shared, and it's working; the video explains the process of assembling, linking, running, and debugging. (10 marks)  
- The code is not shared, but the video explains the code. (4 marks)
- The code is shared but not working, regardless of the video showing the working solution. (0 marks)
