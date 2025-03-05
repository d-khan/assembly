iqr fuqrbf iuqbefi qnofqf
eqrgeqr

```assembly
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
