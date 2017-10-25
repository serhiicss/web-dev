## Functions
---
```
function foo() {
	...
}
```

`foo` is basically just a **variable** in the outer enclosing scope that's given a **reference** to the function being declared. That is, the function itself is a **value**, just like 42 or [1,2,3] would be.

>**The main difference between a function expression and a function statement is the function name, which can be omitted in function expressions to create anonymous functions.**  
Function expression results in  a value.

If "function" is the very first thing in the statement, then it's a function declaration. Otherwise, it's a function expression.  
`function foo(){..}` - **Function declaration**.  Identifier `foo` is global.  
`(function foo(){..})();` - **Function expression**. Identifier `foo` is local (bound to itself).  
`(function(){..})();` - **Anonymous function expression**. Identifier `foo` is local (bound to itself).  
`var foo = function(){..}` - **Anonymous function expression**. Identifier `foo` is global.   
`var foo = function bar(){..}` - **Function expression**. Identifier `foo` is global. Identifier `bar` is local (bound to itself).

**Syntax**
```
function name([param,[, param,[..., param]]]) {
   [statements]
}
```

**Crate a function**

```
function addNumbers(a, b) {
    return a + b;
}
```
**or**

```
function addNumbers(a, b) {
    var total =  a + b;
    return total;
}
```

**or**

```
var addNumbers = function(a, b) {
    var total =  a + b;
    return total;
}
```

### Higher order functions
---

```
var people = [
  { name: 'David', job: 'surgeon' },
  { name: 'Sarah', job: 'driver' },
  { name: 'Mark', job: 'surgeon' },
  { name: 'Sam', job: 'broker' },
  { name: 'Natali', job: 'surgeon' },
  { name: 'Anna', job: 'clerk' }
]

var surgeons = people.filter(function(person) {
    return person.job === 'surgeon'
});
```
**or**

```
var isSurgeon = function(person) {
  return person.job === 'surgeon'
}

var surgeons = people.filter(isSurgeon)
```

### Immediately Invoked Function Expressions (IIFEs)
---
```
(function IIFE(){
	console.log( "Hello!" );
})();
// "Hello!"
```
The outer `( .. )` that surrounds the `(function IIFE(){ .. })` function expression is just a nuance of JS grammar needed to prevent it from being treated as a normal function declaration.

The final `()` on the end of the expression -- the `})();` line -- is what actually executes the function expression referenced immediately before it.

### let vs var
`var` is a function scope  
`let`is its own block scope  
So if using `le`t within a function, it will not be in function scope, but only in its own.