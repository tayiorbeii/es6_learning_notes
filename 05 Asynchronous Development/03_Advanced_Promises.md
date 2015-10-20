# Advanced Promises

Chaining promises to make multiple async calls sequentially:
```JavaScript
function getOrder(orderId) {
  return Promise.resolve({userId: 35});
}

function getUser(userId) {
  return Promise.resolve({companyId: 18});
}

function getCompany(companyId) {
  return Promise.resolve({name: 'Pluralsight'})
}


getOrder(3).then(function(order) {
  return getUser(order.userId);
}).then(function(user) {
  return getCompany(user.companyId);
}).then(function(company) {
  company.name; // 'Pluralsight'
}).catch(function(error) {
  // handle error
});
```

#### Execute after all promises have been returned
```JavaScript
function getCourse(courseId) {
  var courses {
    1: {name: 'Intro to Cobol'},
    2: {name: 'Another class'},
    3: {name: 'Class 3'}
  }

  return Promise.resolve(courses[courseId]);
}


var courseIds [1, 2, 3];
var promises = [];

for(var i = 0; i < courseIds.length; i++){
  promises.push(getCourse(courseIds[i]));
}

// 
Promise.all(promises).then(function(values) { 
  values.length; // 3
})
```

#### How to make a promise resolve after the very first of a set of promises resolves:
If you have several async processes going on and you want something to happen after the first one resolves, then you would use the `race` function.
```JavaScript

var courseIds [1, 2, 3];
var promises = [];

for(var i = 0; i < courseIds.length; i++){
  promises.push(getCourse(courseIds[i]));
}

Promise.race(promises).then(function(firstValue) {
  firstValue.name; // should be defined, but we don't know what order the promises resolve in.
})

```
