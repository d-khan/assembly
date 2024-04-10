# Functions in Assembly Language

When a function is called, a stack frame is created to support the function’s execution. The stack frame contains the function’s local variables and the arguments passed to the function by its caller. The frame also contains housekeeping information that allows the called function (the callee) to return to the caller safely. The exact contents and layout of the stack vary by processor architecture and function call convention.

The stack is a last in, first out (LIFO) structure, the data stored first is retrieved last. Values are placed onto the stack via `push` and removed via `pop`.

To keep track of the stack, the system uses the base pointer `ebp` and the stack pointer `esp`, whereas `esp` points to the top of the stack and `ebp` points to the bottom of the stack. In the Intel architecture, as the program adds data to the stack, the stack grows downward from high to low. When items are removed from the stack, the stack shrinks upward from low to high memory. When a word value is pushed onto the stack, the memory address of `esp` decreases by 2 bytes, and when a word value is popped off the stack, the memory address of `esp` increases by 2 bytes. When a double word value is pushed onto/popped off the stack, the memory address of `esp` decreases/increases by 4 bytes.

<img width="400" alt="image" src="https://user-images.githubusercontent.com/11669149/235361036-c88c7910-a6e7-4946-8a92-4d002bd078ed.png">

So when we say “top of the stack” on x86, we actually mean the lowest address in the memory area occupied by the stack.

To push new data onto the stack, we use the `push` instruction. What `push` does is first decrement `esp` by 4, and then store its operand in the location `esp` points to.

```assembly
push eax
;means
sub esp,4
mov [esp],eax
```

Similarly, the `pop` instruction takes a value off the top of the stack and places it in its operand, increasing the stack pointer afterwards.

```assembly
pop eax
;means
mov eax,[esp]
add esp,4
```

The function has three components: function prologue, function body, and function epilogue. The purpose of the function prologue is to save the previous state of the program and set up the stack for the function's local variables. The function body is usually responsible for some unique and specific task. This part of the function may contain various instructions, branches (jumps) to other functions, etc. The function epilogue is used to restore the program’s state to its initial.

Let’s take a look at an example

```assembly
;;; ;------------------------------------------------------
;;; ;------------------------------------------------------
;;; ; _foobar: needs 3 arguments. The arguments are pushed onto the stack before calling this function.
;;; ;
;;; ; Examples:
;;; ;          push    110
;;; ;          push    45
;;; ;          push    67
;;; ;          call _foobar
;;; ;
;;; ;REGISTERS MODIFIED: EAX
;;; ;------------------------------------------------------
;;; ;------------------------------------------------------
_foobar:
    ; ebp must be preserved across calls. Since
    ; this function modifies it, it must be
    ; saved.
    ;
    push    ebp

    ; From now on, ebp points to the current stack
    ; frame of the function
    ;
    mov     ebp, esp

    ; Make space on the stack for local variables
    ;
    sub     esp, 16

    ; eax <-- a. eax += 2. then store eax in xx
    ;
    mov     eax, DWORD[ebp+8]
    add     eax, 2
    mov     DWORD[ebp-4], eax

    ; eax <-- b. eax += 3. then store eax in yy
    ;
    mov     eax, DWORD[ebp+12]
    add     eax, 3
    mov     DWORD[ebp-8], eax

    ; eax <-- c. eax += 4. then store eax in zz
    ;
    mov     eax, DWORD[ebp+16]
    add     eax, 4
    mov     DWORD[ebp-12], eax

    ; add xx + yy + zz and store it in sum
    ;
    mov     eax, DWORD[ebp-8]
    mov     edx, DWORD[ebp-4]
    lea     eax, [edx+eax]
    add     eax, DWORD[ebp-12]
    mov     DWORD[ebp-16], eax

    ; Compute final result into eax, which
    ; stays there until return
    ;
    mov     eax, DWORD[ebp-4]
    imul    eax, DWORD[ebp-8]
    imul    eax, DWORD[ebp-12]
    add     eax, DWORD[ebp-16]

    ; The leave instruction here is equivalent to:
    ;
    ;   mov esp, ebp
    ;   pop ebp
    ;
    ; Which cleans the allocated locals and restores
    ; ebp.
    ;
    leave
    ret

section .text
        global _start
_start:
     push    34
     push    59
     push    98
     call    _foobar

     mov     eax, 1
     int     0x80

```

