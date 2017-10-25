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

If an object value is a primitve, it is called a property  
If an object value is a function, it is called a method
```
var myObj = {
  name: 'Alan', // property
  log: function() { // method
    console.log(name);
  }
}
```

#### Accessing objects

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

// 4
// 3
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

// {name: "Natalie"}
// {name: "Natalie"}

```
Now, if we mutate `c` like this `c.name = 'Adam'`, then `d` will now point to the same memory location. Therefore it will reference valut of `c` still which is now `Adam`.
```
var c = {name: 'Natalie'};
var d;
d = c;

c.name = 'Adam';

console.log(c);
console.log(d);

// {name: "Adam"}
// {name: "Adam"}
```
Now, if we asign another value to object `d`, then the reference is still to the same location in memory, but the value is new and is asigned to other objects with same reference like `c`. Samething happens if we pass objects as parameters.
```
var c = {name: 'Natalie'};
var d;
d = c;

d.name = 'Monica';

console.log(c);
console.log(d);

// {name: "Monica"}
// {name: "Monica"}
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

// Vera
// Natalie 
```

### this keyword

`this` keyword value depends on how and where the function is called.  

On global lever, for example, `this` references the global object, which is the `window` object.  
`console.log(this)` = `Window`  

Another example:
```
function a() {
  console.log(this);
}

a(); // Window
```

If `this` key is a method on an object, then it referenced to the object itself.
```
var person = {
  name: 'Monica',
  log: function() {
    console.log(this);
    }
  }

person.log(); // person object
```

#### Exception (bug)

`this` keyword used in a function within a function within an object references to the global scope(Window).   

```
var person = {
  name: 'Monica',
  log: function() {
    console.log(this);
    var setName = function(newName) {
      this.name = newName;
    }
    setName('Oliver');
    console.log(this);
    }
  }

person.log(); // Monica
```
The value of key person hasn't been changed because `this` within a function of a function points to global object, not the `person` object.

#### And here is how to fix this:

We set a variable within the object to `this` on very first line of first function. Then we change all other `this` to `self`. This way all `self` will reference to `this` in the scope of object.

```
var person = {
  name: 'Monica',
  log: function() {
    var self = this;
    console.log(self);
    var setName = function(newName) {
      self.name = newName;
    }
    setName('Oliver');
    console.log(self);
    }
  }

person.log(); // Oliver
```
