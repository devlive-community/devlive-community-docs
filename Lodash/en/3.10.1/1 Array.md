[TOC]

### .chunk(array, [size=1])

Creates an array of elements split into groups the length of `size`.
If `collection` can't be split evenly, the final chunk will be the remaining
elements.

#### Arguments
1. `array` *(Array)*: The array to process.
2. `[size=1]` *(number)*: The length of each chunk.

#### Returns
*(Array)*:  Returns the new array containing chunks.

#### Example
```js
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

### .compact(array)

Creates an array with all falsey values removed. The values `false`, `null`,
`0`, `""`, `undefined`, and `NaN` are falsey.

#### Arguments
1. `array` *(Array)*: The array to compact.

#### Returns
*(Array)*:  Returns the new array of filtered values.

#### Example
```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

### .difference(array, [values])

Creates an array of unique `array` values not included in the other
provided arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons.

#### Arguments
1. `array` *(Array)*: The array to inspect.
2. `[values]` *(...Array)*: The arrays of values to exclude.

#### Returns
*(Array)*:  Returns the new array of filtered values.

#### Example
```js
_.difference([1, 2, 3], [4, 2]);
// => [1, 3]
```

### .drop(array, [n=1])

Creates a slice of `array` with `n` elements dropped from the beginning.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[n=1]` *(number)*: The number of elements to drop.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.drop([1, 2, 3]);
// => [2, 3]

_.drop([1, 2, 3], 2);
// => [3]

_.drop([1, 2, 3], 5);
// => []

_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

### .dropRight(array, [n=1])

Creates a slice of `array` with `n` elements dropped from the end.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[n=1]` *(number)*: The number of elements to drop.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.dropRight([1, 2, 3]);
// => [1, 2]

_.dropRight([1, 2, 3], 2);
// => [1]

_.dropRight([1, 2, 3], 5);
// => []

_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]
```

### .dropRightWhile(array, [predicate=_.identity], [thisArg])

Creates a slice of `array` excluding elements dropped from the end.
Elements are dropped until `predicate` returns falsey. The predicate is
bound to `thisArg` and invoked with three arguments: (value, index, array).
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
callback returns `true` for elements that match the properties of the given
object, else `false`.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.dropRightWhile([1, 2, 3], function(n) {
  return n > 1;
});
// => [1]

var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

// using the `_.matches` callback shorthand
_.pluck(_.dropRightWhile(users, { 'user': 'pebbles', 'active': false }), 'user');
// => ['barney', 'fred']

// using the `_.matchesProperty` callback shorthand
_.pluck(_.dropRightWhile(users, 'active', false), 'user');
// => ['barney']

// using the `_.property` callback shorthand
_.pluck(_.dropRightWhile(users, 'active'), 'user');
// => ['barney', 'fred', 'pebbles']
```

### .dropWhile(array, [predicate=_.identity], [thisArg])

Creates a slice of `array` excluding elements dropped from the beginning.
Elements are dropped until `predicate` returns falsey. The predicate is
bound to `thisArg` and invoked with three arguments: (value, index, array).
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
1. `array` *(Array)*: The array to query.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.dropWhile([1, 2, 3], function(n) {
  return n < 3;
});
// => [3]

var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

// using the `_.matches` callback shorthand
_.pluck(_.dropWhile(users, { 'user': 'barney', 'active': false }), 'user');
// => ['fred', 'pebbles']

// using the `_.matchesProperty` callback shorthand
_.pluck(_.dropWhile(users, 'active', false), 'user');
// => ['pebbles']

// using the `_.property` callback shorthand
_.pluck(_.dropWhile(users, 'active'), 'user');
// => ['barney', 'fred', 'pebbles']
```

### .fill(array, value, [start=0], [end=array.length])

Fills elements of `array` with `value` from `start` up to, but not
including, `end`.
<br>
<br>
**Note:** This method mutates `array`.

#### Arguments
1. `array` *(Array)*: The array to fill.
2. `value` *(&#42;)*: The value to fill `array` with.
3. `[start=0]` *(number)*: The start position.
4. `[end=array.length]` *(number)*: The end position.

#### Returns
*(Array)*:  Returns `array`.

#### Example
```js
var array = [1, 2, 3];

