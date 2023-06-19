# Activity - Variables and constants

## Objective

Learn how to assign variables and constants

## Prerequisites

- Before doing the lab, please review the lecture.
- Knowledge of how to run an assembly code using nasm assembler in Linux OS

## Task

Write a code in Assembly that uses uninitialized and initialized variables. For example:

- Assign 10 to the variable var1.
- Assign 15 to the variable var2.
- Add var1 and var2 and save them into the result variable.

```
section .text
        global _start

_start:
        ;use this space for the main body of your program
   			;======== write your code below ===========
   			
   			
   			
   			
   			;======== write your code above ===========
        
        mov eax,1					;set eax register to 1 (do not remove this line)
        int 0x80					;interrupt 0x80 (do not remove this line)

segment .bss
        ;use this space for uninitialized variable (result)

segment .data
				;use this space for initialized variables (var1 and var2)
```



To run, ensure you have reviewed the lecture contents, where I have explained how to compile, link and debug the assembly code using `gdb`. Alternatively, you can find the video here as well. [How to execute your first assembly language code](https://sdccd-edu.zoom.us/rec/share/h2iXYblKtPxTjeDgJ4086AW6H-73QlXUZJlskQ3_2Nkew7RqNNeaSwcxUrISrzk.zONixP8fPYoJkrgq?startTime=1687163989000)

When you execute the code on the command line (terminal),  you will not see any output if there is no error. You need to debug your code using `gdb`. 

**Note: You need to set up 'result' as a watch variable in gdb. Then, you should be able to see the sum of var1 and var2. **

## What to submit?

1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io/) very useful. However, you can use any application of your choice. (1 mark)
2. What were your challenges in performing the lab (from design to the implementation phases)? (1 mark)
3. Working and error-free code. (3 marks)

## How to submit it?

- Upload the work in Canvas and clearly define your responses.
- Upload the code in __.txt__ format and include comments to describe the code.
- Do not compress or zip your work.

## Deadline

The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric

- All the questions are answered, and the working code is submitted. (Grade 100%)
- Questions are partially answered, and the code has errors or incorrect output. (Grade 50%)

------

Last updated: Feb 2023 by Dr. Danish Khan. 

