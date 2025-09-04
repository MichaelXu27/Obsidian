## Options

- having max return 0 for the empty list is poor
	- could raise an exception
	- could return a zero element or one element list
		- that works but it is poor style because the build in support for options expresses this situation directly
- t option is a type for any type t
- Building:
	- NONE has type 'a option' (much like [] has type a list)
	- SOME e has type t option if e has type t (much like e::[])
- Accessing:
	- isSome has type 'a option' -> bool
	- valOf has type 'a option' -> (exception if given NONE)

## Boolean Operations
- `e1 andalso e2`
- Type checking: e1 and e2 must have type bool
- Evaluation: if result of e1 is false then false else result of e2
- `e1 orelse e2` == }}
- `not e1` == ~

#### Comparisons
- for comparing int values:
- =, <>, >, <, >=, <=
- you might see weird error messages because comparators can be used with some other types too
- >, <, >=, <= can be used with real, but not 1 int and 1 real
- = <> can be used with any equality type but not with real 


## No mutation:
- In ML theres no mutation (immutable)
- so once you create a list/tuple or some data structure theres no way to change the data in that created data structure 
- If language allows you to mutate then you have to know what is an alias of what etc.