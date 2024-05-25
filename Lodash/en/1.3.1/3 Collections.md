[TOC]

### _.at(collection [, index1, index2, ...])

Creates an array of elements from the specified indexes, or keys, of the `collection`. Indexes may be specified as individual arguments or as arrays of indexes.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[index1, index2, ...]` *(Array|Number|String)*: The indexes of `collection` to retrieve, either as individual arguments or arrays.

#### Returns

*(Array)*: Returns a new array of elements corresponding to the  provided indexes.

#### Example

```js
_.at(['a', 'b', 'c', 'd', 'e'], [0, 2, 4]);
// => ['a', 'c', 'e']

_.at(['moe', 'larry', 'curly'], 0, 2);
// => ['moe', 'curly']
```

* * *

### _.contains(collection, target [, fromIndex=0])

Checks if a given `target` element is present in a `collection` using strict equality for comparisons, i.e. `===`. If `fromIndex` is negative, it is used as the offset from the end of the collection.

#### Aliases

*include*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `target` *(Mixed)*: The value to check for.
3. `[fromIndex=0]` *(Number)*: The index to search from.

#### Returns

*(Boolean)*: Returns `true` if the `target` element is found, else `false`.

#### Example

```js
_.contains([1, 2, 3], 1);
// => true

_.contains([1, 2, 3], 1, 2);
// => false

_.contains({ 'name': 'moe', 'age': 40 }, 'moe');
// => true

_.contains('curly', 'ur');
// => true
```

* * *

### _.countBy(collection [, callback=identity, thisArg])

Creates an object composed of keys returned from running each element of the `collection` through the given `callback`. The corresponding value of each key is the number of times the key was returned by the `callback`. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns the composed aggregate object.

#### Example

```js
_.countBy([4.3, 6.1, 6.4], function(num) { return Math.floor(num); });
// => { '4': 1, '6': 2 }

_.countBy([4.3, 6.1, 6.4], function(num) { return this.floor(num); }, Math);
// => { '4': 1, '6': 2 }

_.countBy(['one', 'two', 'three'], 'length');
// => { '3': 2, '5': 1 }
```

* * *

### _.every(collection [, callback=identity, thisArg])

Checks if the `callback` returns a truthy value for **all** elements of a `collection`. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*all*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Boolean)*: Returns `true` if all elements pass the callback check,  else `false`.

#### Example

```js
_.every([true, 1, null, 'yes'], Boolean);
// => false

var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

// using "_.pluck" callback shorthand
_.every(stooges, 'age');
// => true

// using "_.where" callback shorthand
_.every(stooges, { 'age': 50 });
// => false
```

* * *

### _.filter(collection [, callback=identity, thisArg])

Examines each element in a `collection`, returning an array of all elements the `callback` returns truthy for. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*select*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a new array of elements that passed the callback check.

#### Example

```js
var evens = _.filter([1, 2, 3, 4, 5, 6], function(num) { return num % 2 == 0; });
// => [2, 4, 6]

var food = [
  { 'name': 'apple',  'organic': false, 'type': 'fruit' },
  { 'name': 'carrot', 'organic': true,  'type': 'vegetable' }
];

// using "_.pluck" callback shorthand
_.filter(food, 'organic');
// => [{ 'name': 'carrot', 'organic': true, 'type': 'vegetable' }]

// using "_.where" callback shorthand
_.filter(food, { 'type': 'fruit' });
// => [{ 'name': 'apple', 'organic': false, 'type': 'fruit' }]
```

* * *

### _.find(collection [, callback=identity, thisArg])

Examines each element in a `collection`, returning the first that the `callback` returns truthy for. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*detect, findWhere*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the found element, else `undefined`.

#### Example

```js
_.find([1, 2, 3, 4], function(num) {
  return num % 2 == 0;
});
// => 2

var food = [
  { 'name': 'apple',  'organic': false, 'type': 'fruit' },
  { 'name': 'banana', 'organic': true,  'type': 'fruit' },
  { 'name': 'beet',   'organic': false, 'type': 'vegetable' }
];

// using "_.where" callback shorthand
_.find(food, { 'type': 'vegetable' });
// => { 'name': 'beet', 'organic': false, 'type': 'vegetable' }

// using "_.pluck" callback shorthand
_.find(food, 'organic');
// => { 'name': 'banana', 'organic': true, 'type': 'fruit' }
```

* * *

### _.forEach(collection [, callback=identity, thisArg])

Iterates over a `collection`, executing the `callback` for each element in the `collection`. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*. Callbacks may exit iteration early by explicitly returning `false`.

#### Aliases

*each*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array, Object, String)*: Returns `collection`.

#### Example

```js
_([1, 2, 3]).forEach(alert).join(',');
// => alerts each number and returns '1,2,3'

