# Comprehensions

Comprehensions are a terse syntax for building arrays and generators, similar to what's found in Python.

#### Array Comprehension
We know we are building an array from the square brackets.

```JavaScript
var numbers = [for (n of [1, 2, 3]) n * n];
numbers; // [1, 4, 9]
```

This comprehension is the same as:
```JavaScript
let numbers = [];
for(let n of [1, 2, 3]) {
  numbers.push(n * n);
}
numbers; // [1, 4, 9]
```

We can also use a filter predicate to look for numbers greater than 1:
```JavaScript
var numbers = [for (n of [1, 2, 3]) if (n > 1) n * n];
```

Using this syntax, an array will be yielded. In order to yield the members of the array, a `*` is used.
Example:
```JavaScript
yield [for (item of items) item] // is like `yield ["Tim", "Sue", "Joy", "Tom"]`

yield* [for (item of items) item] // is like `yield "Tim"; yield "Sue"; yield "Joy"; yield "Tom"`
```

Array comprehensions are a greedy syntax. In the Company example, we had a filter that would filter the list using a predicate. Rewriting it using an array comprehension:

```JavaScript
let filter = function*(items, predicate) {
  yield* [for (item of items) if(predicate(item)) item];
}
```

The problem with this is that the entire array is iterated before returning just the desired item. In order to stop iterating as soon as we've "taken" what we wanted, use a generator comprehension:


#### Generator Comprehension
Use `()` instead of `[]`
```JavaScript
var numbers = (for (n of [1, 2, 3]) n * n);
```

So to rewrite our filter function to stop iterating when we've got what we wanted (using the `take` function in the Company example):
```JavaScript
yield* (for (item of items) if(predicate(item)) item);
```

Essentially, use the Generator Comprehension when you want to be lazy and do as little work as possible, or use the Array Comprehension when you want to have everything in a data structure from the start.





