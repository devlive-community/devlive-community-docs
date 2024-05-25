[TOC]

### _.compact(array)

Creates an array with all falsey values of `array` removed. The values `false`, `null`, `0`, `""`, `undefined` and `NaN` are all falsey.

#### Arguments

1. `array` *(Array)*: The array to compact.

#### Returns

*(Array)*: Returns a new filtered array.

#### Example

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

* * *

### _.difference(array [, array1, array2, ...])

Creates an array of `array` elements not present in the other arrays using strict equality for comparisons, i.e. `===`.

#### Arguments

1. `array` *(Array)*: The array to process.
2. `[array1, array2, ...]` *(Array)*: Arrays to check.

#### Returns

*(Array)*: Returns a new array of `array` elements not present in the  other arrays.

#### Example

```js
_.difference([1, 2, 3, 4, 5], [5, 2, 10]);
// => [1, 3, 4]
```

* * *

### _.findIndex(array [, callback=identity, thisArg])

This method is similar to `_.find`, except that it returns the index of the element that passes the callback check, instead of the element itself.

#### Arguments

1. `array` *(Array)*: The array to search.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the index of the found element, else `-1`.

#### Example

```js
_.findIndex(['apple', 'banana', 'beet'], function(food) {
  return /^b/.test(food);
});
// => 1
```

* * *

### _.first(array [, callback|n, thisArg])

Gets the first element of the `array`. If a number `n` is passed, the first `n` elements of the `array` are returned. If a `callback` function is passed, elements at the beginning of the array are returned as long as the `callback` returns truthy. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, array)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*head, take*

#### Arguments

1. `array` *(Array)*: The array to query.
2. `[callback|n]` *(Function|Object|Number|String)*: The function called per element or the number of elements to return. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the first element(s) of `array`.

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

var food = [
  { 'name': 'banana', 'organic': true },
  { 'name': 'beet',   'organic': false },
];

// using "_.pluck" callback shorthand
_.first(food, 'organic');
// => [{ 'name': 'banana', 'organic': true }]

var food = [
  { 'name': 'apple',  'type': 'fruit' },
  { 'name': 'banana', 'type': 'fruit' },
  { 'name': 'beet',   'type': 'vegetable' }
];

// using "_.where" callback shorthand
_.first(food, { 'type': 'fruit' });
// => [{ 'name': 'apple', 'type': 'fruit' }, { 'name': 'banana', 'type': 'fruit' }]
```

* * *

### _.flatten(array [, isShallow=false, callback=identity, thisArg])

Flattens a nested array *(the nesting can be to any depth)*. If `isShallow` is truthy, `array` will only be flattened a single level. If `callback` is passed, each element of `array` is passed through a `callback` before flattening. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, array)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `array` *(Array)*: The array to flatten.
2. `[isShallow=false]` *(Boolean)*: A flag to indicate only flattening a single level.
3. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a new flattened array.

#### Example

```js
_.flatten([1, [2], [3, [[4]]]]);
// => [1, 2, 3, 4];

_.flatten([1, [2], [3, [[4]]]], true);
// => [1, 2, 3, [[4]]];

var stooges = [
  { 'name': 'curly', 'quotes': ['Oh, a wise guy, eh?', 'Poifect!'] },
  { 'name': 'moe', 'quotes': ['Spread out!', 'You knucklehead!'] }
];

// using "_.pluck" callback shorthand
_.flatten(stooges, 'quotes');
// => ['Oh, a wise guy, eh?', 'Poifect!', 'Spread out!', 'You knucklehead!']
```

* * *

### _.indexOf(array, value [, fromIndex=0])

Gets the index at which the first occurrence of `value` is found using strict equality for comparisons, i.e. `===`. If the `array` is already sorted, passing `true` for `fromIndex` will run a faster binary search.

#### Arguments

1. `array` *(Array)*: The array to search.
2. `value` *(Mixed)*: The value to search for.
3. `[fromIndex=0]` *(Boolean|Number)*: The index to search from or `true` to perform a binary search on a sorted `array`.

#### Returns

*(Number)*: Returns the index of the matched value or `-1`.

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

### _.initial(array [, callback|n=1, thisArg])

Gets all but the last element of `array`. If a number `n` is passed, the last `n` elements are excluded from the result. If a `callback` function is passed, elements at the end of the array are excluded from the result as long as the `callback` returns truthy. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, array)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `array` *(Array)*: The array to query.
2. `[callback|n=1]` *(Function|Object|Number|String)*: The function called per element or the number of elements to exclude. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a slice of `array`.

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

var food = [
  { 'name': 'beet',   'organic': false },
  { 'name': 'carrot', 'organic': true }
];

// using "_.pluck" callback shorthand
_.initial(food, 'organic');
// => [{ 'name': 'beet',   'organic': false }]

var food = [
  { 'name': 'banana', 'type': 'fruit' },
  { 'name': 'beet',   'type': 'vegetable' },
  { 'name': 'carrot', 'type': 'vegetable' }
];

// using "_.where" callback shorthand
_.initial(food, { 'type': 'vegetable' });
// => [{ 'name': 'banana', 'type': 'fruit' }]
```

