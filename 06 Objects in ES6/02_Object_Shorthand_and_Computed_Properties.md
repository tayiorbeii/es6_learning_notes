# Property Initializer Shorthand

Example:
```JavaScript
var model = 'Ford';
var year = 1969;

// Old way
var Classic = {
  model: model,
  year: year // { model: 'Ford', year: 1969 }
}

// ES6 way
var Classic = {
  model, year // {model: 'Ford', year: 1969 }
}
```

# Method Initializer Shorthand

Create methods on objects using a shorthand.

```JavaScript
var server = {
  
  // Old way
  getPort: function() {
    // stuff
  }

  // ES6 way
  getPort() {
    //stuff
  }
}
```

# Computed Property Names

```JavaScript
// Old way
function createSimpleObject(propName, propVal) {
  var obj = {};
  obj[propName] = propVal;
  return obj;
}

// New way
function createSimpleObject(propName, propVal) {
  return {
    [propName]: propVal
  }
}
```

Being able to use expressions like this for property name also allows us to do string concatenation:
```JavaScript
function createTriumvirate(first, second, third) {
  return {
    ['member_' + first.name]: first,
    ['member_' + second.name]: second,
    ['member_' + third.name]: third
  }
}

var Joe = {name: 'Joe'}
var Ralph = {name: 'Ralph'}
var Harry = {name: 'Harry'}

var tri = createTriumvirate(Joe, Ralph, Hary)

tri.member_Joe; // Joe (the person object)

```