_.forEach({ 'one': 1, 'two': 2, 'three': 3 }, alert);
// => alerts each number value (order is not guaranteed)
```

* * *

### _.groupBy(collection [, callback=identity, thisArg])

Creates an object composed of keys returned from running each element of the `collection` through the `callback`. The corresponding value of each key is an array of elements passed to `callback` that returned the key. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns the composed aggregate object.

#### Example

```js
_.groupBy([4.2, 6.1, 6.4], function(num) { return Math.floor(num); });
// => { '4': [4.2], '6': [6.1, 6.4] }

_.groupBy([4.2, 6.1, 6.4], function(num) { return this.floor(num); }, Math);
// => { '4': [4.2], '6': [6.1, 6.4] }

// using "_.pluck" callback shorthand
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

* * *

### _.invoke(collection, methodName [, arg1, arg2, ...])

Invokes the method named by `methodName` on each element in the `collection`, returning an array of the results of each invoked method. Additional arguments will be passed to each invoked method. If `methodName` is a function, it will be invoked for, and `this` bound to, each element in the `collection`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `methodName` *(Function|String)*: The name of the method to invoke or the function invoked per iteration.
3. `[arg1, arg2, ...]` *(Mixed)*: Arguments to invoke the method with.

#### Returns

*(Array)*: Returns a new array of the results of each invoked method.

#### Example

```js
_.invoke([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invoke([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

* * *

### _.map(collection [, callback=identity, thisArg])

Creates an array of values by running each element in the `collection` through the `callback`. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*collect*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a new array of the results of each `callback` execution.

#### Example

```js
_.map([1, 2, 3], function(num) { return num * 3; });
// => [3, 6, 9]

_.map({ 'one': 1, 'two': 2, 'three': 3 }, function(num) { return num * 3; });
// => [3, 6, 9] (order is not guaranteed)

var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

// using "_.pluck" callback shorthand
_.map(stooges, 'name');
// => ['moe', 'larry']
```

* * *

### _.max(collection [, callback=identity, thisArg])

Retrieves the maximum value of an `array`. If `callback` is passed, it will be executed for each value in the `array` to generate the criterion by which the value is ranked. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the maximum value.

#### Example

```js
_.max([4, 2, 8, 6]);
// => 8

var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

_.max(stooges, function(stooge) { return stooge.age; });
// => { 'name': 'larry', 'age': 50 };

// using "_.pluck" callback shorthand
_.max(stooges, 'age');
// => { 'name': 'larry', 'age': 50 };
```

* * *

### _.min(collection [, callback=identity, thisArg])

Retrieves the minimum value of an `array`. If `callback` is passed, it will be executed for each value in the `array` to generate the criterion by which the value is ranked. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the minimum value.

#### Example

```js
_.min([4, 2, 8, 6]);
// => 2

var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

_.min(stooges, function(stooge) { return stooge.age; });
// => { 'name': 'moe', 'age': 40 };

// using "_.pluck" callback shorthand
_.min(stooges, 'age');
// => { 'name': 'moe', 'age': 40 };
```

* * *

### _.pluck(collection, property)

Retrieves the value of a specified property from all elements in the `collection`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `property` *(String)*: The property to pluck.

#### Returns

*(Array)*: Returns a new array of property values.

#### Example

```js
var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

_.pluck(stooges, 'name');
// => ['moe', 'larry']
```

* * *

### _.reduce(collection [, callback=identity, accumulator, thisArg])

Reduces a `collection` to a value which is the accumulated result of running each element in the `collection` through the `callback`, where each successive `callback` execution consumes the return value of the previous execution. If `accumulator` is not passed, the first element of the `collection` will be used as the initial `accumulator` value. The `callback` is bound to `thisArg` and invoked with four arguments; *(accumulator, value, index|key, collection)*.

#### Aliases

*foldl, inject*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[accumulator]` *(Mixed)*: Initial value of the accumulator.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the accumulated value.

#### Example

```js
var sum = _.reduce([1, 2, 3], function(sum, num) {
  return sum + num;
});
// => 6

var mapped = _.reduce({ 'a': 1, 'b': 2, 'c': 3 }, function(result, num, key) {
  result[key] = num * 3;
  return result;
}, {});
// => { 'a': 3, 'b': 6, 'c': 9 }
```

* * *

### _.reduceRight(collection [, callback=identity, accumulator, thisArg])

This method is similar to `_.reduce`, except that it iterates over a `collection` from right to left.

