# ES6 Modules

There are two reasons we covered CommonJS and AMD. ES6 modules are similar to the other two systems-- we can select things we want to export, and what we want to import into another module. 

Notice the `export` keyword. It is reasonable to have one export per file. 

Example of ES6 Module syntax:
```JavaScript
export class Employee {
  constructor(name) {
    this._name = name;
  }

  get name() {
    return this._name;
  }

  doWork {
    return `${this._name} is working`;
  }
}
```

Importing in another module:
```JavaScript
import {Employee} from './es6/employee';

var e = new Employee("Taylor");
e.doWork();
```

_Note we have a destructured import by using `{Employee}`._


What we have is closer to the CommonJS way of doing things. 
