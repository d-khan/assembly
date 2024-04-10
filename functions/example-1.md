```assembly
section .text
        global _start

; the function performs result = num1 + num2


_foobar:
        push ebp
        mov ebp, esp
        sub esp, 4
        mov eax, DWORD[ebp+8]    ;this should have 20 
        mov ebx, DWORD[ebp+12]   ;this should have 10
        add eax,ebx  ; alternatively lea eax, [eax, ebx]


_start:
        push DWORD[num1]
        push DWORD[num2]
        call _foobar

        mov eax, 1
        int 0x80


section .data
        num1 dd 10
        num2 dd 20
        mov DWORD[ebp-4], eax   ;saving the addition into the function locally

segment .bss
  result resb 1
```

        mov [result], eax       ;result is a global variable here
        leave
                                    
