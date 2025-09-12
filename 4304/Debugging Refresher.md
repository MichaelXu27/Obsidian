# Level 1:
- running /challenge/embryogdb_level1
- just run it with gdb and type in r and then continue
- https://sourceware.org/gdb/current/onlinedocs/gdb#Starting
- https://sourceware.org/gdb/current/onlinedocs/gdb#Continuing-and-Stepping
# Level 2:
- when in debugger, if you do `info registers` you can get the values of all the registers at that current moment
- to print the value of a register `p $rdi`, always put $ in front of the register
- `p/x $register` will print the register value in hex
# Level 3
- You can examine the contents of memory using the command below
	- `x/<n><u><f> <address>`
		- `<u>` is the unit size to display
			- b, 1 byte
			- h, 2 bytes
			- w, 4 bytes
			- g, 8 bytes
			- d, decimal
			- s, string
			- i, instructions
		- `<n>`  is the number of elements to display
		- `<f>` is the format to display it in
	- For example, `x/8i $rip` will print the next 8 instructions from the current instruction pointer. `x/16i main` will print the first 16 instructions of main. You can also use `disassemble main`, or `disas main` for short, to print all of the instructions of main. Alternatively, `x/16gx $rsp` will print the first 16 values on the stack. `x/gx $rbp-0x32` will print the local variable stored there on the stack.
## Level 4
There are a number of ways to move forward in the program's execution. You can use the `stepi <n>` command, or `si <n>` for short, in order to step forward one instruction. You can use the `nexti <n>` command, or `ni <n>` for short, in order to step forward one instruction, while stepping over any function calls. The `<n>` parameter is optional, but allows you to perform multiple steps at once. You can use the `finish` command in order to finish the currently executing function. You can use the `break *<address>` parameterized command in order to set a breakpoint at the specified-address. You have already used the `continue` command, which will continue execution until the program hits a breakpoint.

While stepping through a program, you may find it useful to have some values displayed to you at all times. There are multiple ways to do this. The simplest way is to use the `display/<n><u><f>` parameterized command, which follows exactly the same format as the `x/<n><u><f>` parameterized command. For example, `display/8i $rip` will always show you the next 8 instructions. On the other hand, `display/4gx $rsp` will always show you the first 4 values on the stack. Another option is to use the `layout regs` command. This will put gdb into its TUI mode and show you the contents of all of the registers, as well as nearby instructions.

In order to solve this level, you must figure out a series of random values which will be placed on the stack. As before, `run` will start you out, but it will interrupt the program and you must, carefully, continue its execution.
