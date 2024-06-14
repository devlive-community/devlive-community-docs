[TOC]

### _.at(collection, [props])

Creates an array of elements corresponding to the given keys, or indexes,
of `collection`. Keys may be specified as individual arguments or as arrays
of keys.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[props]` *(...(number|number&#91;&#93;|string|string&#91;&#93;)*: The property names or indexes of elements to pick, specified individually or in arrays.

#### Returns
*(Array)*:  Returns the new array of picked elements.

#### Example
```js
_.at(['a', 'b', 'c'], [0, 2]);
// => ['a', 'c']

_.at(['barney', 'fred', 'pebbles'], 0, 2);
// => ['barney', 'pebbles']
```

### _.countBy(collection, [iteratee=_.identity], [thisArg])

Creates an object composed of keys generated from the results of running
each element of `collection` through `iteratee`. The corresponding value
of each key is the number of times the key was returned by `iteratee`.
The `iteratee` is bound to `thisArg` and invoked with three arguments:<br>
(value, index|key, collection).
<br>
<br>
If a property name is provided for `iteratee` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `iteratee` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns the composed aggregate object.

#### Example
```js
_.countBy([4.3, 6.1, 6.4], function(n) {
  return Math.floor(n);
});
// => { '4': 1, '6': 2 }

_.countBy([4.3, 6.1, 6.4], function(n) {
  return this.floor(n);
}, Math);
// => { '4': 1, '6': 2 }

_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

### _.every(collection, [predicate=_.identity], [thisArg])

Checks if `predicate` returns truthy for **all** elements of `collection`.
The predicate is bound to `thisArg` and invoked with three arguments:<br>
(value, index|key, collection).
<br>
<br>
If a property name is provided for `predicate` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `predicate` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Aliases
*_.all*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(boolean)*:  Returns `true` if all elements pass the predicate check,
else `false`.

#### Example
```js
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'active': false },
  { 'user': 'fred',   'active': false }
];

// using the `_.matches` callback shorthand
_.every(users, { 'user': 'barney', 'active': false });
// => false

// using the `_.matchesProperty` callback shorthand
_.every(users, 'active', false);
// => true

// using the `_.property` callback shorthand
_.every(users, 'active');
// => false
```

### _.filter(collection, [predicate=_.identity], [thisArg])

Iterates over elements of `collection`, returning an array of all elements
`predicate` returns truthy for. The predicate is bound to `thisArg` and
invoked with three arguments: (value, index|key, collection).
<br>
<br>
If a property name is provided for `predicate` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `predicate` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Aliases
*_.select*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the new filtered array.

#### Example
```js
_.filter([4, 5, 6], function(n) {
  return n % 2 == 0;
});
// => [4, 6]

var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

// using the `_.matches` callback shorthand
_.pluck(_.filter(users, { 'age': 36, 'active': true }), 'user');
// => ['barney']

// using the `_.matchesProperty` callback shorthand
_.pluck(_.filter(users, 'active', false), 'user');
// => ['fred']

// using the `_.property` callback shorthand
_.pluck(_.filter(users, 'active'), 'user');
// => ['barney']
```

### _.find(collection, [predicate=_.identity], [thisArg])

