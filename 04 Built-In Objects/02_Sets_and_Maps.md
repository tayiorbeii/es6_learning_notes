# Set
Sets are a new ES6 object that are unique lists.

```JavaScript
var set = new Set();

set.size; // 0

set.add("somevalue");
set.size; // 1
```

Sets convert everything using the `toString`. Sets can be initialized with an Array:
```JavaScript
var set = new Set([1, 2, 3]);
set.has(1); //true
```

`set.clear();` will empty the set.

`set.delete(item);` will delete the item:

```JavaScript
var set = new Set();
set.add(1);
set.add(2);
set.delete(1);
set.size; // 1
```

Sets can be iterated with a `forEach`, and will be iterated in insertion order. However, if order is really important, use an Array. `for of` can also be used:
```JavaScript
var set = new Set();
set.add(['Tom']);
set.add(['Dick']);
set.add(['Harry']);

var iterCount = 0;
set.forEach(item => iterationCount++);
iterationCount; // 3

var set = new Set([1, 2, 3]);
for (var item of set) {
  iterationCount++;
}
iterationCount; // 3
```


