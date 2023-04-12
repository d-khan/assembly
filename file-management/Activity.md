

# Activity - File management

## Objective

Learn to perform file management in Assembly Language.

## Prerequisites

- Before doing the lab, please review the lecture.
- This lab will only work if you run the code on a Linux platform using an Intel x86 platform. The online assembler will not work due to the lack of debugging features.
- Knowledge of how to run assembly code using nasm assembler in Linux OS.
- Knowledge of how to debug an assembly code using `gdb`.

## Task

Perform the following tasks:

1. Create a text-based file called "quotes.txt" and add the following contents (4 marks)

> *To be, or not to be, that is the question.*
>
> *A fool thinks himself to be wise, but a wise man knows himself to be a fool.*

2.  Append the following quotes in the same file. (5 marks)

> *Better three hours too soon than a minute too late.*
>
> *No legacy is so rich as honesty.*

### How to append?
For updating a file, perform the following tasks −

- Put the system call sys_lseek () number 19, in the EAX register.
- Put the file descriptor in the EBX register.
- Put the offset value in the ECX register.
- Put the reference position for the offset in the EDX register.
- The reference position could be:

Beginning of file - value 0
Current position - value 1
End of file - value 2

The system call returns, in case of error, the error code in the EAX register.

## What to submit?

1. What were your challenges in performing the lab (from design to the implementation phases)? (1 mark)
2. Working and error-free code. (9 marks)

## How to submit it?

- Upload the work in Canvas and clearly define your responses.
- Upload the code in __.txt__ format and include comments to describe the code.
- __Do not compress or zip your work.__

## Deadline

The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric

- All the questions are answered, and the working code is submitted. (Grade 100%)
- Questions are partially answered, and the code has errors or incorrect output. (Grade 50%)

------

Last updated: Mar 2023 by Dr. Danish Khan. 
