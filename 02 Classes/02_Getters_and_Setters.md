# Getters and Setters



```JavaScript
class Employee {
  
  get name() {
    return this._name.toUpperCase;
  }

  set name(newValue) {
    this._name = newValue;
  }
}
let e1 = new Employee("Taylor");
let e1 = new Employee("Charles");

e1.name; // "Taylor"
e2.name; // "Charles"

e1.name = "Chris"; // sets e1's name to "Chris"
```

Using `get` in this manner, we are now able to use the cleaner call `e1.name`.

You don't have to supply a setter if you don't want the object's properties to be changed.

It is also possible for the constructor to call the setter:
```JavaScript
constructor(name) {
  this.name = name;  
}

set name(newValue) {
  this._name = newValue;
}
```
