[TOC]

### _(value)

Creates a `lodash` object which wraps `value` to enable implicit chaining.
Methods that operate on and return arrays, collections, and functions can
be chained together. Methods that retrieve a single value or may return a
primitive value will automatically end the chain returning the unwrapped
value. Explicit chaining may be enabled using `_.chain`. The execution of
chained methods is lazy, that is, execution is deferred until `_#value`
is implicitly or explicitly called.
<br>
<br>
Lazy evaluation allows several methods to support shortcut fusion. Shortcut
fusion is an optimization strategy which merge iteratee calls; this can help
to avoid the creation of intermediate data structures and greatly reduce the
number of iteratee executions.
<br>
<br>
Chaining is supported in custom builds as long as the `_#value` method is
directly or indirectly included in the build.
<br>
<br>
In addition to lodash methods, wrappers have `Array` and `String` methods.
<br>
<br>
The wrapper `Array` methods are:<br>
`concat`, `join`, `pop`, `push`, `reverse`, `shift`, `slice`, `sort`,
`splice`, and `unshift`
<br>
<br>
The wrapper `String` methods are:<br>
`replace` and `split`
<br>
<br>
The wrapper methods that support shortcut fusion are:<br>
`compact`, `drop`, `dropRight`, `dropRightWhile`, `dropWhile`, `filter`,
`first`, `initial`, `last`, `map`, `pluck`, `reject`, `rest`, `reverse`,
`slice`, `take`, `takeRight`, `takeRightWhile`, `takeWhile`, `toArray`,
and `where`
<br>
<br>
The chainable wrapper methods are:<br>
`after`, `ary`, `assign`, `at`, `before`, `bind`, `bindAll`, `bindKey`,
`callback`, `chain`, `chunk`, `commit`, `compact`, `concat`, `constant`,
`countBy`, `create`, `curry`, `debounce`, `defaults`, `defaultsDeep`,
`defer`, `delay`, `difference`, `drop`, `dropRight`, `dropRightWhile`,
`dropWhile`, `fill`, `filter`, `flatten`, `flattenDeep`, `flow`, `flowRight`,
`forEach`, `forEachRight`, `forIn`, `forInRight`, `forOwn`, `forOwnRight`,
`functions`, `groupBy`, `indexBy`, `initial`, `intersection`, `invert`,
`invoke`, `keys`, `keysIn`, `map`, `mapKeys`, `mapValues`, `matches`,
`matchesProperty`, `memoize`, `merge`, `method`, `methodOf`, `mixin`,
`modArgs`, `negate`, `omit`, `once`, `pairs`, `partial`, `partialRight`,
`partition`, `pick`, `plant`, `pluck`, `property`, `propertyOf`, `pull`,
`pullAt`, `push`, `range`, `rearg`, `reject`, `remove`, `rest`, `restParam`,
`reverse`, `set`, `shuffle`, `slice`, `sort`, `sortBy`, `sortByAll`,
`sortByOrder`, `splice`, `spread`, `take`, `takeRight`, `takeRightWhile`,
`takeWhile`, `tap`, `throttle`, `thru`, `times`, `toArray`, `toPlainObject`,
`transform`, `union`, `uniq`, `unshift`, `unzip`, `unzipWith`, `values`,
`valuesIn`, `where`, `without`, `wrap`, `xor`, `zip`, `zipObject`, `zipWith`
<br>
<br>
The wrapper methods that are **not** chainable by default are:<br>
`add`, `attempt`, `camelCase`, `capitalize`, `ceil`, `clone`, `cloneDeep`,
`deburr`, `endsWith`, `escape`, `escapeRegExp`, `every`, `find`, `findIndex`,
`findKey`, `findLast`, `findLastIndex`, `findLastKey`, `findWhere`, `first`,
`floor`, `get`, `gt`, `gte`, `has`, `identity`, `includes`, `indexOf`,
`inRange`, `isArguments`, `isArray`, `isBoolean`, `isDate`, `isElement`,
`isEmpty`, `isEqual`, `isError`, `isFinite` `isFunction`, `isMatch`,
`isNative`, `isNaN`, `isNull`, `isNumber`, `isObject`, `isPlainObject`,
`isRegExp`, `isString`, `isUndefined`, `isTypedArray`, `join`, `kebabCase`,
`last`, `lastIndexOf`, `lt`, `lte`, `max`, `min`, `noConflict`, `noop`,
`now`, `pad`, `padLeft`, `padRight`, `parseInt`, `pop`, `random`, `reduce`,
`reduceRight`, `repeat`, `result`, `round`, `runInContext`, `shift`, `size`,
`snakeCase`, `some`, `sortedIndex`, `sortedLastIndex`, `startCase`,
`startsWith`, `sum`, `template`, `trim`, `trimLeft`, `trimRight`, `trunc`,
`unescape`, `uniqueId`, `value`, and `words`
<br>
<br>
The wrapper method `sample` will return a wrapped value when `n` is provided,
otherwise an unwrapped value is returned.

