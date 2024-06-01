[TOC]

### _.compact(array)

Creates an array with all falsey values removed. The values `false`, `null`,
`0`, `""`, `undefined`, and `NaN` are all falsey.

#### Arguments

1. `array` *(Array)*: The array to compact.

#### Returns

*(Array)*:  Returns a new array of filtered values.

#### Example

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```
* * *

### _.difference(array, [values])

Creates an array excluding all values of the provided arrays using strict
equality for comparisons, i.e. `===`.

#### Arguments

1. `array` *(Array)*: The array to process.
2. `[values]` *(...Array)*: The arrays of values to exclude.

#### Returns

*(Array)*:  Returns a new array of filtered values.

#### Example

```js
_.difference([1, 2, 3, 4, 5], [5, 2, 10]);
// => [1, 3, 4]
```
* * *

### _.findIndex(array, [callback=identity], [thisArg])

This method is like `_.find` except that it returns the index of the first
element that passes the callback check, instead of the element itself.
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments

1. `array` *(Array)*: The array to search.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns

*(number)*:  Returns the index of the found element, else `-1`.

#### Example

```js
var characters = [
  { 'name': 'barney',  'age': 36, 'blocked': false },
  { 'name': 'fred',    'age': 40, 'blocked': true },
  { 'name': 'pebbles', 'age': 1,  'blocked': false }
];

_.findIndex(characters, function(chr) {
  return chr.age < 20;
});
// => 2

// using "_.where" callback shorthand
_.findIndex(characters, { 'age': 36 });
// => 0

// using "_.pluck" callback shorthand
_.findIndex(characters, 'blocked');
// => 1
```
* * *

### _.findLastIndex(array, [callback=identity], [thisArg])

This method is like `_.findIndex` except that it iterates over elements
of a `collection` from right to left.
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to search.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(number)*:  Returns the index of the found element, else `-1`.

#### Example
```js
var characters = [
  { 'name': 'barney',  'age': 36, 'blocked': true },
  { 'name': 'fred',    'age': 40, 'blocked': false },
  { 'name': 'pebbles', 'age': 1,  'blocked': true }
];

_.findLastIndex(characters, function(chr) {
  return chr.age > 30;
});
// => 1

// using "_.where" callback shorthand
_.findLastIndex(characters, { 'age': 36 });
// => 0

// using "_.pluck" callback shorthand
_.findLastIndex(characters, 'blocked');
// => 2
```
* * *

### _.first(array, [callback], [thisArg])

Gets the first element or first `n` elements of an array. If a callback
is provided elements at the beginning of the array are returned as long
as the callback returns truey. The callback is bound to `thisArg` and
invoked with three arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Aliases
*_.head, _.take*

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[callback]` *(Function|Object|number|string)*: The function called per element or the number of elements to return. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the first element(s) of `array`.

#### Example
```js
_.first([1, 2, 3]);
// => 1

_.first([1, 2, 3], 2);
// => [1, 2]

_.first([1, 2, 3], function(num) {
  return num < 3;
});
// => [1, 2]

var characters = [
  { 'name': 'barney',  'blocked': true,  'employer': 'slate' },
  { 'name': 'fred',    'blocked': false, 'employer': 'slate' },
  { 'name': 'pebbles', 'blocked': true,  'employer': 'na' }
];

// using "_.pluck" callback shorthand
_.first(characters, 'blocked');
// => [{ 'name': 'barney', 'blocked': true, 'employer': 'slate' }]

// using "_.where" callback shorthand
_.pluck(_.first(characters, { 'employer': 'slate' }), 'name');
// => ['barney', 'fred']
```
* * *

### _.flatten(array, [isShallow=false], [callback=identity], [thisArg])

Flattens a nested array (the nesting can be to any depth). If `isShallow`
is truey, the array will only be flattened a single level. If a callback
is provided each element of the array is passed through the callback before
flattening. The callback is bound to `thisArg` and invoked with three
arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to flatten.
2. `[isShallow=false]` *(boolean)*: A flag to restrict flattening to a single level.
3. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new flattened array.

