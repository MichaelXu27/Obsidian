# Your First Program

## Your first register

- x86 intel based architecture so mov (destination, source)
- rax is a small part of the x86 cpu
- mov is the instruction used to move data
- an assembly program file should have the extension of '.s'
## Your first Syscall
- program crashes what happens
- starting and stopping handled by OS
- programs interact with the OS via the cpu using the syscall
- syscall number of exit is 60
## Exit Codes
- every program exists with an exit code (42 in this case)
- this is done by passing a param to the exit system call
- system calls can take multiple parameters 
	- exit only takes one: the exit code
- First param to a system call is rdi
## Building executables
- The steps to build an executable in binary are as follows:
	- write the assembly into a file we will use program.s as an example
	- once written, assemble the assembly into an object file using the `as` command (`as -o program.o program.s)
	- link one or more executable object files int a final executable binary using the `ld` command (`ld -o program program.o`)
- You can prepend a directive to the beginning of the assembly code to show that we are using intel assembly syntax:
	- `.intel_syntax noprefix`
- To silence an error that may show up based on `entry symbol _start:`
	- you can put `.global _start \n _start:`
	- this will basically make _start_ globally visible at the linker
## Moving between registers
- mov also allows you to move between registers
# Software Introspection
## Tracing Syscalls
- `strace` is the syscall tracer
- `execve` system call is what some call a yin to an exit's yang
- in this case it isnt invoked by the program but just picked up by `strace`
- `alarm` system call #37, kills the program when it's frozen,
## Starting GDB
- launching gdb is simple as calling gdb /path/to/binary/file
## Starting programs in GDB
- usually gdb prompt window will look like this:
- (gdb) ..type commands here
# Hello Hackers
- Program write text to screen by invoking a system call
	- this is the write system call
	- syscall # is 1
- File descriptors:
	- FD 0: Standard Input is the channel through which the process takes input
	- FD 1: Standard Output is the channel through which processes output normal data, such as the print of ls
	- FD 2: Standard error is the channel through which processes output error details.
- in the write system call, this is how you specify where to write the data to.
- if you want to write to standard output you would set rdi to 1
- if you want to write to the standard error you would set rdi to 2
- ````c
write(file_descriptor, memory_address, number_of_characters_to_write)
````
For a more concrete example, if you wanted to write 10 characters from memory address `1337000` to standard output (file descriptor 1), this would be:

```c
write(1, 1337000, 10);
```

- 1377000 this is the memory address
code:
```x86
.global _start

_start:

mov rdi, 1
mov rsi, 1337000
mov rdx, 1
mov rax, 1
syscall
```
## Chaining Syscalls
Code:
```
.global _start

_start:
mov rdi, 1
mov rsi, 1337000
mov rdx, 1
mov rax, 1
syscall

mov rdi, 42
mov rax, 60
syscall
```
- this code runs our write but also calls exit to cleanly exit the program
## Writing Strings
- writing a 14 byte string to the terminal
```
.global _start

_start:
mov rdi, 1
mov rsi, 1337000
mov rdx, 14
mov rax, 1
syscall

mov rdi, 42
mov rax, 60
syscall
```

## Reading data
- Code:
- rax should be the syscall number for write or read,
```
.global _start

_start:
mov rdi, 0
mov rsi, 1337000
mov rdx, 8
mov rax, 0
syscall

mov rdi, 1
mov rsi, 1337000
mov rdx, 8
mov rax, 1
syscall

mov rdi, 42
mov rax, 60
syscall
```
[[Debugging Refresher]]

# Computer Memory
## Loading from memory
- to access the memory contents at memory of address 31337 you can do 
- `mov rdi, [31337]
- when executed normally, the cpu understands 31337 as an address, not a raw value
```
.global _start

_start:
mov rdi, [133700]
mov rax, 60
syscall
```
## Dereferencing Pointers
- Typically memory address are stored in pointers
- an example of dereferencing the pointer is if an address 133700 has the contents 42. then we do
- `mov rax, 133700`
- mov rdi, [rax]
```
.global _start

_start:
mov rdi, [rax]
mov rax, 60
syscall
```
## Dereferencing yourself
```assembly
mov [133700], 42
mov rax, 133700  # after this, rax will be 133700
mov rax, [rax]   # after this, rax will be 42
```
- Solution
```
.global _start

_start:
mov rdi, [rdi]
mov rax, 60
syscall
```

## Dereferencing with offsets
![[Pasted image 20250909103955.png]]

- If i want the second number of the sequence I would do `mov rax, [rdi + 1]`
- we call each of these slots bytes
- If we want to get something at offset 8
```
.global _start

_start:
mov rdi, [rdi + 8]
mov rax, 60
syscall
```
## Stored addresses
```assembly
mov rdi, 123400    # after this, rdi becomes 123400
mov rdi, [rdi]     # after this, rdi becomes the value stored at 123400 (which is 133700)
mov rax, [rdi]     # here we dereference rdi, reading 42 into rax!
```
- solution
```
.global _start

_start:
mov rdi, [567800]
mov rdi, [rdi]
mov rax, 60
syscall
```
## Double dereference
- solution
```
.global _start

_start:
mov rdi, [rax]
mov rdi, [rdi]
mov rax, 60
syscall
```
## Triple Dereference
- solution
```
.global _start

_start:
mov rdi, [rdi]
mov rdi, [rdi]
mov rdi, [rdi]
mov rax, 60
syscall
```


# Assembly Crash Course
## Building programs:
- Assembly to binary, program should start with
```
.intel_syntax noprefix
.global _start

_start:
mov rdi, 42
mov rax, 60
syscall
```
- run program like any other `./program_name`
- check return code with `echo $?`
- disassembly of program
	- `/objdump -M intel -d quitter`
## set-register
- File written like this
```
.intel_syntax noprefix
.global _start

_start:
        mov rdi, 0x1337
        mov rax, 60
        syscall
```
- make sure to have the .intel_syntax noprefix in order to not use at&T syntax
- and then compile with `gcc -c -o /tmp/solve.o /tmp/solve.s`
## Set multiple registers
```
.intel_syntax noprefix
.global _start

_start:
        mov rax, 0x1337
        mov r12, 0xCAFED00D1337BEEF
        mov rsp, 0x31337

```
## Add-to-register
- When we say `A+=B` we are really saying `A = A + B`
- add to add
- sub to substract
- imul to multiply
```
.intel_syntax noprefix
.global _start

_start:
        add rdi, 0x331337
        mov rax, 60
        syscall
```
## Linear equation registers
```
.intel_syntax noprefix
.global _start

_start:
        imul rdi, rsi
        add rdi, rdx
        mov rax, rdi

```
- make sure to know the difference between imul and mul
## Integer-division
- `div` is a special instruction that can divide a 128 bit dividend by a 64 bit divisor while storing both the quotient and the remainder.
- `div reg` the following happens:
	- `rax = rdx:rax /reg` (rdx:rax means rdx has upper 64 bits and rax has lower 64 bits)
	- `rdx = remainder`
```
.intel_syntax noprefix
.global _start

_start:
        mov rax, rdi
        xor edx, edx
        div rsi

```
## Modulo:
- simply the remainder of the division operation, that value is already stored
## Set-upper-byte
![[Pasted image 20250910162236.png]]
```
.intel_syntax noprefix
.global _start

_start:
        mov ah, 0x42
```
## Efficient-modulo
Got it ✅ This level is about using the **bit-trick** for modulo when the divisor is a power of 2:

- `x % 256` → keep only the **lowest 8 bits** of `x`.
    
- `x % 65536` → keep only the **lowest 16 bits** of `x`.
    

In x86-64, you can directly move those “low parts” of a register:

- `%rdi` → `%dil` (low 8 bits of `rdi`).
    
- `%rsi` → `%si` (low 16 bits of `rsi`).
    

---

### Intel syntax solution

`.intel_syntax noprefix .globl _start _start:     mov al, dil     ; rax = rdi % 256  (mov into low 8 bits of rax)     mov bx, si      ; rbx = rsi % 65536 (mov into low 16 bits of rbx)     hlt`

## Byte Extraction
