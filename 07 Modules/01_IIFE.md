# IIFE Module Pattern

Use an immediately invoked function expression (IIFE).

There won't be any global variables defined by this code as long as the `var` keyword is used appropriately.

You can choose to expose pieces publically if you explicitly do so. 

For example, attaching `target.Employee = Employee` to the `window` of the browser. 

It is easy to have private implementation details like the `privateDoWork` function that is only available inside the IIFE's closure.

```JavaScript
(function(target) {
  var privateDoWork = function(name) {
    return name + " is working";
  };

  var Employee = function(name) {
    this.name = name;
  }

  Employee.prototype = {
    doWork: function() {
      return privateDoWork(this.name);
    }
  }

  target.Employee = Employee;
}(window));
```

## Two Goals of a Module:
1. Organize code into related concepts and treat everything as a unit
2. Control visibility and hide implementation details