#### Example
```js
_.flatten([1, [2], [3, [[4]]]]);
// => [1, 2, 3, 4];

_.flatten([1, [2], [3, [[4]]]], true);
// => [1, 2, 3, [[4]]];

var characters = [
  { 'name': 'barney', 'age': 30, 'pets': ['hoppy'] },
  { 'name': 'fred',   'age': 40, 'pets': ['baby puss', 'dino'] }
];

// using "_.pluck" callback shorthand
_.flatten(characters, 'pets');
// => ['hoppy', 'baby puss', 'dino']
```
* * *

### _.indexOf(array, value, [fromIndex=0])

Gets the index at which the first occurrence of `value` is found using
strict equality for comparisons, i.e. `===`. If the array is already sorted
providing `true` for `fromIndex` will run a faster binary search.

#### Arguments
1. `array` *(Array)*: The array to search.
2. `value` *(&#42;)*: The value to search for.
3. `[fromIndex=0]` *(boolean|number)*: The index to search from or `true` to perform a binary search on a sorted array.

#### Returns
*(number)*:  Returns the index of the matched value or `-1`.

#### Example
```js
_.indexOf([1, 2, 3, 1, 2, 3], 2);
// => 1

_.indexOf([1, 2, 3, 1, 2, 3], 2, 3);
// => 4

_.indexOf([1, 1, 2, 2, 3, 3], 2, true);
// => 2
```
* * *

### _.initial(array, [callback=1], [thisArg])

Gets all but the last element or last `n` elements of an array. If a
callback is provided elements at the end of the array are excluded from
the result as long as the callback returns truey. The callback is bound
to `thisArg` and invoked with three arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[callback=1]` *(Function|Object|number|string)*: The function called per element or the number of elements to exclude. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a slice of `array`.

#### Example
```js
_.initial([1, 2, 3]);
// => [1, 2]

_.initial([1, 2, 3], 2);
// => [1]

_.initial([1, 2, 3], function(num) {
  return num > 1;
});
// => [1]

var characters = [
  { 'name': 'barney',  'blocked': false, 'employer': 'slate' },
  { 'name': 'fred',    'blocked': true,  'employer': 'slate' },
  { 'name': 'pebbles', 'blocked': true,  'employer': 'na' }
];

// using "_.pluck" callback shorthand
_.initial(characters, 'blocked');
// => [{ 'name': 'barney',  'blocked': false, 'employer': 'slate' }]

// using "_.where" callback shorthand
_.pluck(_.initial(characters, { 'employer': 'na' }), 'name');
// => ['barney', 'fred']
```
* * *

### _.intersection([array])

Creates an array of unique values present in all provided arrays using
strict equality for comparisons, i.e. `===`.

#### Arguments
1. `[array]` *(...Array)*: The arrays to inspect.

#### Returns
*(Array)*:  Returns an array of shared values.

#### Example
```js
_.intersection([1, 2, 3], [5, 2, 1, 4], [2, 1]);
// => [1, 2]
```
* * *

### _.last(array, [callback], [thisArg])

Gets the last element or last `n` elements of an array. If a callback is
provided elements at the end of the array are returned as long as the
callback returns truey. The callback is bound to `thisArg` and invoked
with three arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[callback]` *(Function|Object|number|string)*: The function called per element or the number of elements to return. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the last element(s) of `array`.

#### Example
```js
_.last([1, 2, 3]);
// => 3

_.last([1, 2, 3], 2);
// => [2, 3]

_.last([1, 2, 3], function(num) {
  return num > 1;
});
// => [2, 3]

var characters = [
  { 'name': 'barney',  'blocked': false, 'employer': 'slate' },
  { 'name': 'fred',    'blocked': true,  'employer': 'slate' },
  { 'name': 'pebbles', 'blocked': true,  'employer': 'na' }
];

// using "_.pluck" callback shorthand
_.pluck(_.last(characters, 'blocked'), 'name');
// => ['fred', 'pebbles']

// using "_.where" callback shorthand
_.last(characters, { 'employer': 'na' });
// => [{ 'name': 'pebbles', 'blocked': true, 'employer': 'na' }]
```
* * *

### _.lastIndexOf(array, value, [fromIndex=array.length-1])

Gets the index at which the last occurrence of `value` is found using strict
equality for comparisons, i.e. `===`. If `fromIndex` is negative, it is used
as the offset from the end of the collection.
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to search.
2. `value` *(&#42;)*: The value to search for.
3. `[fromIndex=array.length-1]` *(number)*: The index to search from.

#### Returns
*(number)*:  Returns the index of the matched value or `-1`.

#### Example
```js
_.lastIndexOf([1, 2, 3, 1, 2, 3], 2);
// => 4

_.lastIndexOf([1, 2, 3, 1, 2, 3], 2, 3);
// => 1
```
* * *

### _.pull(array, [value])

Removes all provided values from the given array using strict equality for
comparisons, i.e. `===`.

#### Arguments
1. `array` *(Array)*: The array to modify.
2. `[value]` *(...&#42;)*: The values to remove.

#### Returns
*(Array)*:  Returns `array`.

#### Example
```js
var array = [1, 2, 3, 1, 2, 3];
_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```
* * *

### _.range([start=0], end, [step=1])

Creates an array of numbers (positive and/or negative) progressing from
`start` up to but not including `end`. If `start` is less than `stop` a
zero-length range is created unless a negative `step` is specified.

#### Arguments
1. `[start=0]` *(number)*: The start of the range.
2. `end` *(number)*: The end of the range.
3. `[step=1]` *(number)*: The value to increment or decrement by.

#### Returns
*(Array)*:  Returns a new range array.

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
* * *

### _.remove(array, [callback=identity], [thisArg])

Removes all elements from an array that the callback returns truey for
and returns an array of removed elements. The callback is bound to `thisArg`
and invoked with three arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to modify.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new array of removed elements.

#### Example
```js
var array = [1, 2, 3, 4, 5, 6];
var evens = _.remove(array, function(num) { return num % 2 == 0; });

console.log(array);
// => [1, 3, 5]

console.log(evens);
// => [2, 4, 6]
```
* * *

### _.rest(array, [callback=1], [thisArg])

The opposite of `_.initial` this method gets all but the first element or
first `n` elements of an array. If a callback function is provided elements
at the beginning of the array are excluded from the result as long as the
callback returns truey. The callback is bound to `thisArg` and invoked
with three arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Aliases
*_.drop, _.tail*

#### Arguments
1. `array` *(Array)*: The array to query.
2. `[callback=1]` *(Function|Object|number|string)*: The function called per element or the number of elements to exclude. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a slice of `array`.

#### Example
```js
_.rest([1, 2, 3]);
// => [2, 3]

_.rest([1, 2, 3], 2);
// => [3]

_.rest([1, 2, 3], function(num) {
  return num < 3;
});
// => [3]

var characters = [
  { 'name': 'barney',  'blocked': true,  'employer': 'slate' },
  { 'name': 'fred',    'blocked': false,  'employer': 'slate' },
  { 'name': 'pebbles', 'blocked': true, 'employer': 'na' }
];

// using "_.pluck" callback shorthand
_.pluck(_.rest(characters, 'blocked'), 'name');
// => ['fred', 'pebbles']

// using "_.where" callback shorthand
_.rest(characters, { 'employer': 'slate' });
// => [{ 'name': 'pebbles', 'blocked': true, 'employer': 'na' }]
```
* * *

### _.sortedIndex(array, value, [callback=identity], [thisArg])

Uses a binary search to determine the smallest index at which a value
should be inserted into a given sorted array in order to maintain the sort
order of the array. If a callback is provided it will be executed for
`value` and each element of `array` to compute their sort ranking. The
callback is bound to `thisArg` and invoked with one argument; (value).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `array` *(Array)*: The array to inspect.
2. `value` *(&#42;)*: The value to evaluate.
3. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(number)*:  Returns the index at which `value` should be inserted
into `array`.

#### Example
```js
_.sortedIndex([20, 30, 50], 40);
// => 2

// using "_.pluck" callback shorthand
_.sortedIndex([{ 'x': 20 }, { 'x': 30 }, { 'x': 50 }], { 'x': 40 }, 'x');
// => 2

var dict = {
  'wordToNumber': { 'twenty': 20, 'thirty': 30, 'fourty': 40, 'fifty': 50 }
};

_.sortedIndex(['twenty', 'thirty', 'fifty'], 'fourty', function(word) {
  return dict.wordToNumber[word];
});
// => 2

_.sortedIndex(['twenty', 'thirty', 'fifty'], 'fourty', function(word) {
  return this.wordToNumber[word];
}, dict);
// => 2
```
* * *

### _.union([array])

Creates an array of unique values, in order, of the provided arrays using
strict equality for comparisons, i.e. `===`.

#### Arguments
1. `[array]` *(...Array)*: The arrays to inspect.

#### Returns
*(Array)*:  Returns an array of combined values.

#### Example
```js
_.union([1, 2, 3], [5, 2, 1, 4], [2, 1]);
// => [1, 2, 3, 5, 4]
```
* * *

### _.uniq(array, [isSorted=false], [callback=identity], [thisArg])

Creates a duplicate-value-free version of an array using strict equality
for comparisons, i.e. `===`. If the array is sorted, providing
`true` for `isSorted` will use a faster algorithm. If a callback is provided
each element of `array` is passed through the callback before uniqueness
is computed. The callback is bound to `thisArg` and invoked with three
arguments; (value, index, array).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Aliases
*_.unique*

#### Arguments
1. `array` *(Array)*: The array to process.
2. `[isSorted=false]` *(boolean)*: A flag to indicate that `array` is sorted.
3. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a duplicate-value-free array.

#### Example
```js
_.uniq([1, 2, 1, 3, 1]);
// => [1, 2, 3]

_.uniq([1, 1, 2, 2, 3], true);
// => [1, 2, 3]

_.uniq(['A', 'b', 'C', 'a', 'B', 'c'], function(letter) { return letter.toLowerCase(); });
// => ['A', 'b', 'C']

_.uniq([1, 2.5, 3, 1.5, 2, 3.5], function(num) { return this.floor(num); }, Math);
// => [1, 2.5, 3]

// using "_.pluck" callback shorthand
_.uniq([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```
* * *

### _.without(array, [value])

Creates an array excluding all provided values using strict equality for
comparisons, i.e. `===`.

#### Arguments
1. `array` *(Array)*: The array to filter.
2. `[value]` *(...&#42;)*: The values to exclude.

#### Returns
*(Array)*:  Returns a new array of filtered values.

#### Example
```js
_.without([1, 2, 1, 0, 3, 1, 4], 0, 1);
// => [2, 3, 4]
```
* * *

### _.xor([array])

Creates an array that is the symmetric difference of the provided arrays.
See http://en.wikipedia.org/wiki/Symmetric_difference.

#### Arguments

1. `[array]` *(...Array)*: The arrays to inspect.

#### Returns

*(Array)*:  Returns an array of values.

#### Example

```js
_.xor([1, 2, 3], [5, 2, 1, 4]);
// => [3, 5, 4]

_.xor([1, 2, 5], [2, 3, 5], [3, 4, 5]);
// => [1, 4, 5]
```
* * *

### _.zip([array])

Creates an array of grouped elements, the first of which contains the first
elements of the given arrays, the second of which contains the second
elements of the given arrays, and so on.

#### Aliases

*_.unzip*

#### Arguments

1. `[array]` *(...Array)*: Arrays to process.

#### Returns

*(Array)*:  Returns a new array of grouped elements.

#### Example

```js
_.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]]
```
* * *

### _.zipObject(keys, [values=[]])

Creates an object composed from arrays of `keys` and `values`. Provide
either a single two dimensional array, i.e. `[[key1, value1], [key2, value2]]`
or two arrays, one of `keys` and one of corresponding `values`.

#### Aliases

*_.object*

#### Arguments

1. `keys` *(Array)*: The array of keys.
2. `[values=[]]` *(Array)*: The array of values.

#### Returns

*(Object)*:  Returns an object composed of the given keys and
corresponding values.

#### Example

```js
_.zipObject(['fred', 'barney'], [30, 40]);
// => { 'fred': 30, 'barney': 40 }
```
* * *
