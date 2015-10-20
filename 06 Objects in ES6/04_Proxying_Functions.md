# Proxying Functions

```JavaScript
var unicorn = {
  legs: 4,
  color: 'brown',
  horn: true
  hornAttack: function(target) {
    return target.name + ' was obliterated!';
  }
}

// The thief can steal methods from others and use them as his own
var thief = { name: 'Rupert' }
thief.attack = unicorn.hornAttack;
thief.attack(); // the hornAttack method belongs to the thief now.
```

To prevent method theft, we would create a proxy around the `hornAttack` function to intercept its invocation:

```JavaScript
var unicorn = {
  legs: 4,
  color: 'brown',
  horn: true
  hornAttack: function(target) {
    return target.name + ' was obliterated!';
  }
}

unicorn.hornAttack = new Proxy(unicorn.hornAttack) {
  apply: function(target, context, args) {
    if(context !== unicorn) {
      return "Only unicorn can use hornAttack";
    } else {
      return target.apply(context, args);
    }
  }
}

var thief = { name: 'Rupert' }
thief.attack = unicorn.hornAttack;
thief.attack(); // "Only unicorn can use hornAttack"
unicorn.attack(thief); // "Rupert was obliterated!"
```

