### ML Language:
```sml
(* This is a comment. This is our first program. *)
val x = 34;
val y = 17;

```

**Syntax** is how your write something
**Semantics** is what that something you wrote in the syntax mean
* Type checking
* Evaluation

In **Standard ML (SML)**, a **binding** is when you give a _name_ to a _value, function, or type_

For variable bindings
* type check expression and extend static environment
* Evaluate expression and extend dynamic environment
Every exception has
1. Syntax
2. Type checking rules
	1. produces a type or fails
	2. types so far: int bool unit
3. evaluation rules
	1. produces a value (or excpetion or infinite loop)

### Variables
Syntax: sequence of letters, digits, _ , not starting with digit
Type-checking: look up type in currecnt static environment, it not there fail
Evaluation: look up value in current dynamic environment

### Addition
Syntax: e1 + e2 where e1 and e2 are expressions
Type checking: if e1 and e2 have type int hen e1+e2 have type int
Evaluation: if e1 evaluates to v1 and e2 evaluated to v2, then e1 + e2 evaluates to the sum of v1 and v2

### Values:
* all values are expressions
* Not all expressions are values
* every value evaluates to itself in zero steps
* examples 
	* 34,17,42 have type int
	* true false have type bool*
	* () has type unit
### Conditionals
Syntax: if e1 then e2 else e3 where if, then, and else are keywords and e1,e2, and e3 are subexpressinos
Type checking: first e1 must have type bool, e2 and e3 can have any type, but they bust have the same type. the type of the entire expression is alos t
Evaluation: first evaluate e1 to a value call it vc1, if it is true evaluate e2 and that result is the whole expressions result else do the same for e3

## REPL and Error messages:
* repl means read eval print loop
* ctrl+c ctrl+s return to bring up the repl
* ctrl+d ends the session
* "use" 

Negative in ML is `~`
 Floating point division is done with `/` but with integers it is `div`
## Shadowing
* multiple variable binding of the same variable is often poor style
* For this reasoning is why professor is so insistent about not reusing use on a file without restarting the REPL
* Otherwise you are introducing some of the same bindings again
	* it may make it seem that wrong code is correct
	* may make it seem like correct code is wrong
	* its all well defined but humans get confused
## Functions
```sml
fun pow(x: int, y: int) = 
	if y = 0
	then 1
	else x * pow(x, y-1)
fun cube(x : int) = 
	pow(x,3)

```

## Tuples and Lists:
* Tuples: fixed "number of pieces" that may have different types
* Lists: any "number of pieces" that all have the same type
#### Building a pair (2-tuples):
* need a way to build pairs and a way to access the pieces
* Build:
	* syntax: (e1, e2)
	* evaulation: evaulate e1 to v1 and e2 to v2; result is (v1,v2)
		* a pair of values is a value
	* Type checking: if e1 has type ta and e2 has type tb, then the pair expression has type ta * tb
		* - a new kind of type
* Access:
	* syntax: #1 e and #2 e
	* Evaluation: evaluate e to a pair of values and return first or second piece
		* example: if e is a variable x, then look up x in environment
	* Type checking: if e has type ta * tb, then #1 e has type ta and #2 e has type tb
## Lists
* Tuples need to commit to a certain particular amount of data
* whereas with a list it can have any number of elements but all list elements need to have the same type
* Build:
	* The empty list is a value []
	* in general a list of values is a value; elements separated by commas
	* if e1 evaluaets to v and e2 evalutates to a list `[v1,..., vn]`,
	* then e1::e2 evaluates to `[v,...,vn]`
* Accessing lists:
	* Below is all functions
	* `null e` evaluates to true if and only if e evaluates to `[]`
	* if `e` evaluates to `[v1,v2,... ,vn] `then `hd e` evaluates to `v1` (head)
	* if `e` evaluates to `[v1,v2,... ,vn] `then `tl` e evaluates to `[v2,...,vn]` (tail), tail is everything after the first element
* Knowing that the empty list is a value:
		* commands like `null` `hd` and `tl` all on their own return `a list` 'alpha list'
## List Functions:
```sml
fun sum_list (xs: int list) = 
	if null xs:
	then 0
	else hd xs + sum_list(tl xs)
	
fun countdown (x : int) = 
	if x=0
	then []
	else x :: countdown(x-1)

fun append (xs: int list, ys: int list) = 
	 if null xs
	 then ys
	 else (hd xs) :: append((tl xs), ys)
	 
fun sum_pair_list (xs : (int * int) list) = 
	if null xs
	then 0
	else #1 (hd xs) + #2 (hd xs) + sum_pair_list(tl xs)
```
 
## Let expressions
- Syntax: let  ... bi... in  e end
	- each bi is any binding and e is any expression
- Type checking: Type check each bi and e in a static environment that includes the previous bindings
- type of whole let-expression is the type of e
- Evaluation: evaluate each bi and e in a dynamic environment that includes previous bindings
- result of whole let-expression is result of evaluating e
```sml
fun silly1(z: int) = 
	let
		val x = if z > 0 then z else 34
		val y = x + z + 9
	in
		if x > y then x * 2 else y * y
	end

fun silly2 () = 
	let
		val x = 1
	in
		(let x = 2 in x + 1 end) + (let val y = x + 2 in y + 1 end)
	end
```

* `(let val y = x + 2 in y + 1 end)` evaluated to 4
* `(let x = 2 in x + 1 end)` evaluated to 3
## Nested Functions:
* functions are bindings
* therefore you can just wrap a function in a let in end statement and then you have some sort of a 'helper function'
## Let efficiency
