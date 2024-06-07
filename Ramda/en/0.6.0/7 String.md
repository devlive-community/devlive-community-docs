[TOC]

### match

-------------------------------------------------------------------------------------------------------------

`RegExp → String → [String | Undefined]`

Parameters

*   rxA regular expression.
*   strThe string to match against

> Returns Array The list of matches or empty array.

Added in v0.1.0

Tests a regular expression against a String. Note that this function will return an empty array when there are no matches. This differs from [`String.prototype.match`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match) which returns `null` when there are no matches.

See also [test](#test).

```js
R.match(/([a-z]a)/g, 'bananas'); //=> ['ba', 'na', 'na']
R.match(/a/, 'b'); //=> []
R.match(/a/, null); //=> TypeError: null does not have a method named "match"
```

### split

---

`(String | RegExp) → String → [String]`

Parameters

*   sepThe pattern.
*   strThe string to separate into an array.

> Returns Array The array of strings from `str` separated by `sep`.

Added in v0.1.0

Splits a string into an array of strings based on the given separator.

See also [join](#join).

```js
const pathComponents = R.split('/');
R.tail(pathComponents('/usr/local/bin/node')); //=> ['usr', 'local', 'bin', 'node']

R.split('.', 'a.b.c.xyz.d'); //=> ['a', 'b', 'c', 'xyz', 'd']
```

### trim

---

`String → String`

Parameters

*   strThe string to trim.

> Returns String Trimmed version of `str`.

Added in v0.6.0

Removes (strips) whitespace from both ends of the string.

```js
R.trim('   xyz  '); //=> 'xyz'
R.map(R.trim, R.split(',', 'x, y, z')); //=> ['x', 'y', 'z']
```
