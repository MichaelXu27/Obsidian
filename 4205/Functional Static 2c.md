# Exceptions:
- ![[Pasted image 20250910175012.png]]
- if head is empty it will raise an exception.
- ![[Pasted image 20250910175145.png]]
- Exception is passed in here, passing in doesnt cause an exception to be raised.
- hadnling an exception
- ![[Pasted image 20250910175224.png]]
- if e1 has exception then the handle called.
- if no handle the program stops
- ![[Pasted image 20250910175327.png]]
- ![[Pasted image 20250910175348.png]]
- when you declare an exception it is of type exn, its a normal type, not normal but its useful.
## Tail Recursion
- ![[Pasted image 20250910175554.png]]
- New programming idioms
- Call Stacks:![[Pasted image 20250910175652.png]]
- Stack frame!![[Pasted image 20250910175846.png]]
- ![[Pasted image 20250910180028.png]]
- Looking back on this case, this is what is happening
- ![[Pasted image 20250910181418.png]]
- ![[Pasted image 20250910181246.png]]
## Accumulators
- ![[Pasted image 20250910181616.png]]
- This is not a tail recursive function![[Pasted image 20250910181716.png]]
- the bottom example is an example use of accumulator, and that one is tail recursive
- ![[Pasted image 20250910181749.png]]
- ![[Pasted image 20250910181907.png]]
## Tail recursion perspective

- ![[Pasted image 20250910182251.png]]
- ![[Pasted image 20250910182305.png]]
- ![[Pasted image 20250910182434.png]]