* * *

### _.intersection([array1, array2, ...])

Computes the intersection of all the passed-in arrays using strict equality for comparisons, i.e. `===`.

#### Arguments

1. `[array1, array2, ...]` *(Array)*: Arrays to process.

#### Returns

*(Array)*: Returns a new array of unique elements that are present  in **all** of the arrays.

#### Example

```js
_.intersection([1, 2, 3], [101, 2, 1, 10], [2, 1]);
// => [1, 2]
```

* * *

### _.last(array [, callback|n, thisArg])

Gets the last element of the `array`. If a number `n` is passed, the last `n` elements of the `array` are returned. If a `callback` function is passed, elements at the end of the array are returned as long as the `callback` returns truthy. The `callback` is bound to `thisArg` and invoked with three arguments;(value, index, array).

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `array` *(Array)*: The array to query.
2. `[callback|n]` *(Function|Object|Number|String)*: The function called per element or the number of elements to return. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the last element(s) of `array`.

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

var food = [
  { 'name': 'beet',   'organic': false },
  { 'name': 'carrot', 'organic': true }
];

// using "_.pluck" callback shorthand
_.last(food, 'organic');
// => [{ 'name': 'carrot', 'organic': true }]

var food = [
  { 'name': 'banana', 'type': 'fruit' },
  { 'name': 'beet',   'type': 'vegetable' },
  { 'name': 'carrot', 'type': 'vegetable' }
];

// using "_.where" callback shorthand
_.last(food, { 'type': 'vegetable' });
// => [{ 'name': 'beet', 'type': 'vegetable' }, { 'name': 'carrot', 'type': 'vegetable' }]
```

* * *

### _.lastIndexOf(array, value [, fromIndex=array.length-1])

Gets the index at which the last occurrence of `value` is found using strict equality for comparisons, i.e. `===`. If `fromIndex` is negative, it is used as the offset from the end of the collection.

#### Arguments

1. `array` *(Array)*: The array to search.
2. `value` *(Mixed)*: The value to search for.
3. `[fromIndex=array.length-1]` *(Number)*: The index to search from.

#### Returns

*(Number)*: Returns the index of the matched value or `-1`.

#### Example

```js
_.lastIndexOf([1, 2, 3, 1, 2, 3], 2);
// => 4

_.lastIndexOf([1, 2, 3, 1, 2, 3], 2, 3);
// => 1
```

* * *

### _.range([start=0], end [, step=1])

Creates an array of numbers *(positive and/or negative)* progressing from `start` up to but not including `end`.

#### Arguments

1. `[start=0]` *(Number)*: The start of the range.
2. `end` *(Number)*: The end of the range.
3. `[step=1]` *(Number)*: The value to increment or decrement by.

#### Returns

*(Array)*: Returns a new range array.

#### Example

```js
_.range(10);
// => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

_.range(1, 11);
// => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

_.range(0, 30, 5);
// => [0, 5, 10, 15, 20, 25]

_.range(0, -10, -1);
// => [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]

