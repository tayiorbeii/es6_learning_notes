# Object.is()

The `is` function is similar to `===` but has some added features.

Call `Object.is()` and pass in two parameters. If they are the same, then `true` will be returned.
In almost every case, it works the same as `===` but there are some differences:
* Comparing `0` to `-0` with `===` returns `true`, but `false` with `Object.is()`
* `NaN === NaN` returns `false`. `Object.is(NaN, NaN)` returns `true`

&nbsp;

# Object.assign()

The `Object.assign()` allows you to take properties from one object and copy it onto another object. This is similar to `extend` in jQuery and Underscore.

In other languages, this functionality is described as "mixins". 

Example:
```JavaScript
var shark = {
  bite: function(target) {
    target.hurt = true;
  }
}

var person = {}

var laser = {
  pewpew: function(target) {
    target.exploded = true;
  }
}

Object.assign(shark, laser); // Multiple mixins would be added as parameters

shark.pewpew(person);
person.exploded; // true

```

Note that there isn't any type of forwarding going on-- the `shark` object has its own `pewpew()` function. 
