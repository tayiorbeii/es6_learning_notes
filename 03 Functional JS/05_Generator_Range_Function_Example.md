# Range Function Example

```JavaScript
let range = function*(start, end) {
  let current = start;
  while(current <= end) {
    let delta = yield current;
    current += delta || 1;
  }
}


// This is not a generator function, but returns an object that can be used as an iterator::
let range2 = function(start, end) {
  let current = start;
  let first = true;
  return {
    next(delta = 1) {
      let result = { value: undefined, done: true };
      
      if(!first) {
        current += delta;
      }
      
      if(current <= end) {
        result.value = current;
        result.done = false;
      }
      first = false;
      return result;
    }
  }
}

let result = [];
let iterator = range(1, 10);
let next = iterator.next();
while(!next.done) {
  result.push(next.value);
  next = iterator.next(2);
}

result; // [1, 3, 5, 7, 9]
```


