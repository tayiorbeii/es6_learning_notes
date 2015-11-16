# Classes

In the old way of writing classes, a constructor function and a prototype object that all instances would inherit from had to be created.

This looked something like this:
```JavaScript
var Employee = function() {

};

Employee.prototype = {
  doSomething: function(){
    return "done!";
  }  
};

var e = new Employee();
```

This syntax sucks. The new ES6 syntax to do the same thing is like this:
```JavaScript
class Employee {
  doSomething() {
    return "complete!";  
  }

  doSomethingElse() {
    return "also complete!"  
  }
}

var e = new Employee();
e.doSomething(); // "complete!"
```

This doesn't require the use of the `function` keyword. Behind the scenes, the same thing is happening. Commas aren't required between method definitions, and semicolons are optional.

Currently we only have hardcoded strings in our objects, so let's introduce state and constructor functions.

#### The Constructor
Managing state consistently requires some initialization logic for an object, that is implemented with a constructor. The constructor function is automatically invoked when you say `new <classname>`, and inside the constructor you can use the implicit `this` reference to manipulate the object and store instance state.

```JavaScript
class Employee {
  constructor(name) {
    this._name = name;
  }

  doSomething() {
    return "complete!";
  }

  getName() {
    return this._name;
  }
}

let e1 = new Employee("Taylor");
let e2 = new Employee("Charles");

e1.getName(); // "Taylor"
e2.getName(); // "Charles"
```
