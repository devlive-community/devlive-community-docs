[TOC]

### _.clone(value, [isDeep], [customizer], [thisArg])

Creates a clone of `value`. If `isDeep` is `true` nested objects are cloned,
otherwise they are assigned by reference. If `customizer` is provided it's
invoked to produce the cloned values. If `customizer` returns `undefined`
cloning is handled by the method instead. The `customizer` is bound to
`thisArg` and invoked with up to three argument; (value [, index|key, object]).
<br>
<br>
**Note:** This method is loosely based on the
[structured clone algorithm](http://www.w3.org/TR/html5/infrastructure.html#internal-structured-cloning-algorithm).
The enumerable properties of `arguments` objects and objects created by
constructors other than `Object` are cloned to plain `Object` objects. An
empty object is returned for uncloneable values such as functions, DOM nodes,
Maps, Sets, and WeakMaps.

#### Arguments
1. `value` *(&#42;)*: The value to clone.
2. `[isDeep]` *(boolean)*: Specify a deep clone.
3. `[customizer]` *(Function)*: The function to customize cloning values.
4. `[thisArg]` *(&#42;)*: The `this` binding of `customizer`.

#### Returns
*(&#42;)*:  Returns the cloned value.

#### Example
```js
var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

var shallow = _.clone(users);
shallow[0] === users[0];
// => true

var deep = _.clone(users, true);
deep[0] === users[0];
// => false

// using a customizer callback
var el = _.clone(document.body, function(value) {
  if (_.isElement(value)) {
    return value.cloneNode(false);
  }
});

el === document.body
// => false
el.nodeName
// => BODY
el.childNodes.length;
// => 0
```

### _.cloneDeep(value, [customizer], [thisArg])

Creates a deep clone of `value`. If `customizer` is provided it's invoked
to produce the cloned values. If `customizer` returns `undefined` cloning
is handled by the method instead. The `customizer` is bound to `thisArg`
and invoked with up to three argument; (value [, index|key, object]).
<br>
<br>
**Note:** This method is loosely based on the
[structured clone algorithm](http://www.w3.org/TR/html5/infrastructure.html#internal-structured-cloning-algorithm).
The enumerable properties of `arguments` objects and objects created by
constructors other than `Object` are cloned to plain `Object` objects. An
empty object is returned for uncloneable values such as functions, DOM nodes,
Maps, Sets, and WeakMaps.

#### Arguments
1. `value` *(&#42;)*: The value to deep clone.
2. `[customizer]` *(Function)*: The function to customize cloning values.
3. `[thisArg]` *(&#42;)*: The `this` binding of `customizer`.

#### Returns
*(&#42;)*:  Returns the deep cloned value.

#### Example
```js
var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

var deep = _.cloneDeep(users);
deep[0] === users[0];
// => false

// using a customizer callback
var el = _.cloneDeep(document.body, function(value) {
  if (_.isElement(value)) {
    return value.cloneNode(true);
  }
});

el === document.body
// => false
el.nodeName
// => BODY
el.childNodes.length;
// => 20
```

### _.gt(value, other)

Checks if `value` is greater than `other`.

#### Arguments
1. `value` *(&#42;)*: The value to compare.
2. `other` *(&#42;)*: The other value to compare.

#### Returns
*(boolean)*:  Returns `true` if `value` is greater than `other`, else `false`.

#### Example
```js
_.gt(3, 1);
// => true

_.gt(3, 3);
// => false

_.gt(1, 3);
// => false
```

### _.gte(value, other)

Checks if `value` is greater than or equal to `other`.

#### Arguments
1. `value` *(&#42;)*: The value to compare.
2. `other` *(&#42;)*: The other value to compare.

#### Returns
*(boolean)*:  Returns `true` if `value` is greater than or equal to `other`, else `false`.

#### Example
```js
_.gte(3, 1);
// => true

_.gte(3, 3);
// => true

_.gte(1, 3);
// => false
```

### _.isArguments(value)

Checks if `value` is classified as an `arguments` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isArguments(function() { return arguments; }());
// => true

_.isArguments([1, 2, 3]);
// => false
```

### _.isArray(value)

Checks if `value` is classified as an `Array` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isArray([1, 2, 3]);
// => true

_.isArray(function() { return arguments; }());
// => false
```

### _.isBoolean(value)

Checks if `value` is classified as a boolean primitive or object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isBoolean(false);
// => true

_.isBoolean(null);
// => false
```

### _.isDate(value)

Checks if `value` is classified as a `Date` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isDate(new Date);
// => true

_.isDate('Mon April 23 2012');
// => false
```

### _.isElement(value)

Checks if `value` is a DOM element.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is a DOM element, else `false`.

#### Example
```js
_.isElement(document.body);
// => true

_.isElement('<body>');
// => false
```

### _.isEmpty(value)

Checks if `value` is empty. A value is considered empty unless it's an
`arguments` object, array, string, or jQuery-like collection with a length
greater than `0` or an object with own enumerable properties.

#### Arguments
1. `value` *(Array|Object|string)*: The value to inspect.

#### Returns
*(boolean)*:  Returns `true` if `value` is empty, else `false`.

#### Example
```js
_.isEmpty(null);
// => true

_.isEmpty(true);
// => true

_.isEmpty(1);
// => true

_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({ 'a': 1 });
// => false
```

### _.isEqual(value, other, [customizer], [thisArg])

Performs a deep comparison between two values to determine if they are
equivalent. If `customizer` is provided it's invoked to compare values.
If `customizer` returns `undefined` comparisons are handled by the method
instead. The `customizer` is bound to `thisArg` and invoked with up to
three arguments: (value, other [, index|key]).
<br>
<br>
**Note:** This method supports comparing arrays, booleans, `Date` objects,
numbers, `Object` objects, regexes, and strings. Objects are compared by
their own, not inherited, enumerable properties. Functions and DOM nodes
are **not** supported. Provide a customizer function to extend support
for comparing other values.

#### Aliases
*_.eq*

#### Arguments
1. `value` *(&#42;)*: The value to compare.
2. `other` *(&#42;)*: The other value to compare.
3. `[customizer]` *(Function)*: The function to customize value comparisons.
4. `[thisArg]` *(&#42;)*: The `this` binding of `customizer`.

#### Returns
*(boolean)*:  Returns `true` if the values are equivalent, else `false`.

#### Example
```js
var object = { 'user': 'fred' };
var other = { 'user': 'fred' };

object == other;
// => false

_.isEqual(object, other);
// => true

// using a customizer callback
var array = ['hello', 'goodbye'];
var other = ['hi', 'goodbye'];

_.isEqual(array, other, function(value, other) {
  if (_.every([value, other], RegExp.prototype.test, /^h(?:i|ello)$/)) {
    return true;
  }
});
// => true
```

### _.isError(value)

Checks if `value` is an `Error`, `EvalError`, `RangeError`, `ReferenceError`,
`SyntaxError`, `TypeError`, or `URIError` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is an error object, else `false`.

#### Example
```js
_.isError(new Error);
// => true

_.isError(Error);
// => false
```

### _.isFinite(value)

Checks if `value` is a finite primitive number.
<br>
<br>
**Note:** This method is based on [`Number.isFinite`](http://ecma-international.org/ecma-262/6.0/#sec-number.isfinite).

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is a finite number, else `false`.

#### Example
```js
_.isFinite(10);
// => true

_.isFinite('10');
// => false

_.isFinite(true);
// => false

_.isFinite(Object(10));
// => false

_.isFinite(Infinity);
// => false
```

### _.isFunction(value)

Checks if `value` is classified as a `Function` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isFunction(_);
// => true

_.isFunction(/abc/);
// => false
```

### _.isMatch(object, source, [customizer], [thisArg])

Performs a deep comparison between `object` and `source` to determine if
`object` contains equivalent property values. If `customizer` is provided
it's invoked to compare values. If `customizer` returns `undefined`
comparisons are handled by the method instead. The `customizer` is bound
to `thisArg` and invoked with three arguments: (value, other, index|key).
<br>
<br>
**Note:** This method supports comparing properties of arrays, booleans,
`Date` objects, numbers, `Object` objects, regexes, and strings. Functions
and DOM nodes are **not** supported. Provide a customizer function to extend
support for comparing other values.

#### Arguments
1. `object` *(Object)*: The object to inspect.
2. `source` *(Object)*: The object of property values to match.
3. `[customizer]` *(Function)*: The function to customize value comparisons.
4. `[thisArg]` *(&#42;)*: The `this` binding of `customizer`.

#### Returns
*(boolean)*:  Returns `true` if `object` is a match, else `false`.

#### Example
```js
var object = { 'user': 'fred', 'age': 40 };

_.isMatch(object, { 'age': 40 });
// => true

_.isMatch(object, { 'age': 36 });
// => false

// using a customizer callback
var object = { 'greeting': 'hello' };
var source = { 'greeting': 'hi' };

_.isMatch(object, source, function(value, other) {
  return _.every([value, other], RegExp.prototype.test, /^h(?:i|ello)$/) || undefined;
});
// => true
```

### _.isNaN(value)

Checks if `value` is `NaN`.
<br>
<br>
**Note:** This method is not the same as [`isNaN`](https://es5.github.io/#x15.1.2.4)
which returns `true` for `undefined` and other non-numeric values.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is `NaN`, else `false`.

#### Example
```js
_.isNaN(NaN);
// => true

_.isNaN(new Number(NaN));
// => true

isNaN(undefined);
// => true

_.isNaN(undefined);
// => false
```

### _.isNative(value)

Checks if `value` is a native function.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is a native function, else `false`.

#### Example
```js
_.isNative(Array.prototype.push);
// => true

_.isNative(_);
// => false
```

### _.isNull(value)

Checks if `value` is `null`.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is `null`, else `false`.

#### Example
```js
_.isNull(null);
// => true

_.isNull(void 0);
// => false
```

### _.isNumber(value)

Checks if `value` is classified as a `Number` primitive or object.
<br>
<br>
**Note:** To exclude `Infinity`, `-Infinity`, and `NaN`, which are classified
as numbers, use the `_.isFinite` method.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isNumber(8.4);
// => true

_.isNumber(NaN);
// => true

_.isNumber('8.4');
// => false
```

### _.isObject(value)

Checks if `value` is the [language type](https://es5.github.io/#x8) of `Object`.
(e.g. arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`)

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is an object, else `false`.

#### Example
```js
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(1);
// => false
```

### _.isPlainObject(value)

Checks if `value` is a plain object, that is, an object created by the
`Object` constructor or one with a `[[Prototype]]` of `null`.
<br>
<br>
**Note:** This method assumes objects created by the `Object` constructor
have no inherited enumerable properties.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is a plain object, else `false`.

#### Example
```js
function Foo() {
  this.a = 1;
}

_.isPlainObject(new Foo);
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true

_.isPlainObject(Object.create(null));
// => true
```

### _.isRegExp(value)

Checks if `value` is classified as a `RegExp` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isRegExp(/abc/);
// => true

_.isRegExp('/abc/');
// => false
```

### _.isString(value)

Checks if `value` is classified as a `String` primitive or object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isString('abc');
// => true

_.isString(1);
// => false
```

### _.isTypedArray(value)

Checks if `value` is classified as a typed array.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is correctly classified, else `false`.

#### Example
```js
_.isTypedArray(new Uint8Array);
// => true

_.isTypedArray([]);
// => false
```

### _.isUndefined(value)

Checks if `value` is `undefined`.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is `undefined`, else `false`.

#### Example
```js
_.isUndefined(void 0);
// => true

_.isUndefined(null);
// => false
```

### _.lt(value, other)

Checks if `value` is less than `other`.

#### Arguments
1. `value` *(&#42;)*: The value to compare.
2. `other` *(&#42;)*: The other value to compare.

#### Returns
*(boolean)*:  Returns `true` if `value` is less than `other`, else `false`.

#### Example
```js
_.lt(1, 3);
// => true

_.lt(3, 3);
// => false

_.lt(3, 1);
// => false
```

### _.lte(value, other)

Checks if `value` is less than or equal to `other`.

#### Arguments
1. `value` *(&#42;)*: The value to compare.
2. `other` *(&#42;)*: The other value to compare.

#### Returns
*(boolean)*:  Returns `true` if `value` is less than or equal to `other`, else `false`.

#### Example
```js
_.lte(1, 3);
// => true

_.lte(3, 3);
// => true

_.lte(3, 1);
// => false
```

### _.toArray(value)

Converts `value` to an array.

#### Arguments
1. `value` *(&#42;)*: The value to convert.

#### Returns
*(Array)*:  Returns the converted array.

#### Example
```js
(function() {
  return _.toArray(arguments).slice(1);
}(1, 2, 3));
// => [2, 3]
```

### _.toPlainObject(value)

Converts `value` to a plain object flattening inherited enumerable
properties of `value` to own properties of the plain object.

#### Arguments
1. `value` *(&#42;)*: The value to convert.

#### Returns
*(Object)*:  Returns the converted plain object.

#### Example
```js
function Foo() {
  this.b = 2;
}

Foo.prototype.c = 3;

_.assign({ 'a': 1 }, new Foo);
// => { 'a': 1, 'b': 2 }

_.assign({ 'a': 1 }, _.toPlainObject(new Foo));
// => { 'a': 1, 'b': 2, 'c': 3 }
```
