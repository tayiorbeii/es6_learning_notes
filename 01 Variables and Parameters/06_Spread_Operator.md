# Spread Operator

The spread operator uses the same `...` syntax as the rest parameter. However, when used outside a function parameter list, the `...` means we want to spread an array across individual parameters.

In this example, 1 goes to `x`, 2 goes to `y`, and `3` goes to z:
```JavaScript
let doSomething = function(x, y, z) {
  return x + y + z;
}

var result = doSomething(...[1, 2, 3]); // gives us 6
```

&nbsp;

#### Building Arrays with the Spread Operator
```JavaScript
var a = [4, 5, 6];
var b = [1, 2, 3, ...a, 7, 8, 9]; //b is now [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Spreading makes data we already have in arrays easier to work with.

