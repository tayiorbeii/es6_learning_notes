# New `Array` Changes

ES6 has added several new functions to Array instances.

#### `find`
Find the first member whose value is greater than 8:

```JavaScript
var ary = [1, 5, 10];
var match = ary.find(item => item > 8);
match; // 10
```


#### `findIndex`
Returns the index of the first match:
```JavaScript
var ary = [1, 5, 10];
var match = ary.findIndex(item => item > 3);
match; // 1
```

#### `fill`
The `fill` function will fill the entire array with what you supply:
```JavaScript
var ary = [1, 2, 3, 4, 5];
ary.fill('a');
ary; // ['a', 'a', 'a', 'a', 'a']
```

You can also supply a start and end index to the call:

`ary.fill('a', 2, 3) // would change only index 2 to 'a'`


#### `copyWithin`
Copies portions of existing array on top itself in a different location.

```JavaScript
var ary = [1, 2, 3, 4]; // we want [1, 2, 1, 2]

// First parameter as the target (index 2)
// Second parameter is where you copy from (index 0)
// A third parameter would be the stopping point.
ary.copyWithin(2, 0); // [1, 2, 1, 2]
ary.copyWithin(2, 0, 1); // [1, 2, 1, 4]
ary.copyWithin(2, 0, 2); // [1, 2, 1, 2]

// Can also use negative indexes:
ary.copyWithin(0, -2); // [3, 4, 3, 4]
```

#### `of`
This is a way to create an array:
```JavaScript
var ary = new Array(3); //[, , ]
var ofAry = Array.of(3); // [3]

ary.length; // 3
ofAry.length; // 1
```

#### `from`
Creates an array when given an array-like object.
Example grabbing all `div`s in an HTML document:
```JavaScript
var arrayLike = document.querySelectorAll('div');
// arrayLike.forEach is undefined

var fromArray = Array.from(arrayLike);
```

#### `entries` and `keys`
Returns entries from the entries function
```JavaScript
var a = ['Joe', 'Jim', 'John'];
var entries = a.entries();

var firstEntry = entries.next().value;
firstEntry[0]; // 0 (the index)
firstEntry[1]; // 'Joe' (the value)

// `keys` are the indexes
var firstKey = keys.next().value;
firstKey; // 0
```

# Array Comprehensions
Create a list based on an original list. This is easier to read than `map`.

```JavaScript
var ary = [for (i of [1, 2, 3]) i]; // [1, 2, 3]

var ary2 = [for (i of [1, 2, 3]) i * i]; // [1, 4, 9]

var ary3 = [for (i of [1, 2, 3]) if (i < 3 ) i]; // [1, 2]

// Cartesian product:
var ary4 = [for (first of ['William', 'John', 'Blake'])
            for (middle of ['Robert', 'Andrew', 'John'])
            if(first != middle) (first + ' ' + middle + ' Smith')]

ary4; // ["William Robert Smith", "William Andrew Smith" ...]
```





