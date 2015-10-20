# Template Literals

Template literals can help to build string values we may want to assign to a variable, among other uses.

Old school string concatenation becomes tedious:
```JavaScript
let category = "music";
let id = 2112;

let url = "http://apiserver/" + category + "/" + id;
```

In ES6, there are some differences:
* The string is delimited with backticks (` `` `)
* Inside of the backticks, you can have literal text and substitution placeholders via `${placeholder}`

```JavaScript
let category = "music";
let id = 2112;

let url= `http://apiserver/${category}/${id}`;
```

#### A more interesting example:
```JavaScript
let upper = function(strings, ...values){
  let result = "";
  for (var i = 0; i < strings.length; i++){
    result += strings[i];
    
    if (i < values.length){
      result += values[i];
    }

  }

  return result.toUpperCase();
};

var x = 1;
var y = 3;
var result = upper `${x} + ${y} is ${x + y}`; // Gives us "1 + 3 IS 4"
```

You can associate a tag with a template. In this case, the tag `upper` is a function that is invoked. 

The first parameter being passed into the `upper()` function is known as a parsed template string. These are the pieces of literal text in the template, chopped into an array such that the substitutions are removed. The second parameter is a rest parameter (also an array) using the values of the substitutions. 

```JavaScript
strings = ["", " + ", " is ", ""];
values = [1, 3, 4]
```

&nbsp;

This shows us that there are lots of possibilities in terms of tags that take a template and encode it, tags for localization, and more.
