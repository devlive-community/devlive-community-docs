[TOC]

### and

------------------------------------------------------------------------------------------------------

`a → b → a | b`

Added in v0.1.0

Returns the first argument if it is falsy, otherwise the second argument. Acts as the boolean `and` statement if both inputs are `Boolean`s.

See also [both](#both), [or](#or).

```js
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```

### isEmpty

------------------------------------------------------------------------------------------------------------------

`a → Boolean`

Added in v0.1.0

Returns `true` if the given value is its type's empty value; `false` otherwise.

See also [empty](#empty), [isNotEmpty](#isNotEmpty).

```js
R.isEmpty([1, 2, 3]);           //=> false
R.isEmpty([]);                  //=> true
R.isEmpty('');                  //=> true
R.isEmpty(null);                //=> false
R.isEmpty({});                  //=> true
R.isEmpty({length: 0});         //=> false
R.isEmpty(Uint8Array.from('')); //=> true
```

### not

------------------------------------------------------------------------------------------------------

`* → Boolean`

Parameters

*   aany value

> Returns Boolean the logical inverse of passed argument.

Added in v0.1.0

A function that returns the `!` of its argument. It will return `true` when passed false-y value, and `false` when passed a truth-y one.

See also [complement](#complement).

```js
R.not(true); //=> false
R.not(false); //=> true
R.not(0); //=> true
R.not(1); //=> false
```

### or

---------------------------------------------------------------------------------------------------

`a → b → a | b`

Added in v0.1.0

Returns the first argument if it is truthy, otherwise the second argument. Acts as the boolean `or` statement if both inputs are `Boolean`s.

See also [either](#either), [and](#and).

```js
R.or(true, true); //=> true
R.or(true, false); //=> true
R.or(false, true); //=> true
R.or(false, false); //=> false
```
