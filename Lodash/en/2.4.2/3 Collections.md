[TOC]

### _.at(collection, [index])

Creates an array of elements from the specified indexes, or keys, of the
`collection`. Indexes may be specified as individual arguments or as arrays
of indexes.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[index]` *(...(number|number&#91;&#93;|string|string&#91;&#93;)*: The indexes of `collection` to retrieve, specified as individual indexes or arrays of indexes.

#### Returns
*(Array)*:  Returns a new array of elements corresponding to the
provided indexes.

#### Example
```js
_.at(['a', 'b', 'c', 'd', 'e'], [0, 2, 4]);
// => ['a', 'c', 'e']

_.at(['fred', 'barney', 'pebbles'], 0, 2);
// => ['fred', 'pebbles']
```
* * *

### _.contains(collection, target, [fromIndex=0])

Checks if a given value is present in a collection using strict equality
for comparisons, i.e. `===`. If `fromIndex` is negative, it is used as the
offset from the end of the collection.

#### Aliases
*_.include*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `target` *(&#42;)*: The value to check for.
3. `[fromIndex=0]` *(number)*: The index to search from.

#### Returns
*(boolean)*:  Returns `true` if the `target` element is found, else `false`.

#### Example
```js
_.contains([1, 2, 3], 1);
// => true

_.contains([1, 2, 3], 1, 2);
// => false

_.contains({ 'name': 'fred', 'age': 40 }, 'fred');
// => true

_.contains('pebbles', 'eb');
// => true
```
* * *

### _.countBy(collection, [callback=identity], [thisArg])

Creates an object composed of keys generated from the results of running
each element of `collection` through the callback. The corresponding value
of each key is the number of times the key was returned by the callback.
The callback is bound to `thisArg` and invoked with three arguments;
(value, index|key, collection).
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
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns the composed aggregate object.

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

### _.every(collection, [callback=identity], [thisArg])

Checks if the given callback returns truey value for **all** elements of
a collection. The callback is bound to `thisArg` and invoked with three
arguments; (value, index|key, collection).
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
*_.all*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(boolean)*:  Returns `true` if all elements passed the callback check,
else `false`.

#### Example
```js
_.every([true, 1, null, 'yes']);
// => false

var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

// using "_.pluck" callback shorthand
_.every(characters, 'age');
// => true

// using "_.where" callback shorthand
_.every(characters, { 'age': 36 });
// => false
```
* * *

### _.filter(collection, [callback=identity], [thisArg])

Iterates over elements of a collection, returning an array of all elements
the callback returns truey for. The callback is bound to `thisArg` and
invoked with three arguments; (value, index|key, collection).
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
*_.select*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new array of elements that passed the callback check.

#### Example
```js
var evens = _.filter([1, 2, 3, 4, 5, 6], function(num) { return num % 2 == 0; });
// => [2, 4, 6]

var characters = [
  { 'name': 'barney', 'age': 36, 'blocked': false },
  { 'name': 'fred',   'age': 40, 'blocked': true }
];

// using "_.pluck" callback shorthand
_.filter(characters, 'blocked');
// => [{ 'name': 'fred', 'age': 40, 'blocked': true }]

// using "_.where" callback shorthand
_.filter(characters, { 'age': 36 });
// => [{ 'name': 'barney', 'age': 36, 'blocked': false }]
```
* * *

### _.find(collection, [callback=identity], [thisArg])

Iterates over elements of a collection, returning the first element that
the callback returns truey for. The callback is bound to `thisArg` and
invoked with three arguments; (value, index|key, collection).
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
*_.detect, _.findWhere*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the found element, else `undefined`.

#### Example
```js
var characters = [
  { 'name': 'barney',  'age': 36, 'blocked': false },
  { 'name': 'fred',    'age': 40, 'blocked': true },
  { 'name': 'pebbles', 'age': 1,  'blocked': false }
];

_.find(characters, function(chr) {
  return chr.age < 40;
});
// => { 'name': 'barney', 'age': 36, 'blocked': false }

// using "_.where" callback shorthand
_.find(characters, { 'age': 1 });
// =>  { 'name': 'pebbles', 'age': 1, 'blocked': false }

