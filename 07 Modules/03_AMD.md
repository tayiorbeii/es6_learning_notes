# AMD

While CommonJS focuses on coming up with a standard for running JS outside of a web browser, Asynchronous Module Definition (AMD) takes into account loading scripts asynchronously in a web app, as well as optimizing scripts into fewer and smaller downloads at runtime.

During development of a webapp, we want to use modules in our code and develop them independently.

The popular implementation of AMD is provided by RequireJS. It's a script loader that consists primarily of a define function, that contains a callback to be given to the script loader.

This function needs to return the object you want to be a public member. In this example we only return an Employee, but we could return an object with many attributes to make public. 

This is similar to an IIFE, because our implementation details can be kept private, and we have closure around functions. The primary difference is that an IIFE executes immediately, and AMD executes when the script loader tells it to. 


```JavaScript
// employee.js
define(function() {
  
  var privateDoWork = function() {
    // ...
  }

  var Employee = function(name) {
    // ...
  }

  return Employee;
});
```

In order to use this, define a module with an array of the imports you need to include.

```JavaScript
define(["employee"], function(Employee){
  var e = new Employee("Taylor");
});
```



