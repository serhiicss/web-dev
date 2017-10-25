## JavaScript Objects

`[keys]` must be strings. Object key is automatically coerced to string

### Object structure

```
var foo = {
    a: 1,
    b: 2
}
```
`foo` is an object  
`a` and `b` are keys  
`1`, `2`, are values  
`a: 1` and `b: 2` are properties 

### Accessing objects

create:  
`var myObj = new Object();`  
`var myObj = {};`  
`var myObj = {firstname: "Tony", lastname: "Stark"};` 

get:  
`object.name` - dot notation  
`object[expression]` - bracket notation

set:  
`object.name = value`  
`objecet.[expression] = value`

delete:  
`delete object.name`
`delete object[expression]`

#### Examples:

`var person = new Object();` - create new object  
`person.firstname = "John";` - create a **property** with **key** `firstname` and *value* `"John"`  
`person.lastname = "Doe";`    
`person.age = 40;`    
`person.height = 180;`

```
var person = {
  "firstname": "John",
  "lastname": "Doe",
  "age": 40,
  "height": 180
}
```


#### Objects within objects

`person.address = new Object();` - creating a new `object`  
`person.address.street = "100 Main st";` - adding the new object to the existing object of `person`  
`person.address.city = "New York";`  
`person.address.state = "NY";`  
`person.address.zip = 123;`
```
var person = {
  "firstname": "John",
  "lastname": "Doe",
  "age": 40,
  "height": 180,
  "address":
    "street": "100 Main st",
    "city": "New York",
    "state": "NY",
    "zip": 123"
}
```

### By value vs by reference
---

#### By value
Primitive values (string, number or boolean) sit in a certain location of memory.  
`var a;` once declared has its own memory container.  
If we asign `b` to `a` like this `b = a`, then `b` will have its own memory container with a copy of the `a` value.  
For example:
```
var a = 3; // has a memory container with value 3  
b = a; // b has its own memory container with value 3
```
so if we change `a = 4;` then `b` will still be `3` because it is referenced by value.

```
var a = 3;
b = a;
a = 4;

console.log(a);
console.log(b);

4
3
```

#### By reference
Objects (and functions) share the same memory location.  
`var c = {name: 'Natalie'};` has its own memory location.  
`var d;`  
`d = c;` now `d` points to the same memory location as `c`. Therefore `d` references to the value of object `c`.  

```
var c = {name: 'Natalie'};
var d;
d = c;

console.log(c);
console.log(d);

{name: "Natalie"}
{name: "Natalie"}

```
Now, if we mutate `c` like this `c.name = 'Adam'`, then `d` will now point to the same memory location. Therefore it will reference valut of `c` still which is now `Adam`.
```
var c = {name: 'Natalie'};
var d;
d = c;

c.name = 'Adam';

console.log(c);
console.log(d);

{name: "Adam"}
{name: "Adam"}
```
Now, if we asign another value to object `d`, then the reference is still to the same location in memory, but the value is new and is asigned to other objects with same reference like `c`. Samething happens if we pass objects as parameters.
```
var c = {name: 'Natalie'};
var d;
d = c;

d.name = 'Monica';

console.log(c);
console.log(d);

{name: "Monica"}
{name: "Monica"}
```
#### Exception
Creating a new object `c = {name: 'Vera'};` will create a new memory container. `d` however, will still point to the original memory container.
```
var c = {name: 'Natalie'};
var d;
d = c;

c = {name: 'Vera'};

console.log(c);
console.log(d);

Vera
Natalie 
```