## The pieces of a programming language
- five different things
	- syntax: how do you write language constructs?
	- semantics: what do programs mean? (evaluation rules)
	- idioms: What are the typical patterns for using language features to express your computation
	- libraries: what facilities does the language provide standard
	- tools: what do language implementations provide to make your job easier
- The focus on this course is on semantics and idioms==
## Ways to build new types
- Already know that there are various base types line int bool unit char
- ways to build nested compound types: tuples, lists, options
- First: 3 most important type building-blocks in any language
	- "each of": A t value contains values of each of t1,t2...tn
	- "one of": A t value contains valyes of one of t1,t2...tn
	- "self reference": A t valye can reer to other t values
- Remarkable a lot of data can be described with just these building blocks
## Records
- ![[Pasted image 20250903231900.png]]
## Tuples as syntactic sugar
-  tuples are nothing more than records with specific field names
- they are syntactic sugar for records with fields names 1,2, ... n
- Syntactic: can describe the semantics entirely by the corresponding record syntax
## Datatype bindings
- ![[Pasted image 20250907105430.png]]
-  ![[Pasted image 20250907105558.png]]
- ![[Pasted image 20250907105716.png]]
- ![[Pasted image 20250907105726.png]]
## Case Expressions
- ![[Pasted image 20250907105854.png]]
- ![[Pasted image 20250907105917.png]]
- ![[Pasted image 20250907111218.png]]
- ![[Pasted image 20250907111254.png]]
## useful datatypes
- ![[Pasted image 20250907135114.png]]
- ![[Pasted image 20250907135221.png]]
- ![[Pasted image 20250907135310.png]]
- ![[Pasted image 20250907135331.png]]
- ![[Pasted image 20250907135502.png]]
## Precise pattern matching so far
- ![[Pasted image 20250907140119.png]]
- ![[Pasted image 20250907140130.png]]
## Type Synonyms
- ![[Pasted image 20250907140304.png]]
- ![[Pasted image 20250907140356.png]]
- 