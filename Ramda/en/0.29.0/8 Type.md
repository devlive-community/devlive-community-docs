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

### isNil

---

`* → Boolean`

Parameters

*   xThe value to test.

> Returns Boolean `true` if `x` is `undefined` or `null`, otherwise `false`.

Added in v0.9.0

Checks if the input value is `null` or `undefined`.

```js
R.isNil(null); //=> true
R.isNil(undefined); //=> true
R.isNil(0); //=> false
R.isNil([]); //=> false
```

### propIs

---

`Type → String → Object → Boolean`

Parameters

*   type
*   name
*   obj

> Returns Boolean

Added in v0.16.0

Returns `true` if the specified object property is of the given type; `false` otherwise.

See also [is](#is), [propSatisfies](#propSatisfies).

```js
R.propIs(Number, 'x', {x: 1, y: 2});  //=> true
R.propIs(Number, 'x', {x: 'foo'});    //=> false
R.propIs(Number, 'x', {});            //=> false
```

### isNotNil

---

`* → Boolean`

Parameters

*   xThe value to test.

> Returns Boolean `true` if `x` is not `undefined` or not `null`, otherwise `false`.

Added in v0.29.0

Checks if the input value is not `null` and not `undefined`.

```js
R.isNotNil(null); //=> false
R.isNotNil(undefined); //=> false
R.isNotNil(0); //=> true
R.isNotNil([]); //=> true
```

