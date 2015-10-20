# The `const` Keyword

`const` creates and initializes a read-only variable at a constant value that you can never change.

In ES6, `const` has block scoping:

```javascript
var doSomething = function() {  
  const x = 12;
  var x = 10; //Syntax error: Variable 'x' has already been declared.
}
```

The `x` defined in `doSomething` shadows the outer `x`:
```JavaScript
const x = 12;
var doSomething = function() {
  let x = 10; // Note: would also work with `var`
  return x; // 10
}
```

*Note: it is convention to use ALL CAPS for constants, but the above is for illustrative purposes.*


