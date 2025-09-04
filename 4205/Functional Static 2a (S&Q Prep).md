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