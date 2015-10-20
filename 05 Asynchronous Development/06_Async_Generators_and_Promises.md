# Asynchronous Generators and Promises

Let's pair up our async generators with promises.

One of the downsides to the async generators we've been working with is that they must be aware that they're being called from within an async generator, so they have to be able to call `async.resume()` or `async.fail()`.

```JavaScript
(function() {
  var run = function(generator) {
    var sequence;
    var process = function(result) {
      // parameter receives the value that the promise resolves with
      result.value.then(function(value) {
        if(!result.done) {
          process(sequence.next(value))
        }
      }, function(error) {
        if(!result.done) {
          process(sequence.throw(error));
        }
      })
    } 

    sequence = generator();
    var next = sequence.next();
    process(next);
  }


// Because we are going to use promises,
// the promises themselves will be the notifications to `asyncP`
// as to whether they are done or failed.
  window.asyncP = {
    run: run,
  }
}());

function getStockPriceP() {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      resolve(50);
    }, 300);
  });
}

function executeTradeP() {
  return new Promise(function(resolve, reject){
    setTimeout(function() {
      resolve();
    }, 300);
  });
}

function* main() {
  try {
    var price = yield getStockPriceP();
    if(price > 45) {
      yield executeTradeP();
    } else {
      console.log('trade not made');
    }
  } catch(ex) {
    console.log('error! ' + ex.message);
  }
  done();
}

asyncP.run(main);
```
