# The `let` Keyword

`let` allows us to define variables in a different way than `var`. 

With `var` there are two types of scope: *global* when the variable is defined outside of the function, and *function scope* for variables declared inside of a function. 

**JavaScript has no block scope.** In this example, it seems like `x` would only be available inside of the `if`, but that's not the case:

```javascript
var doesSomething = function(param) {
  
  if(param){
    var x = 5;
  }
  return x;
};
```

`x` is avaible throughout the `doesSomething` function, and the `return` will work because there is going to be a variable named `x`.


**`let` gives us true block scoping:**

```javascript
var doesSomething = function(param) {
  
  if(param){
    let x = 5;
  }
  return x;
};
```
In the above example, there will be an error if no other `x` variables are defined in an outer scope and the `if` block isn't hit.

Here is an example of behavior in a `for` loop:
```javascript
for(var i = 0; i < 10; i++){
    
}
return i; // returns 10

for(let j = 0; j < 10; j++){
  
}
return j; // ReferenceError: j is not defined
```


`let` will be the replacement for `var` because it will let us declare variables where we need them, avoid hoisting, and give us true block scoping like most developers expect.

