# Compile and link script

Copy the following code:

```assembly
#!/bin/bash
nasm -f elf ./$1.asm
ld -m elf_i386 ./$1.o -o ./$1
./$1
```