// using "_.pluck" callback shorthand
_.find(characters, 'blocked');
// => { 'name': 'fred', 'age': 40, 'blocked': true }
```
* * *

### _.findLast(collection, [callback=identity], [thisArg])

This method is like `_.find` except that it iterates over elements
of a `collection` from right to left.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the found element, else `undefined`.

#### Example
```js
_.findLast([1, 2, 3, 4], function(num) {
  return num % 2 == 1;
});
// => 3
```
* * *

### _.forEach(collection, [callback=identity], [thisArg])

Iterates over elements of a collection, executing the callback for each
element. The callback is bound to `thisArg` and invoked with three arguments;
(value, index|key, collection). Callbacks may exit iteration early by
explicitly returning `false`.
<br>
<br>
Note: As with other "Collections" methods, objects with a `length` property
are iterated like arrays. To avoid this behavior `_.forIn` or `_.forOwn`
may be used for object iteration.

#### Aliases
*_.each*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array|Object|string)*:  Returns `collection`.

#### Example
```js
_([1, 2, 3]).forEach(function(num) { console.log(num); }).join(',');
// => logs each number and returns '1,2,3'

_.forEach({ 'one': 1, 'two': 2, 'three': 3 }, function(num) { console.log(num); });
// => logs each number and returns the object (property order is not guaranteed across environments)
```
* * *

### _.forEachRight(collection, [callback=identity], [thisArg])

This method is like `_.forEach` except that it iterates over elements
of a `collection` from right to left.

#### Aliases
*_.eachRight*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array|Object|string)*:  Returns `collection`.

#### Example
```js
_([1, 2, 3]).forEachRight(function(num) { console.log(num); }).join(',');
// => logs each number from right to left and returns '3,2,1'
```
* * *

### _.groupBy(collection, [callback=identity], [thisArg])

Creates an object composed of keys generated from the results of running
each element of a collection through the callback. The corresponding value
of each key is an array of the elements responsible for generating the key.
The callback is bound to `thisArg` and invoked with three arguments;
(value, index|key, collection).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns the composed aggregate object.

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

### _.indexBy(collection, [callback=identity], [thisArg])

Creates an object composed of keys generated from the results of running
each element of the collection through the given callback. The corresponding
value of each key is the last element responsible for generating the key.
The callback is bound to `thisArg` and invoked with three arguments;
(value, index|key, collection).
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
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns the composed aggregate object.

#### Example
```js
var keys = [
  { 'dir': 'left', 'code': 97 },
  { 'dir': 'right', 'code': 100 }
];

_.indexBy(keys, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }

_.indexBy(keys, function(key) { return String.fromCharCode(key.code); });
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }

