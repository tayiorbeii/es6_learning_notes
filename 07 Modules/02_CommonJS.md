# CommonJS Modules

CommonJS revolves primarily around `exports` and `require`.

There is no IIFE required, because the module system will execute the script in a non-global context.

The `exports` object is required to make code publicly available. 

Example of the Module:
```JavaScript
var privateDoWork = function(name) {
  return name + " is working";
}

var Employee = function(name) {
  this.name = name;
}

Employee.prototype = {
  doWork: function() {
    return privateDoWork(this.name);
  }
}

exports.Employee = Employee;

// or if there is more...
// exports.Employee = Employee;
// exports.Another = SomethingElse;
```

Accessing the module:
```JavaScript
var Employee = require('./Employee').Employee;

var e1 = new Employee("Taylor");
console.log(e1.doWork()); // "Taylor is working"
```
