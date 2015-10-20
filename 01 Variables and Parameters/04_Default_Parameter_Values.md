# Default Parameter Values

In JS, the old way of handling a missing or falsey parameter:
```JavaScript
var doSomething = function(name){
  name = name | "Taylor";
  return name;
};
```

The new way in ES6 is like so:
```JavaScript
var doSomething = function(name="Taylor"){
  return name;
};
```

**Note: The default parameter syntax has some different behavior with different calling parameters.**

```JavaScript
let result = doSomething(); // "Taylor"
let result = doSomething(""); // Undefined
let result = doSomething(undefined); // "Taylor"
let result = doSomething("Colleen"); // "Colleen"
let result = doSomething(null); // null
```

&nbsp;

#### Combining Concepts:
```JavaScript
let doSomething = function(a = 1, b = 2, c = 3){
    return [a, b, c];
};

let [a,b,c] = doSomething(5, undefined); // a = 5, b = 2, c = 3
```

Example with destructuring:
```JavaScript
let doSomething = function(url, {data = "Taylor", cache = true}){
  return data;
};

let result = doSomething("api/test", { cache: false }); // "Taylor" is returned (and `cache` is `false` inside the function)


