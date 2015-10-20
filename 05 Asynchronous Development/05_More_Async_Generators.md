# More Async Generators

Imagine we are writing a program that will conduct stock trades. 

```JavaScript
// IIFE to create variables without polluting the global namespace
(function() {
  var sequence;

  var run = function(generator) {
    sequence = generator();
    var next = sequence.next();
  }

  // Notify that the pause function has completed
  // Any caller to
  var resume = function(value) {
    sequence.next(value);
  }

  // Put it all inside an object that can be accessed anywhere
  window.async = {
    run: run,
    resume: resume
  }
}());

function getStockPrice() {
  // $.get('/prices', function(prices) {
  //   mimic jQuery's get request
  // }); 

  setTimeout(function() {
    async.resume(50);
  }, 300);
}

function executeTrade() {
  setTimeout(function() {
    console.log('trade completed');
    async.resume();
  }, 300);
}

function* main() {
  // when this function calls sequence.next, 
  // we're going to pass in the result of the yield statement 
  // which will be the price variable.
  var price = yield getStockPrice(); 
  
  if(price > 45) {
    yield executeTrade();
  } else {
    console.log('trade not made');
  }
}

async.run(main);
```


