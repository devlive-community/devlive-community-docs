[TOC]

### is

---

`(* → {*}) → a → Boolean`

Parameters

*   ctorA constructor
*   valThe value to test

> Returns Boolean

Added in v0.3.0

See if an object (i.e. `val`) is an instance of the supplied constructor. This function will check up the inheritance chain, if any. If `val` was created using `Object.create`, `R.is(Object, val) === true`.

```js
R.is(Object, {}); //=> true
R.is(Number, 1); //=> true
R.is(Object, 1); //=> false
R.is(String, 's'); //=> true
R.is(String, new String('')); //=> true
R.is(Object, new String('')); //=> true
R.is(Object, 's'); //=> false
R.is(Number, {}); //=> false
```

### type

---

`* → String`

Parameters

*   valThe value to test

> Returns String

Added in v0.8.0

Gives a single-word string description of the (native) type of a value, returning such answers as 'Object', 'Number', 'Array', or 'Null'. Does not attempt to distinguish user Object types any further, reporting them all as 'Object'.

```js
R.type({}); //=> "Object"
R.type(1); //=> "Number"
R.type(false); //=> "Boolean"
R.type('s'); //=> "String"
R.type(null); //=> "Null"
R.type([]); //=> "Array"
R.type(/[A-z]/); //=> "RegExp"
R.type(() => {}); //=> "Function"
R.type(async () => {}); //=> "AsyncFunction"
R.type(undefined); //=> "Undefined"
R.type(BigInt(123)); //=> "BigInt"
```

