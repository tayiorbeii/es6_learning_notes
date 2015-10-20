# Arrows as Async Callbacks

One problem with callbacks is managing the `this` reference, since it is established by the context. 
To illustrate:
```JavaScript
e1.doWork()

....

doWork() {
  this.name = "Taylor"; // this refers to e1

  ajaxCall("aUrl", function(response) {
    // this does not point to e1
    this.name = response.data;
  });
}
```

However, Arrow functions always capture the `this` value of the context they are in (it lexically binds to `this`). 

```JavaScript
  this.name = "Taylor";

  ajaxCall("aUrl", (response) => {
      this.name = response.data;
    });
```
