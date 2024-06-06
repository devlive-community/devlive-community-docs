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
