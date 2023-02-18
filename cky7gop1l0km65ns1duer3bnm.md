# Temporal Dead Zone, Scope and Hoisting

With ES6, two very important ways to declare a variable were introduced, `let` and `const`. These were introduced to replace `var` which was previous standard way of declaring a variable.


Although by definition `let` and `var` are functionally similar. They are interpreted differently in some ways. 

### Temporal Dead Zone
The area of code before the variable is initialized by `let` or `const` is called Temporal Dead Zone (TDZ)


```
// Temporal Dead Zone
// Temporal Dead Zone
let a = 1;
console.log(a);
``` 

This concept is introduced with `let` and `const` and is not applicable for `var`

If we try to access a variable declared using `let` or `const` before it is initialized returns a Reference Error. This is because of TDZ.

```
console.log(a); // returns "Reference Error" (a is in TDZ)
let a = 1;
```

Where as for `var`, the console returns `undefined`
```
console.log(a); // returns "undefined"
var a = 1;
```

### Scope
There are three types of scopes in JavaScript. Global Scope, Function Scope and Block Scope.
Block Scope is relatively new, and is introduced with ES6, `let` and `const`

**Global Scope** is the scope of the file/program. Once declared in Global Scope, the variable can be accessed anywhere in the file/program. (Ofcourse, exception is TDZ in the case of `let` and `const`)

```
let num = 1;
{
    let n = 2;
    num = n + num;
    console.log(num); // logs 3
}
console.log(num); // logs 3
```

But if `num` is in TDZ...

```
let num = 1;
{
    let n = 2;
    let num = n + num; // throws "Reference Error", because num is not initialized in this Block Scope
    console.log(num); 
}
console.log(num);
```

**Block Scope** is the code between `{ }`
Let's try the above code with `var`

```
var num = 1;
{
    var n = 2;
    var num = n + num;
    console.log(num); // logs 3
}
console.log(num); // logs 3
```

**Function Scope** is the scope inside a function.
```
let num = 1;
function addNum(n) {
    num = n + num;
    return num;
}
console.log(addNum(2)); // logs 3
console.log(num); // logs 3
```
The above code works because `num` is the declared in the Block of file/program.

```
let num = 1;
function addNum(n) {
    let num = n + num; // throws "Reference Error", because num is not yet initialized in the block of function
    return num;
}
console.log(addNum(2)); 
console.log(num); 
```

Let's try the same examples with `var`

```
var num = 1;
function addNum(n) {
    num = n + num; 
    return num;
}
console.log(addNum(2)); // logs 3
console.log(num); // logs 3
```

```
var num = 1;
function addNum(n) {
    var num = n + num; 
    return num;
}
console.log(addNum(2)); // logs NaN
console.log(num); // logs 1
```
The `num` inside the function is being refernced before it's declaration, but since `var` doesn't have TDZ, it is initialized as `undefined` when it is hoisted. So when the function is called `undefined` is added to `2` and returns `NaN`

If you notice, When `num` is declared with `var` inside a function, the `num` outside the function is not used. But when `num` is declared with `var` inside a block, the `num` outside the block is used. This is because `var` is **Functional Scoped**, not **Block Scoped**.

Whereas when `num` declared with `let`, it throwed "Reference Error" when `num` is accessed before initialized, because of TDZ and because `let` is **Block Scoped**

### Hoisting
All the variables and functions in a JavaScript program are hoisted, i.e., a memory location is allocated to the variables and functions according to thier scopes.
Although `let` and `const` are hoiseted, a value is not assigned until a value is assigned to the variable creating TDZ in between.
