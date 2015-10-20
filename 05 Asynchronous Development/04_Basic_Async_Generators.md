# Basic Asynchronous Generators

We can use generators to make our async code more readable.

Say we want to log 3 strings to the console, and between each log we want to pause for half a second.

**Without Generators**
```JavaScript
function oldPause(delay, cb) {
  setTimeout(function() {
    console.log('paused for ' + delay + 'ms');
    cb();
  }, delay);
}

console.log('start');
oldPause(500, function() {
  console.log('middle');
  oldPause(500, function() {
    console.log('end');
  });
});

```

**With Generators**
```JavaScript

// IIFE to create variables without polluting the global namespace
(function() {
  var sequence;

  var run = function(generator) {
    sequence = generator();
    var next = sequence.next();
  }

  // Notify that the pause function has completed
  var resume = function() {
    sequence.next();
  }

  // Put it all inside an object that can be accessed anywhere
  window.async = {
    run: run,
    resume: resume
  }
}());

function pause(delay) {
  setTimeout(function() {
    console.log('paused for ' + delay + 'ms');
    async.resume();
  }, delay);
}

function* main() {
  console.log('start');
  yield pause(500);
  console.log('middle');
  yield pause(500);
  console.log('end');
}

async.run(main);

```
