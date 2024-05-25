[TOC]

### _(value)

Creates a `lodash` object, which wraps the given `value`, to enable method chaining.

In addition to Lo-Dash methods, wrappers also have the following `Array` methods:<br>
`concat`, `join`, `pop`, `push`, `reverse`, `shift`, `slice`, `sort`, `splice`, and `unshift`

Chaining is supported in custom builds as long as the `value` method is implicitly or explicitly included in the build.

The chainable wrapper functions are:<br>
`after`, `assign`, `bind`, `bindAll`, `bindKey`, `chain`, `compact`, `compose`, `concat`, `countBy`, `createCallback`, `debounce`, `defaults`, `defer`, `delay`, `difference`, `filter`, `flatten`, `forEach`, `forIn`, `forOwn`, `functions`, `groupBy`, `initial`, `intersection`, `invert`, `invoke`, `keys`, `map`, `max`, `memoize`, `merge`, `min`, `object`, `omit`, `once`, `pairs`, `partial`, `partialRight`, `pick`, `pluck`, `push`, `range`, `reject`, `rest`, `reverse`, `shuffle`, `slice`, `sort`, `sortBy`, `splice`, `tap`, `throttle`, `times`, `toArray`, `transform`, `union`, `uniq`, `unshift`, `unzip`, `values`, `where`, `without`, `wrap`, and `zip`

The non-chainable wrapper functions are:<br>
`clone`, `cloneDeep`, `contains`, `escape`, `every`, `find`, `has`, `identity`, `indexOf`, `isArguments`, `isArray`, `isBoolean`, `isDate`, `isElement`, `isEmpty`, `isEqual`, `isFinite`, `isFunction`, `isNaN`, `isNull`, `isNumber`, `isObject`, `isPlainObject`, `isRegExp`, `isString`, `isUndefined`, `join`, `lastIndexOf`, `mixin`, `noConflict`, `parseInt`, `pop`, `random`, `reduce`, `reduceRight`, `result`, `shift`, `size`, `some`, `sortedIndex`, `runInContext`, `template`, `unescape`, `uniqueId`, and `value`

The wrapper functions `first` and `last` return wrapped values when `n` is passed, otherwise they return unwrapped values.

#### Aliases

*chain*

#### Arguments

1. `value` *(Mixed)*: The value to wrap in a `lodash` instance.

#### Returns

*(Object)*: Returns a `lodash` instance.

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

### _.tap(value, interceptor)

Invokes `interceptor` with the `value` as the first argument, and then returns `value`. The purpose of this method is to "tap into" a method chain, in order to perform operations on intermediate results within the chain.

#### Arguments

1. `value` *(Mixed)*: The value to pass to `interceptor`.
2. `interceptor` *(Function)*: The function to invoke.

#### Returns

*(Mixed)*: Returns `value`.

#### Example

```js
_([1, 2, 3, 4])
 .filter(function(num) { return num % 2 == 0; })
 .tap(alert)
 .map(function(num) { return num * num; })
 .value();
// => // [2, 4] (alerted)
// => [4, 16]
```

* * *

### _.prototype.toString()

Produces the `toString` result of the wrapped value.

#### Returns

*(String)*: Returns the string result.

#### Example

```js
_([1, 2, 3]).toString();
// => '1,2,3'
```

* * *

### _.prototype.valueOf()

Extracts the wrapped value.

#### Aliases

*value*

#### Returns

*(Mixed)*: Returns the wrapped value.

#### Example

```js
_([1, 2, 3]).valueOf();
// => [1, 2, 3]
```