_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']

_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8], '*', 1, 2);
// => [4, '*', 8]
```

### .findIndex(array, [predicate=_.identity], [thisArg])

This method is like `_.find` except that it returns the index of the first
element `predicate` returns truthy for instead of the element itself.
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
1. `array` *(Array)*: The array to search.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(number)*:  Returns the index of the found element, else `-1`.

#### Example
```js
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

_.findIndex(users, function(chr) {
  return chr.user == 'barney';
});
// => 0

// using the `_.matches` callback shorthand
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1

// using the `_.matchesProperty` callback shorthand
_.findIndex(users, 'active', false);
// => 0

// using the `_.property` callback shorthand
_.findIndex(users, 'active');
// => 2
```

### .findLastIndex(array, [predicate=_.identity], [thisArg])

This method is like `_.findIndex` except that it iterates over elements
of `collection` from right to left.
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
1. `array` *(Array)*: The array to search.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(number)*:  Returns the index of the found element, else `-1`.

#### Example
```js
var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

_.findLastIndex(users, function(chr) {
  return chr.user == 'pebbles';
});
// => 2

// using the `_.matches` callback shorthand
_.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0

// using the `_.matchesProperty` callback shorthand
_.findLastIndex(users, 'active', false);
// => 2

// using the `_.property` callback shorthand
_.findLastIndex(users, 'active');
// => 0
```

### .first(array)

Gets the first element of `array`.

#### Aliases
*_.head*

#### Arguments
1. `array` *(Array)*: The array to query.

#### Returns
*(&#42;)*:  Returns the first element of `array`.

#### Example
```js
_.first([1, 2, 3]);
// => 1

_.first([]);
// => undefined
```

### .flatten(array, [isDeep])

Flattens a nested array. If `isDeep` is `true` the array is recursively
flattened, otherwise it's only flattened a single level.

#### Arguments
1. `array` *(Array)*: The array to flatten.
2. `[isDeep]` *(boolean)*: Specify a deep flatten.

#### Returns
*(Array)*:  Returns the new flattened array.

#### Example
```js
_.flatten([1, [2, 3, [4]]]);
// => [1, 2, 3, [4]]

// using `isDeep`
_.flatten([1, [2, 3, [4]]], true);
// => [1, 2, 3, 4]
```

### .flattenDeep(array)

Recursively flattens a nested array.

#### Arguments
1. `array` *(Array)*: The array to recursively flatten.

#### Returns
*(Array)*:  Returns the new flattened array.

#### Example
```js
_.flattenDeep([1, [2, 3, [4]]]);
// => [1, 2, 3, 4]
```

### .indexOf(array, value, [fromIndex=0])

Gets the index at which the first occurrence of `value` is found in `array`
using [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons. If `fromIndex` is negative, it's used as the offset
from the end of `array`. If `array` is sorted providing `true` for `fromIndex`
performs a faster binary search.

#### Arguments
1. `array` *(Array)*: The array to search.
2. `value` *(&#42;)*: The value to search for.
3. `[fromIndex=0]` *(boolean|number)*: The index to search from or `true` to perform a binary search on a sorted array.

#### Returns
*(number)*:  Returns the index of the matched value, else `-1`.

#### Example
```js
_.indexOf([1, 2, 1, 2], 2);
// => 1

// using `fromIndex`
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3

// performing a binary search
_.indexOf([1, 1, 2, 2], 2, true);
// => 2
```

### .initial(array)

Gets all but the last element of `array`.

#### Arguments
1. `array` *(Array)*: The array to query.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.initial([1, 2, 3]);
// => [1, 2]
```

### .intersection([arrays])

