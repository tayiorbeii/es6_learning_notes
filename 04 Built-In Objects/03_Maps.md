# Maps
Maps are collections of key-value pairs.

```JavaScript
var map = new Map();

map.set("age", 35);
map.size; // 1
map.get("age"); // 35


var ageMap = new Map();
var ralph = {'name': 'Ralph'};
ageMap.set(ralph, 29);
ageMap.get(ralph); // 29


vap map = new Map([['name', 'John'], ['age', 15], ['weight', 155]]);
map.size; // 3
map.has('age'); // true

// Maps do not allow duplicate keys:
var map = new Map();
var key = {};
map.set(key, 'first');
map.set(key, 'second');
map.get(key); // 'second'
```

Maps have `clear` and `delete` like Sets.

Iterate Maps:
```JavaScript
vap map = new Map([['name', 'John'], ['age', 15], ['weight', 155]]);
var iterationCount = 0;

map.forEach(function(value, key) {
  iterationCount++;
  // use value & key
});

// Now with `for of`
for(var [key, value] of map) {
  // the key and the value are their own variables
  iterationCount++;
}
```


Maps return an iterator of arrays of key-value pairs when `entries` is called:
```JavaScript
  var map = new Map();
  map.set('name', 'Joe');
  var items = map.entries();
  var first = items.next().value;
  first[0]; // 'name'
  first[1]; // 'Joe'
```

An iterator of values is returned when calling `values`, and iterator of keys when calling `keys`:
```JavaScript
 var map = new Map();
 map.set(1, 'a');
 var values = map.values();
 var first = values.next().value;
 first; // 'a'

 var keys = map.keys();
 var firstKey = keys.next().value;
 firstKey; // 1 
```

Maps can be constructed with an iterator.
