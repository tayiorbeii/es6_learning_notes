# Arrow Functions

Arrow functions introduce a concise syntax for defining a function.

Example:
```JavaScript
let add = (x,y) => x + y;
add(3,5); // 8
```

On the left hand side of the arrow (`=>`) are the parameters, and on the right hand side is the function body. There is no need for braces or a return statement.

Example:
```JavaScript
let add = (x,y) => x + y;
let square = x => x * x;

square(add(2,3)); // 25
```

In order to write an arrow function that takes no parameters, you must include empty parenthesis:
```JavaScript
let three = () => 3;
```

If you need multiple lines of code for an arrow function, you must use braces and a return statement (but this isn't really best practice for an arrow function):
```JavaScript
let add = (x,y) => {
  let temp = x + y;
  return temp;
};
```

Arrow functions can be used as parameters to other functions.
Example of adding all numbers in an array:
```JavaScript
var numbers = [1, 2, 3, 4];

var sum = 0;
numbers.forEach(n => sum += n); // 10
```

This code takes each number in the array `numbers`, assigns its value to `n`, then adds it to `sum`.

Example of creating a new array with each value doubled:
```JavaScript
var doubled = numbers.map(n => n * 2);

doubled; //[2, 4, 6, 8]
```

