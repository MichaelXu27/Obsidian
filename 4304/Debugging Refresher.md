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