# File management

The system considers any input or output data as stream of bytes. There are three standard file streams −

- Standard input (stdin),
- Standard output (stdout), and
- Standard error (stderr).

A **file descriptor** is a 16-bit integer assigned to a file as a file id. When a new file is created, or an existing file is opened, the file descriptor is used for accessing the file.

The file descriptor of the standard file streams - **stdin, stdout,** and **stderr** are 0, 1, and 2, respectively.

A **file pointer** specifies the location for a subsequent read/write operation in the file in terms of bytes. Each file is considered a sequence of bytes. Each open file is associated with a file pointer that specifies an offset in bytes relative to the beginning of the file. When a file is opened, the file pointer is set to zero.

## File handling system calls

The following table briefly describes the system calls related to file handling −

| %eax |   Name    |      %ebx      |     %ecx     |     %edx     |
| :--: | :-------: | :------------: | :----------: | :----------: |
|  2   | sys_fork  | struct pt_regs |      -       |      -       |
|  3   | sys_read  |  unsigned int  |    char *    |    size_t    |
|  4   | sys_write |  unsigned int  | const char * |    size_t    |
|  5   | sys_open  |  const char *  |     int      |     int      |
|  6   | sys_close |  unsigned int  |      -       |      -       |
|  8   | sys_creat |  const char *  |     int      |      -       |
|  19  | sys_lseek |  unsigned int  |    off_t     | unsigned int |

## Creating a file

To create a file, perform the following tasks −

- eax register = 8. This is to call `sys_creat()`
- ebx register = filename
- ecx register = file permissions

Read about [file permissions here](https://www.redhat.com/sysadmin/linux-file-permissions-explained)

The system call returns the file descriptor of the created file in the EAX register; in case of an error, the error code is in the EAX register.

### Example - creating a new file

``` assembly
SECTION .text
global  _start
 
_start:
 
        mov     ecx, 0711o ; set all permissions to read, write, execute (octal format)
        mov     ebx, filename       ; filename we will create
        mov     eax, 8              ; invoke SYS_CREAT (kernel opcode 8)
        int     0x80                ; call the kernel

        mov     eax,1
        int     0x80

SECTION .data
filename db 'readme.txt', 0h    ; the filename to create
```

Compile and run. You should be able to see the `readme.txt` file. Use `ls -l read*` command to check the file with permission.

## Opening a file
For opening an existing file, perform the following tasks 
- eax register = 5. This is to call `sys_open()`
- ebx register = file name
- ecx register = file access mode
- edx register = file permissions

The system call returns the file descriptor of the created file in the EAX register, in case of error, the error code is in the EAX register.

Among the file access modes, most commonly used are: read-only (0), write-only (1), and read-write (2).

## Writing a file

For writing to a file, perform the following tasks

- eax register = 4. This is to call `sys_write()`
- ebx register = file descriptor
- ecx register = pointer to the output buffer
- edx register = buffer size (the number of bytes to write)

The system call returns the actual number of bytes written in the EAX register, in case of error, the error code is in the EAX register.

### Example - open and write to a file

``` assembly
SECTION .data
        filename db 'readme.txt', 0h    ; the filename to create
        contents db 'Hello world!', 0h  ; the contents to write
 
SECTION .text
        global  _start
 
_start:
        ;file open operation
        ;assuming that the file has already been created.
        ;If the readme.txt file is not created, then crrate a file
        ;using the example above.
        mov eax, 5					;file handling system call
        mov ebx, filename
        mov ecx, 1
        mov edx, 0777o
        int 0x80

        mov [fd_out],eax

        ;file write operation
        mov eax, 4					;file handling system call
        mov ebx, [fd_out]   ;file descriptor
        mov ecx, contents
        mov edx, 12         ;number of bytes written
        int 0x80

        mov eax, 1
        int 0x80

section .bss
        fd_out resb 1
```

## Closing a file
- eax register = 6. This is to call `sys_close()`
- ebx register = file descriptor
In case of an error, the system call returns the error code in the EAX register.

### Example - open, write, and close

```assembly
SECTION .data
        filename db 'readme.txt', 0h    ; the filename to create
        contents db 'Hello world!', 0h  ; the contents to write
 
SECTION .text
        global  _start
 
_start:

        ;file open operation
        mov eax, 5					;file handling system call
        mov ebx, filename
        mov ecx, 1
        mov edx, 0777o
        int 0x80

        mov [fd_out],eax

        ;file write operation
        mov eax, 4					;file handling system call
        mov ebx, [fd_out]   ;file descriptor
        mov ecx, contents
        mov edx, 12         ;number of bytes written
        int 0x80

        ;file close operation
        mov eax, 6					;file handling system call
        mov ebx, [fd_out]
        int 0x80

        mov eax, 1
        int 0x80

section .bss
        fd_out resb 1
```

------

Last updated Mar 2023

