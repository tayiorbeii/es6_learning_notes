# Proxies

Proxies allow us to intercept operations done on objects. The most straightforward operations to intercept are `set` and `get`. 

### Intercepting `get`
```JavaScript
var unicorn = {
  legs: 4,
  color: 'brown',
  horn: true
}

```

When we use a proxy object, we aren't modifying the original object, but are instead creating a new object that is a wrapper around the original object. If you are going to use proxies, you have to access to the original object through the proxy.

Say we want to make it so when someone gets the color of a unicorn, it says "awesome" in front.

```JavaScript
// Create a proxy object by passing the target object and an object literal of the operation you want to intercept.
var proxyUnicorn = new Proxy(unicorn, {
  get: function(target, property) {
    if(property === 'color') {
      return 'awesome ' + target[property];
      } else {
        return target[property];
      }
  }
})
```


### Intercepting `set`
```JavaScript
var unicorn = {
  legs: 4,
  color: 'brown'
  horn: true
}

// Disallow the 'horn' from being set to `false`
var proxyUnicorn = new Proxy(unicorn, {
  set: function(target, property, value) {
    if (property === 'horn' && value === false) {
      console.log('Unicorn will never be hornless!');
    } else {
      target[property] = value;
    }
  }
})
```


In addition to `get` and `set`, you can intercept calls to `delete`, `define`, `freeze`, `in`, `has`, etc. You can intercept multiple calls by adding to the handler:

```JavaScript
set: function (...),
get: function (...)
```
