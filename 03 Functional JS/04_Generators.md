# Generators

A generator is a function that generates an iterator. It uses `function*()` and the `yield` keyword:

```JavaScript
let numbers = function*() {
  yield 1;
  yield 2;
  yield 3;
  yield 4;
};
```

`yield` returns multiple values (instead of `return`ing just one). You can `yield` multiple values because the generator is a factory for iterators:

```JavaScript
let sum = 0;
let iterator = numbers();
let next = iterator.next();
while(!next.done){
  sum += next.value;
  next = iterator.next();
}

sum; // 10
```

Each time a generator uses `yield`, it yields the thread of execution back to the caller. The value is returned immediately, the caller can do whatever it needs to do, and then when the caller asks for the next value, the generator picks up where it left off. 

#### Using a `for of` with a Generator

```JavaScript
let numbers = function*(start, end) {
  for(let i = start; i <= end; i++) {
    console.log(i);
    yield i;
  }
};

let sum = 0;

for(let n of numbers(1,5)){
  sum += n;
  console.log("next");
}

sum; // 15
```

# Replacing the iterator we built in the Company example

We will create a filter generator function to look for employees with a "T" in their name:

```JavaScript
class Company {
  constructor() {
    this.employees = [];
  }

  addEmployees(...names) {
    this.employees = this.employees.concat(names);
  }

  *[Symbol.iterator]() {
    for(let e of this.employees) {
      console.log(e);
      yield e;
    }
  }
}

let filter = function*(items, predicate) {
  for(let item of items) {
    console.log("filter", item);

    // Only process items that match the filter
    if(predicate(item)) {
      yield item;
    }
  }
}

// Function that only matches a set number without iterating the entire collection
// (e.g. we only want 'x employees out of everyone')
let take = function*(items, number) {
  let count = 0;
  if(number < 1) return; // Inside a generator, hitting a `return` sets the `done` flag to `true`

  for(let item of items) {
    console.log("take", item);
    yield item;
    count += 1;
    if(count >= number) {
      return;
    }
  }
}

let count = 0;
let company = new Company();
company.addEmployees("Tim", "Sue", "Joy", "Tom");

// Pass the filter function our company and an arrow function
// to look for names that start with T
for(let employee of filter(company, e => e[0] == 'T')) {
  count += 1;
}

count; // 2 (Tim and Tom are the only employees starting with T)

// "take" only one employee whose name starts with T
for(let employee of take(filter(company, e => e[0] == 'T'), 1)) {
  count += 1;
}

```


