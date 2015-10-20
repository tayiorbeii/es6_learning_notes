# WeakMap & WeakSet
In a normal Map and Set, pointers to objects are strong. If the object being pointed to is deleted, the Map/Set retains its pointer so the object can't be garbage collected. This is a problem for DOM nodes for example.

Because the garbage collector can happen at any time (and thus could remove items from a `WeakSet` at any time), all the functionality that deals with sets as a whole has been removed from the `WeakSet`.

For example, there is no `size` property, `forEach`, etc.

Other than that, they function the same: `has`, `delete`, `clear`, etc. 

`WeakMap`s are like `WeakSet`s, but we can do `has`, `get`, `delete`, `clear`, etc.

Since you can't check if a `WeakMap` or `WeakSet` are empty, you can just check if a specific member is gone.


