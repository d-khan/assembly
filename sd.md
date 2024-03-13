# Calculate population standard deviation using assembly language

__This is a group activity (2 members per group)__

## Formulas

### Standard deviation
![Standard deviation](https://github.com/d-khan/assembly/blob/main/SD.PNG?raw=true)

|Name|score|
|----|-------|
|Student 1|60|
|Student 2|70|
|Student 3|90|
|Student 4|40|
|Student 5|65|

## Verification
(Use this link to verify the answer)[https://www.calculator.net/standard-deviation-calculator.html]  
Selection population

# Convert the following
- Convert 575 decimal into binary and hexadecimal
- Convert 0x80 into binary

# Represent the following into negative numbers
- Convert -10 into binary using 1's and 2's complements

# Identify error(s) in the following code
```assembly
section .text
    global _start

_start:
    mov eax,10
    mov ebx,20
    add eax,ebx
    mov result,eax
    
    mov eax,1
    int 0x80

section .data
    result resb 1
```