_.range(0);
// => []
```

* * *

### _.rest(array [, callback|n=1, thisArg])

The opposite of `_.initial`, this method gets all but the first value of `array`. If a number `n` is passed, the first `n` values are excluded from the result. If a `callback` function is passed, elements at the beginning of the array are excluded from the result as long as the `callback` returns truthy. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, array)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*drop, tail*

#### Arguments

1. `array` *(Array)*: The array to query.
2. `[callback|n=1]` *(Function|Object|Number|String)*: The function called per element or the number of elements to exclude. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a slice of `array`.

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

var food = [
  { 'name': 'banana', 'organic': true },
  { 'name': 'beet',   'organic': false },
];

// using "_.pluck" callback shorthand
_.rest(food, 'organic');
// => [{ 'name': 'beet', 'organic': false }]

var food = [
  { 'name': 'apple',  'type': 'fruit' },
  { 'name': 'banana', 'type': 'fruit' },
  { 'name': 'beet',   'type': 'vegetable' }
];

// using "_.where" callback shorthand
_.rest(food, { 'type': 'fruit' });
// => [{ 'name': 'beet', 'type': 'vegetable' }]
```

* * *

### _.sortedIndex(array, value [, callback=identity, thisArg])

Uses a binary search to determine the smallest index at which the `value` should be inserted into `array` in order to maintain the sort order of the sorted `array`. If `callback` is passed, it will be executed for `value` and each element in `array` to compute their sort ranking. The `callback` is bound to `thisArg` and invoked with one argument; *(value)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `array` *(Array)*: The array to inspect.
2. `value` *(Mixed)*: The value to evaluate.
3. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Number)*: Returns the index at which the value should be inserted  into `array`.

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

### _.union([array1, array2, ...])

Computes the union of the passed-in arrays using strict equality for comparisons, i.e. `===`.

#### Arguments

1. `[array1, array2, ...]` *(Array)*: Arrays to process.

#### Returns

*(Array)*: Returns a new array of unique values, in order, that are  present in one or more of the arrays.

#### Example

```js
_.union([1, 2, 3], [101, 2, 1, 10], [2, 1]);
// => [1, 2, 3, 101, 10]
```

* * *

### _.uniq(array [, isSorted=false, callback=identity, thisArg])

Creates a duplicate-value-free version of the `array` using strict equality for comparisons, i.e. `===`. If the `array` is already sorted, passing `true` for `isSorted` will run a faster algorithm. If `callback` is passed, each element of `array` is passed through the `callback` before uniqueness is computed. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, array)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*unique*

#### Arguments

1. `array` *(Array)*: The array to process.
2. `[isSorted=false]` *(Boolean)*: A flag to indicate that the `array` is already sorted.
3. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a duplicate-value-free array.

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

### _.unzip(array)

The inverse of `_.zip`, this method splits groups of elements into arrays composed of elements from each group at their corresponding indexes.

#### Arguments

1. `array` *(Array)*: The array to process.

#### Returns

*(Array)*: Returns a new array of the composed arrays.

#### Example

```js
_.unzip([['moe', 30, true], ['larry', 40, false]]);
// => [['moe', 'larry'], [30, 40], [true, false]];
```

* * *

### _.without(array [, value1, value2, ...])

Creates an array with all occurrences of the passed values removed using strict equality for comparisons, i.e. `===`.

#### Arguments

1. `array` *(Array)*: The array to filter.
2. `[value1, value2, ...]` *(Mixed)*: Values to remove.

#### Returns

*(Array)*: Returns a new filtered array.

#### Example

```js
_.without([1, 2, 1, 0, 3, 1, 4], 0, 1);
// => [2, 3, 4]
```

* * *

### _.zip([array1, array2, ...])

Groups the elements of each array at their corresponding indexes. Useful for separate data sources that are coordinated through matching array indexes. For a matrix of nested arrays, `_.zip.apply(...)` can transpose the matrix in a similar fashion.

#### Arguments

1. `[array1, array2, ...]` *(Array)*: Arrays to process.

#### Returns

*(Array)*: Returns a new array of grouped elements.

#### Example

```js
_.zip(['moe', 'larry'], [30, 40], [true, false]);
// => [['moe', 30, true], ['larry', 40, false]]
```

* * *

### _.zipObject(keys [, values=[]])

Creates an object composed from arrays of `keys` and `values`. Pass either a single two dimensional array, i.e. `[[key1, value1], [key2, value2]]`, or two arrays, one of `keys` and one of corresponding `values`.

#### Aliases

*object*

#### Arguments

1. `keys` *(Array)*: The array of keys.
2. `[values=[]]` *(Array)*: The array of values.

#### Returns

*(Object)*: Returns an object composed of the given keys and  corresponding values.

#### Example

```js
_.zipObject(['moe', 'larry'], [30, 40]);
// => { 'moe': 30, 'larry': 40 }
```

* * *