Iterates over elements of `collection`, returning the first element
`predicate` returns truthy for. The predicate is bound to `thisArg` and
invoked with three arguments: (value, index|key, collection).
<br>
<br>
If a property name is provided for `predicate` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `predicate` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Aliases
*_.detect*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to search.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(&#42;)*:  Returns the matched element, else `undefined`.

#### Example
```js
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

_.result(_.find(users, function(chr) {
  return chr.age < 40;
}), 'user');
// => 'barney'

// using the `_.matches` callback shorthand
_.result(_.find(users, { 'age': 1, 'active': true }), 'user');
// => 'pebbles'

// using the `_.matchesProperty` callback shorthand
_.result(_.find(users, 'active', false), 'user');
// => 'fred'

// using the `_.property` callback shorthand
_.result(_.find(users, 'active'), 'user');
// => 'barney'
```

### _.findLast(collection, [predicate=_.identity], [thisArg])

This method is like `_.find` except that it iterates over elements of
`collection` from right to left.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to search.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(&#42;)*:  Returns the matched element, else `undefined`.

#### Example
```js
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 == 1;
});
// => 3
```

### _.findWhere(collection, source)

Performs a deep comparison between each element in `collection` and the
source object, returning the first element that has equivalent property
values.
<br>
<br>
**Note:** This method supports comparing arrays, booleans, `Date` objects,
numbers, `Object` objects, regexes, and strings. Objects are compared by
their own, not inherited, enumerable properties. For comparing a single
own or inherited property value see `_.matchesProperty`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to search.
2. `source` *(Object)*: The object of property values to match.

#### Returns
*(&#42;)*:  Returns the matched element, else `undefined`.

#### Example
```js
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.result(_.findWhere(users, { 'age': 36, 'active': true }), 'user');
// => 'barney'

_.result(_.findWhere(users, { 'age': 40, 'active': false }), 'user');
// => 'fred'
```

### _.forEach(collection, [iteratee=_.identity], [thisArg])

Iterates over elements of `collection` invoking `iteratee` for each element.
The `iteratee` is bound to `thisArg` and invoked with three arguments:<br>
(value, index|key, collection). Iteratee functions may exit iteration early
by explicitly returning `false`.
<br>
<br>
**Note:** As with other "Collections" methods, objects with a "length" property
are iterated like arrays. To avoid this behavior `_.forIn` or `_.forOwn`
may be used for object iteration.

#### Aliases
*_.each*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array|Object|string)*:  Returns `collection`.

#### Example
```js
_([1, 2]).forEach(function(n) {
  console.log(n);
}).value();
// => logs each value from left to right and returns the array

_.forEach({ 'a': 1, 'b': 2 }, function(n, key) {
  console.log(n, key);
});
// => logs each value-key pair and returns the object (iteration order is not guaranteed)
```

### _.forEachRight(collection, [iteratee=_.identity], [thisArg])

This method is like `_.forEach` except that it iterates over elements of
`collection` from right to left.

#### Aliases
*_.eachRight*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array|Object|string)*:  Returns `collection`.

#### Example
```js
_([1, 2]).forEachRight(function(n) {
  console.log(n);
}).value();
// => logs each value from right to left and returns the array
```

### _.groupBy(collection, [iteratee=_.identity], [thisArg])

Creates an object composed of keys generated from the results of running
each element of `collection` through `iteratee`. The corresponding value
of each key is an array of the elements responsible for generating the key.
The `iteratee` is bound to `thisArg` and invoked with three arguments:<br>
(value, index|key, collection).
<br>
<br>
If a property name is provided for `iteratee` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `iteratee` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns the composed aggregate object.

#### Example
```js
_.groupBy([4.2, 6.1, 6.4], function(n) {
  return Math.floor(n);
});
// => { '4': [4.2], '6': [6.1, 6.4] }

_.groupBy([4.2, 6.1, 6.4], function(n) {
  return this.floor(n);
}, Math);
// => { '4': [4.2], '6': [6.1, 6.4] }

// using the `_.property` callback shorthand
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### _.includes(collection, target, [fromIndex=0])

Checks if `target` is in `collection` using
[`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons. If `fromIndex` is negative, it's used as the offset
from the end of `collection`.

#### Aliases
*_.contains, _.include*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to search.
2. `target` *(&#42;)*: The value to search for.
3. `[fromIndex=0]` *(number)*: The index to search from.

#### Returns
*(boolean)*:  Returns `true` if a matching element is found, else `false`.

#### Example
```js
_.includes([1, 2, 3], 1);
// => true

_.includes([1, 2, 3], 1, 2);
// => false

_.includes({ 'user': 'fred', 'age': 40 }, 'fred');
// => true

_.includes('pebbles', 'eb');
// => true
```

### _.indexBy(collection, [iteratee=_.identity], [thisArg])

Creates an object composed of keys generated from the results of running
each element of `collection` through `iteratee`. The corresponding value
of each key is the last element responsible for generating the key. The
iteratee function is bound to `thisArg` and invoked with three arguments:<br>
(value, index|key, collection).
<br>
<br>
If a property name is provided for `iteratee` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `iteratee` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns the composed aggregate object.

#### Example
```js
var keyData = [
  { 'dir': 'left', 'code': 97 },
  { 'dir': 'right', 'code': 100 }
];

_.indexBy(keyData, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }

_.indexBy(keyData, function(object) {
  return String.fromCharCode(object.code);
});
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }

_.indexBy(keyData, function(object) {
  return this.fromCharCode(object.code);
}, String);
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }
```

### _.invoke(collection, path, [args])

Invokes the method at `path` of each element in `collection`, returning
an array of the results of each invoked method. Any additional arguments
are provided to each invoked method. If `methodName` is a function it's
invoked for, and `this` bound to, each element in `collection`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `path` *(Array|Function|string)*: The path of the method to invoke or the function invoked per iteration.
3. `[args]` *(...&#42;)*: The arguments to invoke the method with.

#### Returns
*(Array)*:  Returns the array of results.

#### Example
```js
_.invoke([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invoke([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

### _.map(collection, [iteratee=_.identity], [thisArg])

Creates an array of values by running each element in `collection` through
`iteratee`. The `iteratee` is bound to `thisArg` and invoked with three
arguments: (value, index|key, collection).
<br>
<br>
If a property name is provided for `iteratee` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `iteratee` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.
<br>
<br>
Many lodash methods are guarded to work as iteratees for methods like
`_.every`, `_.filter`, `_.map`, `_.mapValues`, `_.reject`, and `_.some`.
<br>
<br>
The guarded methods are:<br>
`ary`, `callback`, `chunk`, `clone`, `create`, `curry`, `curryRight`,
`drop`, `dropRight`, `every`, `fill`, `flatten`, `invert`, `max`, `min`,
`parseInt`, `slice`, `sortBy`, `take`, `takeRight`, `template`, `trim`,
`trimLeft`, `trimRight`, `trunc`, `random`, `range`, `sample`, `some`,
`sum`, `uniq`, and `words`

#### Aliases
*_.collect*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array)*:  Returns the new mapped array.

#### Example
```js
function timesThree(n) {
  return n * 3;
}

_.map([1, 2], timesThree);
// => [3, 6]

_.map({ 'a': 1, 'b': 2 }, timesThree);
// => [3, 6] (iteration order is not guaranteed)

var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];

// using the `_.property` callback shorthand
_.map(users, 'user');
// => ['barney', 'fred']
```

### _.partition(collection, [predicate=_.identity], [thisArg])

Creates an array of elements split into two groups, the first of which
contains elements `predicate` returns truthy for, while the second of which
contains elements `predicate` returns falsey for. The predicate is bound
to `thisArg` and invoked with three arguments: (value, index|key, collection).
<br>
<br>
If a property name is provided for `predicate` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `predicate` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the array of grouped elements.

#### Example
```js
_.partition([1, 2, 3], function(n) {
  return n % 2;
});
// => [[1, 3], [2]]

_.partition([1.2, 2.3, 3.4], function(n) {
  return this.floor(n) % 2;
}, Math);
// => [[1.2, 3.4], [2.3]]

var users = [
  { 'user': 'barney',  'age': 36, 'active': false },
  { 'user': 'fred',    'age': 40, 'active': true },
  { 'user': 'pebbles', 'age': 1,  'active': false }
];

var mapper = function(array) {
  return _.pluck(array, 'user');
};

// using the `_.matches` callback shorthand
_.map(_.partition(users, { 'age': 1, 'active': false }), mapper);
// => [['pebbles'], ['barney', 'fred']]

// using the `_.matchesProperty` callback shorthand
_.map(_.partition(users, 'active', false), mapper);
// => [['barney', 'pebbles'], ['fred']]

// using the `_.property` callback shorthand
_.map(_.partition(users, 'active'), mapper);
// => [['fred'], ['barney', 'pebbles']]
```

### _.pluck(collection, path)

Gets the property value of `path` from all elements in `collection`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `path` *(Array|string)*: The path of the property to pluck.

#### Returns
*(Array)*:  Returns the property values.

#### Example
```js
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

_.pluck(users, 'user');
// => ['barney', 'fred']

var userIndex = _.indexBy(users, 'user');
_.pluck(userIndex, 'age');
// => [36, 40] (iteration order is not guaranteed)
```

### _.reduce(collection, [iteratee=_.identity], [accumulator], [thisArg])

Reduces `collection` to a value which is the accumulated result of running
each element in `collection` through `iteratee`, where each successive
invocation is supplied the return value of the previous. If `accumulator`
is not provided the first element of `collection` is used as the initial
value. The `iteratee` is bound to `thisArg` and invoked with four arguments:<br>
(accumulator, value, index|key, collection).
<br>
<br>
Many lodash methods are guarded to work as iteratees for methods like
`_.reduce`, `_.reduceRight`, and `_.transform`.
<br>
<br>
The guarded methods are:<br>
`assign`, `defaults`, `defaultsDeep`, `includes`, `merge`, `sortByAll`,
and `sortByOrder`

#### Aliases
*_.foldl, _.inject*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[accumulator]` *(&#42;)*: The initial value.
4. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(&#42;)*:  Returns the accumulated value.

#### Example
```js
_.reduce([1, 2], function(total, n) {
  return total + n;
});
// => 3

_.reduce({ 'a': 1, 'b': 2 }, function(result, n, key) {
  result[key] = n * 3;
  return result;
}, {});
// => { 'a': 3, 'b': 6 } (iteration order is not guaranteed)
```

### _.reduceRight(collection, [iteratee=_.identity], [accumulator], [thisArg])

This method is like `_.reduce` except that it iterates over elements of
`collection` from right to left.

#### Aliases
*_.foldr*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[accumulator]` *(&#42;)*: The initial value.
4. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(&#42;)*:  Returns the accumulated value.

#### Example
```js
var array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

### _.reject(collection, [predicate=_.identity], [thisArg])

The opposite of `_.filter`; this method returns the elements of `collection`
that `predicate` does **not** return truthy for.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the new filtered array.

#### Example
```js
_.reject([1, 2, 3, 4], function(n) {
  return n % 2 == 0;
});
// => [1, 3]

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];

// using the `_.matches` callback shorthand
_.pluck(_.reject(users, { 'age': 40, 'active': true }), 'user');
// => ['barney']

// using the `_.matchesProperty` callback shorthand
_.pluck(_.reject(users, 'active', false), 'user');
// => ['fred']

// using the `_.property` callback shorthand
_.pluck(_.reject(users, 'active'), 'user');
// => ['barney']
```

### _.sample(collection, [n])

Gets a random element or `n` random elements from a collection.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to sample.
2. `[n]` *(number)*: The number of elements to sample.

#### Returns
*(&#42;)*:  Returns the random sample(s).

#### Example
```js
_.sample([1, 2, 3, 4]);
// => 2

_.sample([1, 2, 3, 4], 2);
// => [3, 1]
```

### _.shuffle(collection)

Creates an array of shuffled values, using a version of the
[Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle).

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to shuffle.

#### Returns
*(Array)*:  Returns the new shuffled array.

#### Example
```js
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

### _.size(collection)

Gets the size of `collection` by returning its length for array-like
values or the number of own enumerable properties for objects.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to inspect.

#### Returns
*(number)*:  Returns the size of `collection`.

#### Example
```js
_.size([1, 2, 3]);
// => 3

_.size({ 'a': 1, 'b': 2 });
// => 2

_.size('pebbles');
// => 7
```

### _.some(collection, [predicate=_.identity], [thisArg])

Checks if `predicate` returns truthy for **any** element of `collection`.
The function returns as soon as it finds a passing value and does not iterate
over the entire collection. The predicate is bound to `thisArg` and invoked
with three arguments: (value, index|key, collection).
<br>
<br>
If a property name is provided for `predicate` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `predicate` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Aliases
*_.any*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(boolean)*:  Returns `true` if any element passes the predicate check,
else `false`.

#### Example
```js
_.some([null, 0, 'yes', false], Boolean);
// => true

var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];

// using the `_.matches` callback shorthand
_.some(users, { 'user': 'barney', 'active': false });
// => false

// using the `_.matchesProperty` callback shorthand
_.some(users, 'active', false);
// => true

// using the `_.property` callback shorthand
_.some(users, 'active');
// => true
```

### _.sortBy(collection, [iteratee=_.identity], [thisArg])

Creates an array of elements, sorted in ascending order by the results of
running each element in a collection through `iteratee`. This method performs
a stable sort, that is, it preserves the original sort order of equal elements.
The `iteratee` is bound to `thisArg` and invoked with three arguments:<br>
(value, index|key, collection).
<br>
<br>
If a property name is provided for `iteratee` the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If a value is also provided for `thisArg` the created `_.matchesProperty`
style callback returns `true` for elements that have a matching property
value, else `false`.
<br>
<br>
If an object is provided for `iteratee` the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array)*:  Returns the new sorted array.

#### Example
```js
_.sortBy([1, 2, 3], function(n) {
  return Math.sin(n);
});
// => [3, 1, 2]

_.sortBy([1, 2, 3], function(n) {
  return this.sin(n);
}, Math);
// => [3, 1, 2]

var users = [
  { 'user': 'fred' },
  { 'user': 'pebbles' },
  { 'user': 'barney' }
];

// using the `_.property` callback shorthand
_.pluck(_.sortBy(users, 'user'), 'user');
// => ['barney', 'fred', 'pebbles']
```

### _.sortByAll(collection, iteratees)

This method is like `_.sortBy` except that it can sort by multiple iteratees
or property names.
<br>
<br>
If a property name is provided for an iteratee the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If an object is provided for an iteratee the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `iteratees` *(...(Function|Function&#91;&#93;|Object|Object&#91;&#93;|string|string&#91;&#93;)*:  The iteratees to sort by, specified as individual values or arrays of values.

#### Returns
*(Array)*:  Returns the new sorted array.

#### Example
```js
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 42 },
  { 'user': 'barney', 'age': 34 }
];

_.map(_.sortByAll(users, ['user', 'age']), _.values);
// => [['barney', 34], ['barney', 36], ['fred', 42], ['fred', 48]]

_.map(_.sortByAll(users, 'user', function(chr) {
  return Math.floor(chr.age / 10);
}), _.values);
// => [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 42]]
```

### _.sortByOrder(collection, iteratees, [orders])

This method is like `_.sortByAll` except that it allows specifying the
sort orders of the iteratees to sort by. If `orders` is unspecified, all
values are sorted in ascending order. Otherwise, a value is sorted in
ascending order if its corresponding order is "asc", and descending if "desc".
<br>
<br>
If a property name is provided for an iteratee the created `_.property`
style callback returns the property value of the given element.
<br>
<br>
If an object is provided for an iteratee the created `_.matches` style
callback returns `true` for elements that have the properties of the given
object, else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `iteratees` *(Function&#91;&#93;|Object&#91;&#93;|string&#91;&#93;)*: The iteratees to sort by.
3. `[orders]` *(boolean&#91;&#93;)*: The sort orders of `iteratees`.

#### Returns
*(Array)*:  Returns the new sorted array.

#### Example
```js
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 42 },
  { 'user': 'barney', 'age': 36 }
];

// sort by `user` in ascending order and by `age` in descending order
_.map(_.sortByOrder(users, ['user', 'age'], ['asc', 'desc']), _.values);
// => [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 42]]
```

### _.where(collection, source)

Performs a deep comparison between each element in `collection` and the
source object, returning an array of all elements that have equivalent
property values.
<br>
<br>
**Note:** This method supports comparing arrays, booleans, `Date` objects,
numbers, `Object` objects, regexes, and strings. Objects are compared by
their own, not inherited, enumerable properties. For comparing a single
own or inherited property value see `_.matchesProperty`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to search.
2. `source` *(Object)*: The object of property values to match.

#### Returns
*(Array)*:  Returns the new filtered array.

#### Example
```js
var users = [
  { 'user': 'barney', 'age': 36, 'active': false, 'pets': ['hoppy'] },
  { 'user': 'fred',   'age': 40, 'active': true, 'pets': ['baby puss', 'dino'] }
];

_.pluck(_.where(users, { 'age': 36, 'active': false }), 'user');
// => ['barney']

_.pluck(_.where(users, { 'pets': ['dino'] }), 'user');
// => ['fred']
```
