# Iterables and Iterators

If you have a collection of objects that is iterable, you can call an iterator. For example, an array has a `next()` function. The iterator holds the value and a boolean `done`.

You have to use the iterator to get the items in the iterable. There is no length attribute of an iterator. 

Let's look at different ways to sum up all the numbers in an array.

```JavaScript
let sum = 0;
let numbers = [1, 2, 3, 4];

// for loop
sum = 0;
for(let i = 0; i < numbers.length; i++){
  sum += numbers[i];
}
sum; // 10

// "for in"
sum = 0;
for(let i in numbers){
  sum += numbers[i];
}

// iterator
sum = 0;
let iterator = numbers.values(); // returns an iterator, not an array
let next = iterator.next();
while(!next.done){
  sum += next.value;
  next = iterator.next();
}

but there's a new way...

# for of
Sometimes we only want to iterate values and not worry about indexes or keys:
```JavaScript
let numbers = [1, 2, 3, 4];

for(let i of numbers) {
  console.log(i);
}
```

This type of loop works with iterators:
```JavaScript

let sum = 0;
let numbers = [1, 2, 3, 4];

for(let n of numbers){
  sum += n;
}
```

"for of" gets to an iterator's value without having to use .values() like above because it implements `Symbol.iterator`.

# Implementing `Symbol.iterator`

The "hard way":
```JavaScript
class Company {
  constructor() {
    this.employees = [];
  }

  addEmployees(...names) {
    this.employees = this.employees.concat(names);
  }
  
  [Symbol.iterator]() {
    return {
      next() {
        ... // This is the hard way
      }
    }
  }

  let count = 0;
  let company = new Company();
  company.addEmployees("Tim", "Sue", "Joy", "Tom");

  for(let employee of company) {
    count += 1;
  }
}
```

It is better to implement the iterator with a class (but still not the easiest way!):
```JavaScript
class Company {

  constructor() {
    this.employees = [];
  }

  addEmployees(...names) {
    this.employees = this.employees.concat(names);
  }

  [Symbol.iterator]() {
    return new ArrayIterator(this.employees);
  }
}

class ArrayIterator {
  constructor(array) {
    this.array = array;
    this.index = 0;
  }

  next() {
    var result = { value: undefined, done: true };

    if(this.index < this.array.length) {
      result.value = this.array[this.index];
      result.done = false;
      this.index += 1;
    }
    return result;
  }
}
```

What's good about implementing an iterator like this is that it allows users to go through our employees without giving them access to the underlying data structure. 

However, the better way to implement an iterator is by using a **Generator**.

