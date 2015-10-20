# Inheritance

The 3 Pillars of Object Oriented Programming:
1. Encapsulation
2. Polymorphism
3. Inheritance

In ES6, it is easy to specify an inheritance relationship. 

```JavaScript
class Person {
  constructor(name) {
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(newValue) {
    this._name = newValue;
  }
}
```

Say we want to create an employee, and each employee "is-a" person. The `extends` keyword handles our inheritance.

```JavaScript
.
.
.
class Employee extends Person {
  doWork() {
    return `${this._name} is working`; // uses ES6's literal syntax
  }
}

let p1 = new Person("Taylor");
let e1 = new Employee("Chris");
e1.doWork(); // "Chris is working"
```

Often there will be additional pieces of information that will need to be stored in an object. For example, our Employees should have a title...

# super

`super` allows you to forward a call from a child class's constructor to the superclass's constructor and forward along the required parameters.

```JavaScript
class Employee extends Person {
  constructor(name, title){
    super(name);
    this._title = title;
  }  

  get title() {
    return this._title;  
  }
}
```
You could use `this._name = name;` in the derived class constructor, but this isn't the appropriate approach, since there could be validation logic, etc.

`super` can also be called in other ways. For example, If a `Person` does work, they do it for free. If they are an `Employee`, they are paid:

```JavaScript
class Person {
  
  constructor(name) {
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(newValue) {
    if(newValue) {
      this._name = newValue;
    }
  }

  doWork() {
    return "free";
  }
}


class Employee extends Person {
  
  constructor(title, name) {
    super(name);
    this._title = title;
  }

  get title() {
    return this._title;
  }

  doWork() {
    return "paid";  
  }
}

let e1 = new Employee("Taylor", "Developer");
let p1 = new Person("Charles");

p1.doWork(); // "free"
e1.doWork(); // "paid"
```

We have overwritten the `doWork()` method. We can also overwrite the `toString()` method:

```JavaScript
class Person {
  .
  .
  .
  toString() {
    return this.name;
  }
}
```

We can cycle through an array of people to see if they're working:
```JavaScript
let makeEveryoneWork = function(...people) {
  var results = [];
  for (var i = 0; i < people.length; i++){
    results.push(people[i].doWork());
  };
  return results;
}

makeEveryoneWork(p1, e1); // ["free", "paid"]
```
Note that the `makeEveryoneWork` function doesn't care if someone is a person or an employee, because both have a `doWork` method. To adjust to code to have a check that the object passed in has a `doWork` function, use:
```JavaScript
if(people[i].doWork) { ... }
```
or 

```JavaScript
if(people[i] instanceof Person) { ... }
```



