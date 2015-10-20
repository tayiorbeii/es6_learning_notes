# Destructuring

Destructuring allows you to assign values to a set of variables.

```JavaScript
let x = 2;
let y = 3;

[x, y] = [y, x]; // x is now 3, and y is now 2
```
What we see on the right side of the destructuring assignment in the above example is an array built from the values that are in `y` and `x`. 
However, on the left side, it is **not** an array, but rather the individual variables `x` and `y` surrounded by square brackets (`[]`) because we are destructuring an array. 

In other words, in the above example we are taking the value of the variable in the first index of the array `[y, x]` (in this case '`y = 3`') and assigning it to `x`, and taking the value of the variable in the second index of the array [`y, x`] (in this case `x = 2`) and assigning it to `y`. Thus, our variables have switched values.

Variable assignment can also be done from a function that returns an array:
```JavaScript
var doSomething = function() {
  return [3, 2];
}

let [x, y] = doSomething(); // x = 3, y = 2
```

If there was an additional member of the array, but you still wanted `x` to be 3 and `y` to be 2, a `,` can be added to skip the value the destructuring assignment:
```JavaScript
var doSomething = function() {
  return [1, 3, 2];
}

let [, x, y] = doSomething(); // x = 3, y = 2
```

&nbsp;

###### Object Destructuring

In this example, we create variables `first`, `last`, and `twitter` and assign them to the return values of the `doSomething` function.

```JavaScript
let doSomething = function() {
  return {
    firstName: "Charles",
    lastName: "Bronson",
    twitter: "@NoDice"
  };
}
  let { firstName: first,
        lastName: last,
        twitter: twitter } = doSomething();
```
*It looks like we're creating an object literal, but we're not.*

Think of the left hand side as being how you navigate into an object:

```JavaScript
let doSomething = function() {
  return {
    firstName: "Charles",
    lastName: "Bronson",
    handles: {
        twitter: "@NoDice",
        facebook: "bronson69"
      }
    };
}
  let { firstName: first,
        lastName: last,
        handles:{twitter: twitter} } = doSomething();
```

If you are cool with having your variable names be the same as the properties, you can use the shorthand:

```JavaScript
let { firstName, lastName, handles:{twitter} } = doSomething();
```

&nbsp;

###### Destructuring in a function
The old way when working with a function:


```JavaScript
  let doSomething = function(url, config){
    return config.data; // "test"
  };

  var config = { data: "test", cache: false }

  let result = doSomething("api/test", config);
```

New way:
```JavaScript
  let doSomething = function(url, {data, cache}){
    return data; // `test` comes directly from the `data` property
  };

  let result = doSomething(
        "api/test", {
          data: "test",
          cache: false
        }
      );

```