_.indexBy(characters, function(key) { this.fromCharCode(key.code); }, String);
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }
```
* * *

### _.invoke(collection, methodName, [arg])

Invokes the method named by `methodName` on each element in the `collection`
returning an array of the results of each invoked method. Additional arguments
will be provided to each invoked method. If `methodName` is a function it
will be invoked for, and `this` bound to, each element in the `collection`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `methodName` *(Function|string)*: The name of the method to invoke or the function invoked per iteration.
3. `[arg]` *(...&#42;)*: Arguments to invoke the method with.

#### Returns
*(Array)*:  Returns a new array of the results of each invoked method.

#### Example
```js
_.invoke([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]

_.invoke([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```
* * *

### _.map(collection, [callback=identity], [thisArg])

Creates an array of values by running each element in the collection
through the callback. The callback is bound to `thisArg` and invoked with
three arguments; (value, index|key, collection).
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
*_.collect*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new array of the results of each `callback` execution.

#### Example
```js
_.map([1, 2, 3], function(num) { return num * 3; });
// => [3, 6, 9]

_.map({ 'one': 1, 'two': 2, 'three': 3 }, function(num) { return num * 3; });
// => [3, 6, 9] (property order is not guaranteed across environments)

var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

// using "_.pluck" callback shorthand
_.map(characters, 'name');
// => ['barney', 'fred']
```
* * *

### _.max(collection, [callback=identity], [thisArg])

Retrieves the maximum value of a collection. If the collection is empty or
falsey `-Infinity` is returned. If a callback is provided it will be executed
for each value in the collection to generate the criterion by which the value
is ranked. The callback is bound to `thisArg` and invoked with three
arguments; (value, index, collection).
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
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the maximum value.

#### Example
```js
_.max([4, 2, 8, 6]);
// => 8

var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

_.max(characters, function(chr) { return chr.age; });
// => { 'name': 'fred', 'age': 40 };

// using "_.pluck" callback shorthand
_.max(characters, 'age');
// => { 'name': 'fred', 'age': 40 };
```
* * *

### _.min(collection, [callback=identity], [thisArg])

Retrieves the minimum value of a collection. If the collection is empty or
falsey `Infinity` is returned. If a callback is provided it will be executed
for each value in the collection to generate the criterion by which the value
is ranked. The callback is bound to `thisArg` and invoked with three
arguments; (value, index, collection).
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
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the minimum value.

#### Example
```js
_.min([4, 2, 8, 6]);
// => 2

var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

_.min(characters, function(chr) { return chr.age; });
// => { 'name': 'barney', 'age': 36 };

// using "_.pluck" callback shorthand
_.min(characters, 'age');
// => { 'name': 'barney', 'age': 36 };
```
* * *

### _.pluck(collection, property)

Retrieves the value of a specified property from all elements in the collection.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `property` *(string)*: The name of the property to pluck.

#### Returns
*(Array)*:  Returns a new array of property values.

#### Example
```js
var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

_.pluck(characters, 'name');
// => ['barney', 'fred']
```
* * *

### _.reduce(collection, [callback=identity], [accumulator], [thisArg])

Reduces a collection to a value which is the accumulated result of running
each element in the collection through the callback, where each successive
callback execution consumes the return value of the previous execution. If
`accumulator` is not provided the first element of the collection will be
used as the initial `accumulator` value. The callback is bound to `thisArg`
and invoked with four arguments; (accumulator, value, index|key, collection).

#### Aliases
*_.foldl, _.inject*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[accumulator]` *(&#42;)*: Initial value of the accumulator.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the accumulated value.

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

### _.reduceRight(collection, [callback=identity], [accumulator], [thisArg])

This method is like `_.reduce` except that it iterates over elements
of a `collection` from right to left.

#### Aliases
*_.foldr*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[accumulator]` *(&#42;)*: Initial value of the accumulator.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the accumulated value.

#### Example
```js
var list = [[0, 1], [2, 3], [4, 5]];
var flat = _.reduceRight(list, function(a, b) { return a.concat(b); }, []);
// => [4, 5, 2, 3, 0, 1]
```
* * *

### _.reject(collection, [callback=identity], [thisArg])

The opposite of `_.filter` this method returns the elements of a
collection that the callback does **not** return truey for.
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
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new array of elements that failed the callback check.

#### Example
```js
var odds = _.reject([1, 2, 3, 4, 5, 6], function(num) { return num % 2 == 0; });
// => [1, 3, 5]

var characters = [
  { 'name': 'barney', 'age': 36, 'blocked': false },
  { 'name': 'fred',   'age': 40, 'blocked': true }
];

// using "_.pluck" callback shorthand
_.reject(characters, 'blocked');
// => [{ 'name': 'barney', 'age': 36, 'blocked': false }]

// using "_.where" callback shorthand
_.reject(characters, { 'age': 36 });
// => [{ 'name': 'fred', 'age': 40, 'blocked': true }]
```
* * *

### _.sample(collection, [n])

Retrieves a random element or `n` random elements from a collection.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to sample.
2. `[n]` *(number)*: The number of elements to sample.

#### Returns
*(Array)*:  Returns the random sample(s) of `collection`.

#### Example
```js
_.sample([1, 2, 3, 4]);
// => 2

_.sample([1, 2, 3, 4], 2);
// => [3, 1]
```
* * *

### _.shuffle(collection)

Creates an array of shuffled values, using a version of the Fisher-Yates
shuffle. See http://en.wikipedia.org/wiki/Fisher-Yates_shuffle.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to shuffle.

#### Returns
*(Array)*:  Returns a new shuffled collection.

#### Example
```js
_.shuffle([1, 2, 3, 4, 5, 6]);
// => [4, 1, 6, 3, 5, 2]
```
* * *

### _.size(collection)

Gets the size of the `collection` by returning `collection.length` for arrays
and array-like objects or the number of own enumerable properties for objects.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to inspect.

#### Returns
*(number)*:  Returns `collection.length` or number of own enumerable properties.

#### Example
```js
_.size([1, 2]);
// => 2

_.size({ 'one': 1, 'two': 2, 'three': 3 });
// => 3

_.size('pebbles');
// => 7
```
* * *

### _.some(collection, [callback=identity], [thisArg])

Checks if the callback returns a truey value for **any** element of a
collection. The function returns as soon as it finds a passing value and
does not iterate over the entire collection. The callback is bound to
`thisArg` and invoked with three arguments; (value, index|key, collection).
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
*_.any*

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(boolean)*:  Returns `true` if any element passed the callback check,
else `false`.

#### Example
```js
_.some([null, 0, 'yes', false], Boolean);
// => true

var characters = [
  { 'name': 'barney', 'age': 36, 'blocked': false },
  { 'name': 'fred',   'age': 40, 'blocked': true }
];

// using "_.pluck" callback shorthand
_.some(characters, 'blocked');
// => true

// using "_.where" callback shorthand
_.some(characters, { 'age': 1 });
// => false
```
* * *

### _.sortBy(collection, [callback=identity], [thisArg])

Creates an array of elements, sorted in ascending order by the results of
running each element in a collection through the callback. This method
performs a stable sort, that is, it will preserve the original sort order
of equal elements. The callback is bound to `thisArg` and invoked with
three arguments; (value, index|key, collection).
<br>
<br>
If a property name is provided for `callback` the created "_.pluck" style
callback will return the property value of the given element.
<br>
<br>
If an array of property names is provided for `callback` the collection
will be sorted by each property value.
<br>
<br>
If an object is provided for `callback` the created "_.where" style callback
will return `true` for elements that have the properties of the given object,
else `false`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[callback=identity]` *(Array|Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new array of sorted elements.

#### Example
```js
_.sortBy([1, 2, 3], function(num) { return Math.sin(num); });
// => [3, 1, 2]

_.sortBy([1, 2, 3], function(num) { return this.sin(num); }, Math);
// => [3, 1, 2]

var characters = [
  { 'name': 'barney',  'age': 36 },
  { 'name': 'fred',    'age': 40 },
  { 'name': 'barney',  'age': 26 },
  { 'name': 'fred',    'age': 30 }
];

// using "_.pluck" callback shorthand
_.map(_.sortBy(characters, 'age'), _.values);
// => [['barney', 26], ['fred', 30], ['barney', 36], ['fred', 40]]

// sorting by multiple properties
_.map(_.sortBy(characters, ['name', 'age']), _.values);
// = > [['barney', 26], ['barney', 36], ['fred', 30], ['fred', 40]]
```
* * *

### _.toArray(collection)

Converts the `collection` to an array.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to convert.

#### Returns
*(Array)*:  Returns the new converted array.

#### Example
```js
(function() { return _.toArray(arguments).slice(1); })(1, 2, 3, 4);
// => [2, 3, 4]
```
* * *

### _.where(collection, props)

Performs a deep comparison of each element in a `collection` to the given
`properties` object, returning an array of all elements that have equivalent
property values.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `props` *(Object)*: The object of property values to filter by.

#### Returns
*(Array)*:  Returns a new array of elements that have the given properties.

#### Example
```js
var characters = [
  { 'name': 'barney', 'age': 36, 'pets': ['hoppy'] },
  { 'name': 'fred',   'age': 40, 'pets': ['baby puss', 'dino'] }
];

_.where(characters, { 'age': 36 });
// => [{ 'name': 'barney', 'age': 36, 'pets': ['hoppy'] }]

_.where(characters, { 'pets': ['dino'] });
// => [{ 'name': 'fred', 'age': 40, 'pets': ['baby puss', 'dino'] }]
```
* * *
