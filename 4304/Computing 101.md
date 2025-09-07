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