Let's examine the stack

```assembly
push 34
push 59
push 98
```

First, three values are pushed onto the stack.

<img width="300" alt="image" src="https://user-images.githubusercontent.com/11669149/235361551-b326ea44-48b3-4aa5-aad4-cda7931068d8.png">

```assembly
call _foobar
```

Next, we call the function _foobar. To return to the caller, a function must have the correct return address. `call` instruction will push the return address onto the stack before jumping to the target address.

<img width="574" alt="image" src="https://user-images.githubusercontent.com/11669149/235361745-97ad8b0f-a99a-4392-b175-c1a4a12aef65.png">

```assembly
push ebp
```

This instruction saves the value of register `ebp` to the stack.

<img width="600" alt="image" src="https://user-images.githubusercontent.com/11669149/235361927-748e2315-0a14-40e3-9a5f-6b1e0d276c77.png">

```assembly
mov ebp,esp
```

This instruction will make register `ebp` point to the same location as register `esp`.

<img width="600" alt="image" src="https://user-images.githubusercontent.com/11669149/235362005-dbb1e8f4-c8f5-4814-8f97-d026e32c8d7a.png">

```assembly
sub esp,16
```

This instruction makes empty space on the stack for local variables.

<img width="611" alt="image" src="https://user-images.githubusercontent.com/11669149/235362176-1989991d-2df3-43dc-ba4c-8c3d630027dc.png">

```assembly
mov     eax, DWORD[ebp+8]
add     eax, 2
mov     DWORD[ebp-4], eax
```

<img width="623" alt="image" src="https://user-images.githubusercontent.com/11669149/235362256-26c08f60-cfa3-4148-801f-702b11ceb2c5.png">

```assembly
mov     eax, DWORD[ebp+12]
add     eax, 3
mov     DWORD[ebp-8], eax
```

<img width="609" alt="image" src="https://user-images.githubusercontent.com/11669149/235363168-340e9f06-ee90-47a6-9783-98be521983c1.png">

```assembly
mov     eax, DWORD[ebp+16]
add     eax, 4
mov     DWORD[ebp-12], eax
```

<img width="609" alt="image" src="https://user-images.githubusercontent.com/11669149/235363284-6fa58895-ab23-4ab7-a917-59552332c211.png">



```assembly
mov     eax, DWORD[ebp-8]
mov     edx, DWORD[ebp-4]
lea     eax, [edx+eax]
add     eax, DWORD[ebp-12]
mov     DWORD[ebp-16], eax
```

<img width="644" alt="image" src="https://user-images.githubusercontent.com/11669149/235363410-2fe6e0f1-46cf-433f-a591-a7fa8a79d129.png">

```assembly
mov     eax, DWORD[ebp-4]
imul    eax, DWORD[ebp-8]
imul    eax, DWORD[ebp-12]
add     eax, DWORD[ebp-16]
```

<img width="631" alt="image" src="https://user-images.githubusercontent.com/11669149/235363508-81f44053-fb52-47b6-b5c3-025ae3866604.png">

```assembly
leave
```

After executing the instruction above, local variables will be removed from the stack, register `esp` will point to the return address, and register `ebp` will return to its initial value.

<img width="637" alt="image" src="https://user-images.githubusercontent.com/11669149/235363569-6ff08c90-0aa9-4077-b38b-c4281ced3260.png">

```assembly
ret
```

The `ret` instruction pops the return address off the stack and returns control from a function to the calling program.

<img width="454" alt="image" src="https://user-images.githubusercontent.com/11669149/235363610-29ad5bca-7103-42f4-a88c-b43a1df591ae.png">
