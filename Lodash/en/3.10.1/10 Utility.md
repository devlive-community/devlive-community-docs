[TOC]

### _.attempt(func)

Attempts to invoke `func`, returning either the result or the caught error
object. Any additional arguments are provided to `func` when it's invoked.

#### Arguments
1. `func` *(Function)*: The function to attempt.

#### Returns
*(&#42;)*:  Returns the `func` result or error object.

#### Example
```js
// avoid throwing errors for invalid selectors
var elements = _.attempt(function(selector) {
  return document.querySelectorAll(selector);
}, '>_>');

if (_.isError(elements)) {
  elements = [];
}
```

### _.callback([func=_.identity], [thisArg])

Creates a function that invokes `func` with the `this` binding of `thisArg`
and arguments of the created function. If `func` is a property name the
created callback returns the property value for a given element. If `func`
is an object the created callback returns `true` for elements that contain
the equivalent object properties, otherwise it returns `false`.

#### Aliases
*_.iteratee*

#### Arguments
1. `[func=_.identity]` *(&#42;)*: The value to convert to a callback.
2. `[thisArg]` *(&#42;)*: The `this` binding of `func`.

#### Returns
*(Function)*:  Returns the callback.

#### Example
```js
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

// wrap to create custom callback shorthands
_.callback = _.wrap(_.callback, function(callback, func, thisArg) {
  var match = /^(.+?)__([gl]t)(.+)$/.exec(func);
  if (!match) {
    return callback(func, thisArg);
  }
  return function(object) {
    return match[2] == 'gt'
      ? object[match[1]] > match[3]
      : object[match[1]] < match[3];
  };
});

_.filter(users, 'age__gt36');
// => [{ 'user': 'fred', 'age': 40 }]
```

### _.constant(value)

Creates a function that returns `value`.

#### Arguments
1. `value` *(&#42;)*: The value to return from the new function.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var object = { 'user': 'fred' };
var getter = _.constant(object);

getter() === object;
// => true
```

### _.identity(value)

This method returns the first argument provided to it.

#### Arguments
1. `value` *(&#42;)*: Any value.

#### Returns
*(&#42;)*:  Returns `value`.

#### Example
```js
var object = { 'user': 'fred' };

_.identity(object) === object;
// => true
```

### _.matches(source)

Creates a function that performs a deep comparison between a given object
and `source`, returning `true` if the given object has equivalent property
values, else `false`.
<br>
<br>
**Note:** This method supports comparing arrays, booleans, `Date` objects,
numbers, `Object` objects, regexes, and strings. Objects are compared by
their own, not inherited, enumerable properties. For comparing a single
own or inherited property value see `_.matchesProperty`.

#### Arguments
1. `source` *(Object)*: The object of property values to match.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, _.matches({ 'age': 40, 'active': false }));
// => [{ 'user': 'fred', 'age': 40, 'active': false }]
```

### _.matchesProperty(path, srcValue)

Creates a function that compares the property value of `path` on a given
object to `value`.
<br>
<br>
**Note:** This method supports comparing arrays, booleans, `Date` objects,
numbers, `Object` objects, regexes, and strings. Objects are compared by
their own, not inherited, enumerable properties.

#### Arguments
1. `path` *(Array|string)*: The path of the property to get.
2. `srcValue` *(&#42;)*: The value to match.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

_.find(users, _.matchesProperty('user', 'fred'));
// => { 'user': 'fred' }
```

### _.method(path, [args])

Creates a function that invokes the method at `path` on a given object.
Any additional arguments are provided to the invoked method.

#### Arguments
1. `path` *(Array|string)*: The path of the method to invoke.
2. `[args]` *(...&#42;)*: The arguments to invoke the method with.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var objects = [
  { 'a': { 'b': { 'c': _.constant(2) } } },
  { 'a': { 'b': { 'c': _.constant(1) } } }
];

_.map(objects, _.method('a.b.c'));
// => [2, 1]

_.invoke(_.sortBy(objects, _.method(['a', 'b', 'c'])), 'a.b.c');
// => [1, 2]
```

### _.methodOf(object, [args])

The opposite of `_.method`; this method creates a function that invokes
the method at a given path on `object`. Any additional arguments are
provided to the invoked method.

#### Arguments
1. `object` *(Object)*: The object to query.
2. `[args]` *(...&#42;)*: The arguments to invoke the method with.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.methodOf(object));
// => [2, 0]
```

### _.mixin([object=lodash], source, [options])

Adds all own enumerable function properties of a source object to the
destination object. If `object` is a function then methods are added to
its prototype as well.
<br>
<br>
**Note:** Use `_.runInContext` to create a pristine `lodash` function to
avoid conflicts caused by modifying the original.

#### Arguments
1. `[object=lodash]` *(Function|Object)*: The destination object.
2. `source` *(Object)*: The object of functions to add.
3. `[options]` *(Object)*: The options object.
4. `[options.chain=true]` *(boolean)*: Specify whether the functions added are chainable.

#### Returns
*(Function|Object)*:  Returns `object`.

#### Example
```js
function vowels(string) {
  return _.filter(string, function(v) {
    return /[aeiou]/i.test(v);
  });
}

_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']

_('fred').vowels().value();
// => ['e']

_.mixin({ 'vowels': vowels }, { 'chain': false });
_('fred').vowels();
// => ['e']
```

### _.noConflict()`
<a href="#_noconflict">#</a> [&#x24C8;](https://github.com/lodash/lodash/blob/3.10.1/lodash.src.js#L11583 "View in source") [&#x24C9;][1] [&#x24C3;](https://www.npmjs.com/package/lodash.noconflict "See the npm package")

Reverts the `_` variable to its previous value and returns a reference to
the `lodash` function.

#### Returns
*(Function)*:  Returns the `lodash` function.

#### Example
```js
var lodash = _.noConflict();
```

### _.noop()

A no-operation function that returns `undefined` regardless of the
arguments it receives.

#### Example
```js
var object = { 'user': 'fred' };

_.noop(object) === undefined;
// => true
```

### _.property(path)

Creates a function that returns the property value at `path` on a
given object.

#### Arguments
1. `path` *(Array|string)*: The path of the property to get.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var objects = [
  { 'a': { 'b': { 'c': 2 } } },
  { 'a': { 'b': { 'c': 1 } } }
];

_.map(objects, _.property('a.b.c'));
// => [2, 1]

_.pluck(_.sortBy(objects, _.property(['a', 'b', 'c'])), 'a.b.c');
// => [1, 2]
```

### _.propertyOf(object)

The opposite of `_.property`; this method creates a function that returns
the property value at a given path on `object`.

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };

_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]

_.map([['a', '2'], ['c', '0']], _.propertyOf(object));
// => [2, 0]
```

### _.range([start=0], end, [step=1])

Creates an array of numbers (positive and/or negative) progressing from
`start` up to, but not including, `end`. If `end` is not specified it's
set to `start` with `start` then set to `0`. If `end` is less than `start`
a zero-length range is created unless a negative `step` is specified.

#### Arguments
1. `[start=0]` *(number)*: The start of the range.
2. `end` *(number)*: The end of the range.
3. `[step=1]` *(number)*: The value to increment or decrement by.

#### Returns
*(Array)*:  Returns the new array of numbers.

#### Example
```js
_.range(4);
// => [0, 1, 2, 3]

_.range(1, 5);
// => [1, 2, 3, 4]

_.range(0, 20, 5);
// => [0, 5, 10, 15]

_.range(0, -4, -1);
// => [0, -1, -2, -3]

_.range(1, 4, 0);
// => [1, 1, 1]

_.range(0);
// => []
```

### _.runInContext([context=root])

Create a new pristine `lodash` function using the given `context` object.

#### Arguments
1. `[context=root]` *(Object)*: The context object.

#### Returns
*(Function)*:  Returns a new `lodash` function.

#### Example
```js
_.mixin({ 'foo': _.constant('foo') });

var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });

_.isFunction(_.foo);
// => true
_.isFunction(_.bar);
// => false

lodash.isFunction(lodash.foo);
// => false
lodash.isFunction(lodash.bar);
// => true

// using `context` to mock `Date#getTime` use in `_.now`
var mock = _.runInContext({
  'Date': function() {
    return { 'getTime': getTimeMock };
  }
});

// or creating a suped-up `defer` in Node.js
var defer = _.runInContext({ 'setTimeout': setImmediate }).defer;
```

### _.times(n, [iteratee=_.identity], [thisArg])

Invokes the iteratee function `n` times, returning an array of the results
of each invocation. The `iteratee` is bound to `thisArg` and invoked with
one argument; (index).

#### Arguments
1. `n` *(number)*: The number of times to invoke `iteratee`.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array)*:  Returns the array of results.

#### Example
```js
var diceRolls = _.times(3, _.partial(_.random, 1, 6, false));
// => [3, 6, 4]

_.times(3, function(n) {
  mage.castSpell(n);
});
// => invokes `mage.castSpell(n)` three times with `n` of `0`, `1`, and `2`

_.times(3, function(n) {
  this.cast(n);
}, mage);
// => also invokes `mage.castSpell(n)` three times
```

### _.uniqueId([prefix])

Generates a unique ID. If `prefix` is provided the ID is appended to it.

#### Arguments
1. `[prefix]` *(string)*: The value to prefix the ID with.

#### Returns
*(string)*:  Returns the unique ID.

#### Example
```js
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```
