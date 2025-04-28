**The code below is used to display three digit numbers on the console**

```assembly
section .text
        global _start

_start:
	; the number 100 will be printed on the terminal
	mov eax, 100
        cmp eax, 9
        jg calculate
        call display_2
        call exit

calculate:
        mov ebx, 10
        div ebx
        push edx        ;edx holds remainder
        cmp eax, 9
        jg calculate
        push eax        ;eax holds quotient

        pop eax         ;
        add eax, 48
        mov [result], eax
        call display

        pop eax
        add eax, 48
        mov [result], eax
        call display

        pop eax
        add eax, 48
        mov [result], eax
        call display

        call linefeed
        call exit

display:
        mov eax, 4
        mov ebx, 1
        mov ecx, result
        mov edx, 1
        int 0x80
	ret
		        
linefeed:
        mov eax, 4
        mov ebx, 1
        mov ecx, space
        mov edx, 1
        int 0x80
        ret

display_2:
        add eax, 48
        mov [result], eax
        call display
        call linefeed
        ret
exit:
        mov eax, 1
        int 0x80

section .bss
        result resb 1
        ;counter resb 1
        
section .data
        space db 0xa
```
