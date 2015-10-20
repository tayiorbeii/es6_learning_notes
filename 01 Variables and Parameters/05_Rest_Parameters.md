# Rest Parameters
Rest parameters are how you deal with an unknown number of params with a function. 

The old way was to use the implicit `arugments` object that holds are the args passed into a function: 
```JavaScript
let sum = function() {
  let result = 0;
  for (let i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
};

let result = sum(1, 2, 3) // 6
```

One of the problems though is that `arguments` looks like an array, but it really isn't (it's an object that has some of the qualities of an array). 

The new way in ES6 gives us a better syntax to achieve the same result:
```JavaScript
let sum = function(...numbers) {
  let result = 0;
  for (let i = 0; i < numbers.length; i++){
    result += numbers[i];
  }
  return result;
};
```

&nbsp;

The *rest parameter* is always the last parameter, and features the `...` prefix.

This version of `sum()` has a parameter named `numbers`, and incoming values passed in are packaged into a true array for the function to use.

Another example:
```JavaScript
let doSomething = function(name, ...numbers){
  let result = 0;
  numbers.forEach(function(n){
      result += n;
    });
  return result;
};

let result = doSomething("Taylor", 1, 2, 3); // 6
```

If you don't pass any numbers in, then the function is fed an empty array, and `result` is returned as 0 like we specified.