Creates an array of unique values that are included in all of the provided
arrays using [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons.

#### Arguments
1. `[arrays]` *(...Array)*: The arrays to inspect.

#### Returns
*(Array)*:  Returns the new array of shared values.

#### Example
```js
_.intersection([1, 2], [4, 2], [2, 1]);
// => [2]
```

### .last(array)

Gets the last element of `array`.

#### Arguments
1. `array` *(Array)*: The array to query.

#### Returns
*(&#42;)*:  Returns the last element of `array`.

#### Example
```js
_.last([1, 2, 3]);
// => 3
```

### .lastIndexOf(array, value, [fromIndex=array.length-1])

This method is like `_.indexOf` except that it iterates over elements of
`array` from right to left.

#### Arguments
1. `array` *(Array)*: The array to search.
2. `value` *(&#42;)*: The value to search for.
3. `[fromIndex=array.length-1]` *(boolean|number)*: The index to search from or `true` to perform a binary search on a sorted array.

#### Returns
*(number)*:  Returns the index of the matched value, else `-1`.

#### Example
```js
_.lastIndexOf([1, 2, 1, 2], 2);
// => 3

// using `fromIndex`
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1

// performing a binary search
_.lastIndexOf([1, 1, 2, 2], 2, true);
// => 3
```

### .pull(array, [values])

Removes all provided values from `array` using
[`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons.
<br>
<br>
**Note:** Unlike `_.without`, this method mutates `array`.

#### Arguments
1. `array` *(Array)*: The array to modify.
2. `[values]` *(...&#42;)*: The values to remove.

#### Returns
*(Array)*:  Returns `array`.

#### Example
```js
var array = [1, 2, 3, 1, 2, 3];

_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```

### .pullAt(array, [indexes])

Removes elements from `array` corresponding to the given indexes and returns
an array of the removed elements. Indexes may be specified as an array of
indexes or as individual arguments.
<br>
<br>
**Note:** Unlike `_.at`, this method mutates `array`.

#### Arguments
1. `array` *(Array)*: The array to modify.
2. `[indexes]` *(...(number|number&#91;&#93;)*: The indexes of elements to remove, specified as individual indexes or arrays of indexes.

#### Returns
*(Array)*:  Returns the new array of removed elements.

#### Example
```js
var array = [5, 10, 15, 20];
var evens = _.pullAt(array, 1, 3);

console.log(array);
// => [5, 15]

console.log(evens);
// => [10, 20]
```

### .remove(array, [predicate=_.identity], [thisArg])

Removes all elements from `array` that `predicate` returns truthy for
and returns an array of the removed elements. The predicate is bound to
`thisArg` and invoked with three arguments: (value, index, array).
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
<br>
<br>
**Note:** Unlike `_.filter`, this method mutates `array`.

#### Arguments
1. `array` *(Array)*: The array to modify.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the new array of removed elements.

#### Example
```js
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4]
```

### .rest(array)

Gets all but the first element of `array`.

#### Aliases
*_.tail*

#### Arguments
1. `array` *(Array)*: The array to query.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.rest([1, 2, 3]);
// => [2, 3]
```

### .slice(array, [start=0], [end=array.length])

Creates a slice of `array` from `start` up to, but not including, `end`.
<br>
<br>
**Note:** This method is used instead of `Array#slice` to support node
lists in IE < 9 and to ensure dense arrays are returned.

#### Arguments
1. `array` *(Array)*: The array to slice.
2. `[start=0]` *(number)*: The start position.
3. `[end=array.length]` *(number)*: The end position.

#### Returns
*(Array)*:  Returns the slice of `array`.

### .sortedIndex(array, value, [iteratee=_.identity], [thisArg])

Uses a binary search to determine the lowest index at which `value` should
be inserted into `array` in order to maintain its sort order. If an iteratee
function is provided it's invoked for `value` and each element of `array`
to compute their sort ranking. The iteratee is bound to `thisArg` and
invoked with one argument; (value).
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
1. `array` *(Array)*: The sorted array to inspect.
2. `value` *(&#42;)*: The value to evaluate.
3. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
4. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(number)*:  Returns the index at which `value` should be inserted
into `array`.

#### Example
```js
_.sortedIndex([30, 50], 40);
// => 1

_.sortedIndex([4, 4, 5, 5], 5);
// => 2

var dict = { 'data': { 'thirty': 30, 'forty': 40, 'fifty': 50 } };

// using an iteratee function
_.sortedIndex(['thirty', 'fifty'], 'forty', function(word) {
  return this.data[word];
}, dict);
// => 1

// using the `_.property` callback shorthand
_.sortedIndex([{ 'x': 30 }, { 'x': 50 }], { 'x': 40 }, 'x');
// => 1
```

### .sortedLastIndex(array, value, [iteratee=_.identity], [thisArg])

This method is like `_.sortedIndex` except that it returns the highest
index at which `value` should be inserted into `array` in order to
maintain its sort order.

#### Arguments
1. `array` *(Array)*: The sorted array to inspect.
2. `value` *(&#42;)*: The value to evaluate.
3. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
4. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(number)*:  Returns the index at which `value` should be inserted
into `array`.

#### Example
```js
_.sortedLastIndex([4, 4, 5, 5], 5);
// => 4
```

### .take(array, [n=1])

Creates a slice of `array` with `n` elements taken from the beginning.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[n=1]` *(number)*: The number of elements to take.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.take([1, 2, 3]);
// => [1]

_.take([1, 2, 3], 2);
// => [1, 2]

_.take([1, 2, 3], 5);
// => [1, 2, 3]

_.take([1, 2, 3], 0);
// => []
```

### .takeRight(array, [n=1])

Creates a slice of `array` with `n` elements taken from the end.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[n=1]` *(number)*: The number of elements to take.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.takeRight([1, 2, 3]);
// => [3]

_.takeRight([1, 2, 3], 2);
// => [2, 3]

_.takeRight([1, 2, 3], 5);
// => [1, 2, 3]

_.takeRight([1, 2, 3], 0);
// => []
```

### .takeRightWhile(array, [predicate=_.identity], [thisArg])

Creates a slice of `array` with elements taken from the end. Elements are
taken until `predicate` returns falsey. The predicate is bound to `thisArg`
and invoked with three arguments: (value, index, array).
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
1. `array` *(Array)*: The array to query.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.takeRightWhile([1, 2, 3], function(n) {
  return n > 1;
});
// => [2, 3]

var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];

// using the `_.matches` callback shorthand
_.pluck(_.takeRightWhile(users, { 'user': 'pebbles', 'active': false }), 'user');
// => ['pebbles']

// using the `_.matchesProperty` callback shorthand
_.pluck(_.takeRightWhile(users, 'active', false), 'user');
// => ['fred', 'pebbles']

// using the `_.property` callback shorthand
_.pluck(_.takeRightWhile(users, 'active'), 'user');
// => []
```

### .takeWhile(array, [predicate=_.identity], [thisArg])

Creates a slice of `array` with elements taken from the beginning. Elements
are taken until `predicate` returns falsey. The predicate is bound to
`thisArg` and invoked with three arguments: (value, index, array).
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
1. `array` *(Array)*: The array to query.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Array)*:  Returns the slice of `array`.

#### Example
```js
_.takeWhile([1, 2, 3], function(n) {
  return n < 3;
});
// => [1, 2]

var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false},
  { 'user': 'pebbles', 'active': true }
];

// using the `_.matches` callback shorthand
_.pluck(_.takeWhile(users, { 'user': 'barney', 'active': false }), 'user');
// => ['barney']

// using the `_.matchesProperty` callback shorthand
_.pluck(_.takeWhile(users, 'active', false), 'user');
// => ['barney', 'fred']

// using the `_.property` callback shorthand
_.pluck(_.takeWhile(users, 'active'), 'user');
// => []
```

### .union([arrays])

Creates an array of unique values, in order, from all of the provided arrays
using [`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons.

#### Arguments
1. `[arrays]` *(...Array)*: The arrays to inspect.

#### Returns
*(Array)*:  Returns the new array of combined values.

#### Example
```js
_.union([1, 2], [4, 2], [2, 1]);
// => [1, 2, 4]
```

### .uniq(array, [isSorted], [iteratee], [thisArg])

Creates a duplicate-free version of an array, using
[`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons, in which only the first occurence of each element
is kept. Providing `true` for `isSorted` performs a faster search algorithm
for sorted arrays. If an iteratee function is provided it's invoked for
each element in the array to generate the criterion by which uniqueness
is computed. The `iteratee` is bound to `thisArg` and invoked with three
arguments: (value, index, array).
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

#### Aliases
*_.unique*

#### Arguments
1. `array` *(Array)*: The array to inspect.
2. `[isSorted]` *(boolean)*: Specify the array is sorted.
3. `[iteratee]` *(Function|Object|string)*: The function invoked per iteration.
4. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array)*:  Returns the new duplicate-value-free array.

#### Example
```js
_.uniq([2, 1, 2]);
// => [2, 1]

// using `isSorted`
_.uniq([1, 1, 2], true);
// => [1, 2]

// using an iteratee function
_.uniq([1, 2.5, 1.5, 2], function(n) {
  return this.floor(n);
}, Math);
// => [1, 2.5]

// using the `_.property` callback shorthand
_.uniq([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```

### .unzip(array)

This method is like `_.zip` except that it accepts an array of grouped
elements and creates an array regrouping the elements to their pre-zip
configuration.

#### Arguments
1. `array` *(Array)*: The array of grouped elements to process.

#### Returns
*(Array)*:  Returns the new array of regrouped elements.

#### Example
```js
var zipped = _.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]]

_.unzip(zipped);
// => [['fred', 'barney'], [30, 40], [true, false]]
```

### .unzipWith(array, [iteratee], [thisArg])

This method is like `_.unzip` except that it accepts an iteratee to specify
how regrouped values should be combined. The `iteratee` is bound to `thisArg`
and invoked with four arguments: (accumulator, value, index, group).

#### Arguments
1. `array` *(Array)*: The array of grouped elements to process.
2. `[iteratee]` *(Function)*: The function to combine regrouped values.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array)*:  Returns the new array of regrouped elements.

#### Example
```js
var zipped = _.zip([1, 2], [10, 20], [100, 200]);
// => [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add);
// => [3, 30, 300]
```

### .without(array, [values])

Creates an array excluding all provided values using
[`SameValueZero`](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)
for equality comparisons.

#### Arguments
1. `array` *(Array)*: The array to filter.
2. `[values]` *(...&#42;)*: The values to exclude.

#### Returns
*(Array)*:  Returns the new array of filtered values.

#### Example
```js
_.without([1, 2, 1, 3], 1, 2);
// => [3]
```

### .xor([arrays])

Creates an array of unique values that is the [symmetric difference](https://en.wikipedia.org/wiki/Symmetric_difference)
of the provided arrays.

#### Arguments
1. `[arrays]` *(...Array)*: The arrays to inspect.

#### Returns
*(Array)*:  Returns the new array of values.

#### Example
```js
_.xor([1, 2], [4, 2]);
// => [1, 4]
```

### .zip([arrays])

Creates an array of grouped elements, the first of which contains the first
elements of the given arrays, the second of which contains the second elements
of the given arrays, and so on.

#### Arguments
1. `[arrays]` *(...Array)*: The arrays to process.

#### Returns
*(Array)*:  Returns the new array of grouped elements.

#### Example
```js
_.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]]
```

### .zipObject(props, [values=[]])

The inverse of `_.pairs`; this method returns an object composed from arrays
of property names and values. Provide either a single two dimensional array,
e.g. `[[key1, value1], [key2, value2]]` or two arrays, one of property names
and one of corresponding values.

#### Aliases
*_.object*

#### Arguments
1. `props` *(Array)*: The property names.
2. `[values=[]]` *(Array)*: The property values.

#### Returns
*(Object)*:  Returns the new object.

#### Example
```js
_.zipObject([['fred', 30], ['barney', 40]]);
// => { 'fred': 30, 'barney': 40 }

_.zipObject(['fred', 'barney'], [30, 40]);
// => { 'fred': 30, 'barney': 40 }
```

### .zipWith([arrays], [iteratee], [thisArg])

This method is like `_.zip` except that it accepts an iteratee to specify
how grouped values should be combined. The `iteratee` is bound to `thisArg`
and invoked with four arguments: (accumulator, value, index, group).

#### Arguments
1. `[arrays]` *(...Array)*: The arrays to process.
2. `[iteratee]` *(Function)*: The function to combine grouped values.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Array)*:  Returns the new array of grouped elements.

#### Example
```js
_.zipWith([1, 2], [10, 20], [100, 200], _.add);
// => [111, 222]
```

