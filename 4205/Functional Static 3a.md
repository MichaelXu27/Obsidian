## Functional Programming
![[Pasted image 20250914114042.png]]
![[Pasted image 20250914114254.png]]
![[Pasted image 20250914114323.png]]
![[Pasted image 20250914114340.png]]
![[Pasted image 20250914114404.png]]

## Funcs as arguments
![[Pasted image 20250914114537.png]]
![[Pasted image 20250914114614.png]]
- second function is (2^n * x)
![[Pasted image 20250914114819.png]]
![[Pasted image 20250914114900.png]]
## Functions and types

![[Pasted image 20250914115024.png]]
![[Pasted image 20250914115105.png]]
![[Pasted image 20250914115239.png]]
- if we didnt have polymorphism then we would need to write multiple versions of that function
![[Pasted image 20250914115404.png]]

## Anonymous Functions
![[Pasted image 20250914115523.png]]
![[Pasted image 20250914115534.png]]
- this one above is better
![[Pasted image 20250914115620.png]]

![[Pasted image 20250914115709.png]]
- this above is the anonymous function
![[Pasted image 20250914115814.png]]
![[Pasted image 20250914115826.png]]

## Unnecessary Function binding
![[Pasted image 20250914120236.png]]
- bottom one is better
## Map and filter
![[Pasted image 20250914120537.png]]
![[Pasted image 20250914120743.png]]
![[Pasted image 20250914120802.png]]
## Generalizing past topics
![[Pasted image 20250914120900.png]]
 ![[Pasted image 20250914121409.png]]
 ![[Pasted image 20250914121416.png]]
 ##  1. **Functions as Arguments**

- Functions can be passed to other functions, enabling abstraction and reuse.
    
- For example, instead of writing separate functions for each transformation, you can pass a transformation function directly into a higher-order function (like `map`).
    

---

### 2. **Functions and Types**

- A highlighted function example is `(2^n * x)`, showing how mathematical expressions naturally translate into function definitions.
    
- The notes suggest being mindful of type signatures, since they define what kinds of inputs and outputs are allowed.
    

---

### 3. **Anonymous Functions (Lambdas)**

- Anonymous functions remove the need to explicitly bind a function to a name when it’s only used once.
    
- Without polymorphism, we’d have to rewrite the same logic for different types; anonymous functions help streamline this.
    
- The “above is better” comment refers to using lambdas for conciseness.
    

---

### 4. **Unnecessary Function Binding**

- Instead of defining a helper function just to pass it once, we can directly insert the anonymous function into `map` or `filter`.
    
- Example:
    
    `map (\x -> x*2) [1,2,3]   -- better than defining a separate “double” function`
    

---

### 5. **Map and Filter**

- These higher-order functions embody the essence of functional programming:
    
    - **Map** applies a function to every element in a list.
        
    - **Filter** selects elements that satisfy a condition.
        
- Both are cleaner and more general than manual recursion.
    

---

### 6. **Generalizing Past Topics**

- The notes stress abstraction—finding patterns that recur and lifting them into reusable functions.
    
- Instead of writing code for every special case, you generalize the logic (often with higher-order functions, polymorphism, or type abstractions).
    

---

✅ **Synthesis:**  
The document is a progression from basic functional programming (passing functions, writing pure functions) toward higher levels of abstraction. The theme is _simplicity through generalization_: prefer anonymous functions over unnecessary bindings, use polymorphism instead of rewriting code, and rely on higher-order functions like `map` and `filter` to make code expressive and reusable.