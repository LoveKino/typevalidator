## Typevalidator

Type checking is normal, we usually do type checking like this: 
```js
function isArray(v){
 return v && typeof v === "object" && typeof v.length === "number";
}

// check type : array or falsy
isArray(type) || !type; 
```

Typevalidator has did those basic works for us.

```
typevalidator.validate("array | falsy", type);
```

## Install

`npm install typevalidator`

## Uasge

- import library

```
var Typevalidator = require("typevalidator");
var typevalidator = Typevalidator();
```

- validate API: typevalidator.validate( expression )

Expresssion is a logic expression which composed by "&", "|" and "~".

```
typevalidator.validate("(~object && ~array) | number", value);
```

- keywords in expression

There are some keywords like number, object, array, etc. Those defined in system. You can define your own keywords also.

You can see system inner keywords below:

```js
// basic
["string", "object", "undefined", "boolean", "function", "number", "symbol"]

// common
"null": v => v === null,
"array": v => v && typeof v === "object" && typeof v.length === "number",
"valueObj": v => v && typeof v === "object",
"pureObj": v => v && typeof v === "object" && typeof v.length !== "number",
"falsy": v => !v,
"truthy": v => v,
"regExp": v => v instanceof RegExp,
"any": v => true
```

You can use those keywords directly.

```
string, object, undefined, boolean, function, number, symbol,
null, array, valueObj, pureObj, falsy, truthy, regExp, any
```

- define keywords yourself

Change the line `var typevalidator = Typevalidator()` to this:

```
var typevalidator = Typevalidator({
    "myType1": function(v){ return v>10; },
    "myType2": function(v){ return v>10; }
});
```

`myType1` and `myType2` are your own keywords, you can use it directly.

- check API: typevalidator.check( expression )

Instead of returning true or false, this function throw exception directly if the value of expression is false.

- batch API

```
typeChecker.checkBatch(["string", "function"], [type, handler]);
typeChecker.validateBatch(["string", "function"], [type, handler]);
```

## License

MIT


