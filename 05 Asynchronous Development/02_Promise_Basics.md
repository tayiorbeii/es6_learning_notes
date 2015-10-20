# Promise Basics
_Note: This code is originally used in Jasmine tests_

Resolve:
```JavaScript
var promise = new Promise(function(resolve, reject){
  resolve(1);
});

promise.then(function(data) {
  console.log(data); // 1
  done();
});
```

Reject:
```JavaScript
var promise = new Promise(function(resolve, reject){
  reject(Error('I am Error'));
});

promise.then(function() {
  // success
}, function(error) {
  console.log(error.message); // 'I am Error'
});
```

There is a shorthand if all you care about is a failure:
```JavaScript
var promise = new Promise(function(resolve, reject){
  reject(Error('I am Error'));
});

promise.catch(function(error) {
  console.log(error.message); // 'I am Error'
});
```

&nbsp;

#### Resolving a Promise with Another Promise
```JavaScript
var previousPromise = new Promise(function(resolve, reject){
  resolve(3);
});

var promise = new Promise(function(resolve, reject) {
  resolve( previousPromise );
});

promise
  .then( function(data) {
    console.log(data); // 3
  })
```