#### Arguments
1. `value` *(&#42;)*: The value to wrap in a `lodash` instance.

#### Returns
*(Object)*:  Returns the new `lodash` wrapper instance.

#### Example
```js
var wrapped = _([1, 2, 3]);

// returns an unwrapped value
wrapped.reduce(function(total, n) {
  return total + n;
});
// => 6

// returns a wrapped value
var squares = wrapped.map(function(n) {
  return n * n;
});

_.isArray(squares);
// => false

_.isArray(squares.value());
// => true
```

### _.chain(value)

Creates a `lodash` object that wraps `value` with explicit method
chaining enabled.

#### Arguments
1. `value` *(&#42;)*: The value to wrap.

#### Returns
*(Object)*:  Returns the new `lodash` wrapper instance.

#### Example
```js
var users = [
  { 'user': 'barney',  'age': 36 },
  { 'user': 'fred',    'age': 40 },
  { 'user': 'pebbles', 'age': 1 }
];

var youngest = _.chain(users)
  .sortBy('age')
  .map(function(chr) {
    return chr.user + ' is ' + chr.age;
  })
  .first()
  .value();
// => 'pebbles is 1'
```

### _.tap(value, interceptor, [thisArg])

This method invokes `interceptor` and returns `value`. The interceptor is
bound to `thisArg` and invoked with one argument; (value). The purpose of
this method is to "tap into" a method chain in order to perform operations
on intermediate results within the chain.

#### Arguments
1. `value` *(&#42;)*: The value to provide to `interceptor`.
2. `interceptor` *(Function)*: The function to invoke.
3. `[thisArg]` *(&#42;)*: The `this` binding of `interceptor`.

#### Returns
*(&#42;)*:  Returns `value`.

#### Example
```js
_([1, 2, 3])
 .tap(function(array) {
   array.pop();
 })
 .reverse()
 .value();
// => [2, 1]
```

### _.thru(value, interceptor, [thisArg])

This method is like `_.tap` except that it returns the result of `interceptor`.

#### Arguments
1. `value` *(&#42;)*: The value to provide to `interceptor`.
2. `interceptor` *(Function)*: The function to invoke.
3. `[thisArg]` *(&#42;)*: The `this` binding of `interceptor`.

#### Returns
*(&#42;)*:  Returns the result of `interceptor`.

#### Example
```js
_('  abc  ')
 .chain()
 .trim()
 .thru(function(value) {
   return [value];
 })
 .value();
// => ['abc']
```

### _.prototype.chain()

Enables explicit method chaining on the wrapper object.

#### Returns
*(Object)*:  Returns the new `lodash` wrapper instance.

#### Example
```js
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

// without explicit chaining
_(users).first();
// => { 'user': 'barney', 'age': 36 }

// with explicit chaining
_(users).chain()
  .first()
  .pick('user')
  .value();
// => { 'user': 'barney' }
```

### _.prototype.commit()

Executes the chained sequence and returns the wrapped result.

#### Returns
*(Object)*:  Returns the new `lodash` wrapper instance.

#### Example
```js
var array = [1, 2];
var wrapped = _(array).push(3);

console.log(array);
// => [1, 2]

wrapped = wrapped.commit();
console.log(array);
// => [1, 2, 3]

wrapped.last();
// => 3

console.log(array);
// => [1, 2, 3]
```

### _.prototype.concat([values])

Creates a new array joining a wrapped array with any additional arrays
and/or values.

#### Arguments
1. `[values]` *(...&#42;)*: The values to concatenate.

#### Returns
*(Array)*:  Returns the new concatenated array.

#### Example
```js
var array = [1];
var wrapped = _(array).concat(2, [3], [[4]]);

console.log(wrapped.value());
// => [1, 2, 3, [4]]

console.log(array);
// => [1]
```

### _.prototype.plant()

Creates a clone of the chained sequence planting `value` as the wrapped value.

#### Returns
*(Object)*:  Returns the new `lodash` wrapper instance.

#### Example
```js
var array = [1, 2];
var wrapped = _(array).map(function(value) {
  return Math.pow(value, 2);
});

var other = [3, 4];
var otherWrapped = wrapped.plant(other);

otherWrapped.value();
// => [9, 16]

wrapped.value();
// => [1, 4]
```

### _.prototype.reverse()

Reverses the wrapped array so the first element becomes the last, the
second element becomes the second to last, and so on.
<br>
<br>
**Note:** This method mutates the wrapped array.

#### Returns
*(Object)*:  Returns the new reversed `lodash` wrapper instance.

#### Example
```js
var array = [1, 2, 3];

_(array).reverse().value()
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

### _.prototype.toString()

Produces the result of coercing the unwrapped value to a string.

#### Returns
*(string)*:  Returns the coerced string value.

#### Example
```js
_([1, 2, 3]).toString();
// => '1,2,3'
```

### _.prototype.value()

Executes the chained sequence to extract the unwrapped value.

#### Aliases
*_.prototype.run, _.prototype.toJSON, _.prototype.valueOf*

#### Returns
*(&#42;)*:  Returns the resolved unwrapped value.

#### Example
```js
_([1, 2, 3]).value();
// => [1, 2, 3]
```
