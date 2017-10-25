## Chapter 1: What is Scope?
---

### Compiler Theory
3 steps of "compilation" before execution:

1. **Tokenizing/Lexing** - breaking breaking up a string of characters into meaningful (to the language) chunks, called tokens.
2. **Parsing** - taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This tree is called an "AST" (Abstract Syntax Tree).
3. **Code-Generation**  - the process of taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it's targeting, etc.

### Understanding Scope

1. `Engine:` responsible for start-to-finish compilation and execution of our JavaScript program.
2. `Compiler:` one of Engine's friends; handles all the dirty work of parsing and code-generation.
3. `Scope:` another friend of Engine; collects and maintains a look-up list of all the declared identifiers (variables), and enforces a strict set of rules as to how these are accessible to currently executing code.

#### What happens:
##### How compiler works (roughly speaking)

```
var foo = "bar";

function bar() {
	var foo = "baz";
}

function baz(foo) {
	foo = "bam";
	bam = "yay";
}
```
```
var foo = "bar";
```

1. Compiler sees a **variable declaration** for an **identifier** called `foo`.  
2. It registers the `foo` **identifier** in current **scope** which is global **scope**.

```
function bar() {
	var foo = "baz";
}
```

1. Compiler sees a **variable declaration** for an **identifier** called `bar` which is a **function declaration**.
2. It registers the `bar` **identifier** in current **scope** which is global **scope**.
3. Compiler sees a **variable declaration** for an **identifier** called `foo`.
4. It registers the `foo` **identifier** in current **scope** which is local scope of **bar**.

```
function baz(foo) {
	foo = "bam";
	bam = "yay";
}
```

1. Compiler sees a **variable declaration** for an **identifier** called `baz` which is a **function declaration**.
2. It registers the `baz` **identifier** in current **scope** which is global **scope**.
3. Compiler sees a **variable declaration** for an **identifier** called `foo`.
4. It registers the `foo` **identifier** in current **scope** which is local scope of **baz**.

Two distinct actions are taken for a variable assignment: 
1. `Compiler` declares a variable (if not previously declared in the current scope)...
2. ...When executing, `Engine` looks up the variable in `Scope` and assigns to it, if found.

##### LHS and RHS lookups
"who's the target of the assignment (LHS)" and "who's the source of the assignment (RHS)".  
**_RHS_** is when it's not a **_LHS_** (not a declaration).
```
var foo = "bar";
```
1. Scope checks if there is an **LHS reference** for a variable called `foo`.
2. Scope locates the **LHS reference** for `foo` because it was declared above.

```
function bar() {
	var foo = "baz";
}
```
1. Scope checks if there is an **LHS reference** for a variable called `foo` in the "scope" of `bar`.
2. Scope locates the **LHS reference** for `foo` because it was declared above.

```
function baz(foo) {
	foo = "bam";
	bam = "yay";
}
```
1. Scope checks if there is an **LHS reference** for a variable called `foo` in the "scope" of `baz`.
2. Scope locates the **LHS reference** for `foo` because it was declared above.
3. Scope checks if there is an **LHS reference** for a variable called `bam` in the "scope" of `baz`.
4. It creates a **variable declaration** for the **identifier** `bam` in the **global** scope because it wasn't declared before. This is how **variable leak** happens.

### Lexical scope

Variable defined outside the function is automatically defined inside the funciton.

Local variable:

```
(function(){
	var i = 2;
})
```

Global variable (without `var`):
```
(funciton(){
	i = 2;
})
```

To prevent declaring variables without `var` use `"use strict";` before each module.


### Hoisting

A compiler-phase task runs first  (declares all variables).  
Then execution-phase task runs (i.e. assigns values to variables).

#### Functions First  

Function declarations are hoisted first, and then variables.  
Function expressions don't hoist.

#### `let` 
`let` doesn't hoist.