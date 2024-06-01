[TOC]

### _(value)

Creates a `lodash` object which wraps the given value to enable intuitive
method chaining.
<br>
<br>
In addition to Lo-Dash methods, wrappers also have the following `Array` methods:<br>
`concat`, `join`, `pop`, `push`, `reverse`, `shift`, `slice`, `sort`, `splice`,
and `unshift`
<br>
<br>
Chaining is supported in custom builds as long as the `value` method is
implicitly or explicitly included in the build.
<br>
<br>
The chainable wrapper functions are:<br>
`after`, `assign`, `bind`, `bindAll`, `bindKey`, `chain`, `compact`,
`compose`, `concat`, `countBy`, `create`, `createCallback`, `curry`,
`debounce`, `defaults`, `defer`, `delay`, `difference`, `filter`, `flatten`,
`forEach`, `forEachRight`, `forIn`, `forInRight`, `forOwn`, `forOwnRight`,
`functions`, `groupBy`, `indexBy`, `initial`, `intersection`, `invert`,
`invoke`, `keys`, `map`, `max`, `memoize`, `merge`, `min`, `object`, `omit`,
`once`, `pairs`, `partial`, `partialRight`, `pick`, `pluck`, `pull`, `push`,
`range`, `reject`, `remove`, `rest`, `reverse`, `shuffle`, `slice`, `sort`,
`sortBy`, `splice`, `tap`, `throttle`, `times`, `toArray`, `transform`,
`union`, `uniq`, `unshift`, `unzip`, `values`, `where`, `without`, `wrap`,
and `zip`
<br>
<br>
The non-chainable wrapper functions are:<br>
`clone`, `cloneDeep`, `contains`, `escape`, `every`, `find`, `findIndex`,
`findKey`, `findLast`, `findLastIndex`, `findLastKey`, `has`, `identity`,
`indexOf`, `isArguments`, `isArray`, `isBoolean`, `isDate`, `isElement`,
`isEmpty`, `isEqual`, `isFinite`, `isFunction`, `isNaN`, `isNull`, `isNumber`,
`isObject`, `isPlainObject`, `isRegExp`, `isString`, `isUndefined`, `join`,
`lastIndexOf`, `mixin`, `noConflict`, `parseInt`, `pop`, `random`, `reduce`,
`reduceRight`, `result`, `shift`, `size`, `some`, `sortedIndex`, `runInContext`,
`template`, `unescape`, `uniqueId`, and `value`
<br>
<br>
The wrapper functions `first` and `last` return wrapped values when `n` is
provided, otherwise they return unwrapped values.
<br>
<br>
Explicit chaining can be enabled by using the `_.chain` method.

#### Arguments
1. `value` *(&#42;)*: The value to wrap in a `lodash` instance.

#### Returns
*(Object)*:  Returns a `lodash` instance.

#### Example
```js
var wrapped = _([1, 2, 3]);

// returns an unwrapped value
wrapped.reduce(function(sum, num) {
  return sum + num;
});
// => 6

// returns a wrapped value
var squares = wrapped.map(function(num) {
  return num * num;
});

_.isArray(squares);
// => false

_.isArray(squares.value());
// => true
```
* * *

### _.chain(value)

Creates a `lodash` object that wraps the given value with explicit
method chaining enabled.

#### Arguments
1. `value` *(&#42;)*: The value to wrap.

#### Returns
*(Object)*:  Returns the wrapper object.

#### Example
```js
var characters = [
  { 'name': 'barney',  'age': 36 },
  { 'name': 'fred',    'age': 40 },
  { 'name': 'pebbles', 'age': 1 }
];

var youngest = _.chain(characters)
    .sortBy('age')
    .map(function(chr) { return chr.name + ' is ' + chr.age; })
    .first()
    .value();
// => 'pebbles is 1'
```
* * *

### _.tap(value, interceptor)

Invokes `interceptor` with the `value` as the first argument and then
returns `value`. The purpose of this method is to "tap into" a method
chain in order to perform operations on intermediate results within
the chain.

#### Arguments
1. `value` *(&#42;)*: The value to provide to `interceptor`.
2. `interceptor` *(Function)*: The function to invoke.

#### Returns
*(&#42;)*:  Returns `value`.

#### Example
```js
_([1, 2, 3, 4])
 .tap(function(array) { array.pop(); })
 .reverse()
 .value();
// => [3, 2, 1]
```
* * *

### _.prototype.chain()

Enables explicit method chaining on the wrapper object.

#### Returns
*(&#42;)*:  Returns the wrapper object.

#### Example
```js
var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

// without explicit chaining
_(characters).first();
// => { 'name': 'barney', 'age': 36 }

// with explicit chaining
_(characters).chain()
  .first()
  .pick('age')
  .value();
// => { 'age': 36 }
```
* * *

### _.prototype.toString()

Produces the `toString` result of the wrapped value.

#### Returns
*(string)*:  Returns the string result.

#### Example
```js
_([1, 2, 3]).toString();
// => '1,2,3'
```
* * *

### _.prototype.valueOf()

Extracts the wrapped value.

#### Aliases
*_.prototype.value*

#### Returns
*(&#42;)*:  Returns the wrapped value.

#### Example
```js
_([1, 2, 3]).valueOf();
// => [1, 2, 3]
```
* * *