#### Aliases

*foldr*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[accumulator]` *(Mixed)*: Initial value of the accumulator.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the accumulated value.

#### Example

```js
var list = [[0, 1], [2, 3], [4, 5]];
var flat = _.reduceRight(list, function(a, b) { return a.concat(b); }, []);
// => [4, 5, 2, 3, 0, 1]
```

* * *

### _.reject(collection [, callback=identity, thisArg])

The opposite of `_.filter`, this method returns the elements of a `collection` that `callback` does **not** return truthy for.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a new array of elements that did **not** pass the  callback check.

#### Example

```js
var odds = _.reject([1, 2, 3, 4, 5, 6], function(num) { return num % 2 == 0; });
// => [1, 3, 5]

var food = [
  { 'name': 'apple',  'organic': false, 'type': 'fruit' },
  { 'name': 'carrot', 'organic': true,  'type': 'vegetable' }
];

// using "_.pluck" callback shorthand
_.reject(food, 'organic');
// => [{ 'name': 'apple', 'organic': false, 'type': 'fruit' }]

// using "_.where" callback shorthand
_.reject(food, { 'type': 'fruit' });
// => [{ 'name': 'carrot', 'organic': true, 'type': 'vegetable' }]
```

* * *

### _.shuffle(collection)

Creates an array of shuffled `array` values, using a version of the Fisher-Yates shuffle. See http://en.wikipedia.org/wiki/Fisher-Yates_shuffle.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to shuffle.

#### Returns

*(Array)*: Returns a new shuffled collection.

#### Example

```js
_.shuffle([1, 2, 3, 4, 5, 6]);
// => [4, 1, 6, 3, 5, 2]
```

* * *

### _.size(collection)

Gets the size of the `collection` by returning `collection.length` for arrays and array-like objects or the number of own enumerable properties for objects.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to inspect.

#### Returns

*(Number)*: Returns `collection.length` or number of own enumerable properties.

#### Example

```js
_.size([1, 2]);
// => 2

_.size({ 'one': 1, 'two': 2, 'three': 3 });
// => 3

_.size('curly');
// => 5
```

* * *

### _.some(collection [, callback=identity, thisArg])

Checks if the `callback` returns a truthy value for **any** element of a `collection`. The function returns as soon as it finds passing value, and does not iterate over the entire `collection`. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Aliases

*any*

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns
*(Boolean)*: Returns `true` if any element passes the callback check,  else `false`.

#### Example

```js
_.some([null, 0, 'yes', false], Boolean);
// => true

var food = [
  { 'name': 'apple',  'organic': false, 'type': 'fruit' },
  { 'name': 'carrot', 'organic': true,  'type': 'vegetable' }
];

// using "_.pluck" callback shorthand
_.some(food, 'organic');
// => true

// using "_.where" callback shorthand
_.some(food, { 'type': 'meat' });
// => false
```

* * *

### _.sortBy(collection [, callback=identity, thisArg])

Creates an array of elements, sorted in ascending order by the results of running each element in the `collection` through the `callback`. This method performs a stable sort, that is, it will preserve the original sort order of equal elements. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, index|key, collection)*.

If a property name is passed for `callback`, the created "_.pluck" style callback will return the property value of the given element.

If an object is passed for `callback`, the created "_.where" style callback will return `true` for elements that have the properties of the given object, else `false`.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a new array of sorted elements.

#### Example

```js
_.sortBy([1, 2, 3], function(num) { return Math.sin(num); });
// => [3, 1, 2]

_.sortBy([1, 2, 3], function(num) { return this.sin(num); }, Math);
// => [3, 1, 2]

// using "_.pluck" callback shorthand
_.sortBy(['banana', 'strawberry', 'apple'], 'length');
// => ['apple', 'banana', 'strawberry']
```

* * *

### _.toArray(collection)

Converts the `collection` to an array.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to convert.

#### Returns

*(Array)*: Returns the new converted array.

#### Example

```js
(function() { return _.toArray(arguments).slice(1); })(1, 2, 3, 4);
// => [2, 3, 4]
```

* * *

### _.where(collection, properties)

Examines each element in a `collection`, returning an array of all elements that have the given `properties`. When checking `properties`, this method performs a deep comparison between values to determine if they are equivalent to each other.

#### Arguments

1. `collection` *(Array|Object|String)*: The collection to iterate over.
2. `properties` *(Object)*: The object of property values to filter by.

#### Returns

*(Array)*: Returns a new array of elements that have the given `properties`.

#### Example

```js
var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

_.where(stooges, { 'age': 40 });
// => [{ 'name': 'moe', 'age': 40 }]
```
