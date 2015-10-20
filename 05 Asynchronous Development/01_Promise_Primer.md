# Callbacks

The most basic form of async programming in JS is the callback.
The caller spawns an asynchronous operation. When the caller initiates this process, it passes the process to a callback, trusting that when the process finishes, it will invoke the callback.
When the async process finishes, the callback is put onto the call stack, and will execute when all the other processes ahead of it are complete.

There are some problems:
* Only the caller can be notified that the async process has completed.
  * No other interested parties can act, unless the callback informs them.
* Error handling is difficult.
* Handling multiple callback processes at once is hard.
* The callback is responsible for multiple things
  * Processing the async call
  * Starting other processes that want to execute

Callback Example:
```JavaScript
function getCompanyFromOrderId(orderId) {
  getOrder(orderId, function(order) {
    getUser(order.userId, function(user) {
      getCompany(user.companyId, function(company) {
        // do something with company
      });
    });
  });
}
```
In this example, first we get the order, then when that's complete we get the user, then when that's complete we can get the company.

Notice that each callback has to process data by calling the next function, but also pass the appropriate callback into the next function. 

When we add in exception handling, it's even worse:
```JavaScript
function getCompanyFromOrderId(orderId) {
  try {
    getOrder(orderId, function(order) {
      try {
        getUser(order.userId, function(user){
          try {
            getCompany(user.companyId, function(company) {
              try {
                 // do something with company
              } catch(ex) {
                // handle exception
              }
            });
          } catch(ex) {
            // handle exception
          }
        });
      } catch(ex) {
        // handle exception
      }
    });
  } catch(ex) {
    // handle exception
  }
}
```

So what's the solution?

# Promises
Promises are what save us from "Callback Hell". A promise is an object which represents a handle to listen to the results of an async operation, whether it succeeds or fails. The promise "promises" to alert you when the async operation is done, and give you the results of that operation.

Promises are composable, which means you can take two promises that represent two different async operations, and chain them together so one happens after the other, or wait for them both to run and do a new operation when both are complete. You can make other promises that depend on the results of a previous promise, and succeeds when it succeeds, or fails when it fails. 

A promise is made up of two parts:

**The Control of a Promise**
* Also called "the deferred". 
  * May be a separate object, or a callback.
* Gives the creator of the promise the ability to mark the promise as "succeeded" or "failed".

**The Promise itself**
* Object can be passed around
* Enables interested parties to register actions to take when the async operation completes.
  * Flow control no longer responsibility of the handler
* Error handling is much easier

&nbsp;

A promise exists in one of three states:
1. Pending (Not yet completed)
2. Fulfilled (Completed sucessfully)
3. Rejected (Failed)

_Note: the "rejected" state means we are no longer dealing with exception handling. We need to let other functions know that the promise failed so they have to do something._

Same example as the Callback + Error Handling, but with Promises:
```JavaScript
function getCompanyFromOrderId(orderId){
  getOrder(orderId).then(function(order) {
    return getUser(order.userId);
  }).then(function(user) {
    return getCompany(user.companyId);
  }).then(function(company) {
    // do something with company
  }).then(undefined, function(error) {
    // handle error
  })
}
```

