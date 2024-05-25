[TOC]

### _.assign(object [, source1, source2, ..., callback, thisArg])

Assigns own enumerable properties of source object(s) to the destination object. Subsequent sources will overwrite property assignments of previous sources. If a `callback` function is passed, it will be executed to produce the assigned values. The `callback` is bound to `thisArg` and invoked with two arguments; *(objectValue, sourceValue)*.

#### Aliases

*extend*

#### Arguments

1. `object` *(Object)*: The destination object.
2. `[source1, source2, ...]` *(Object)*: The source objects.
3. `[callback]` *(Function)*: The function to customize assigning values.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns the destination object.

#### Example

```js
_.assign({ 'name': 'moe' }, { 'age': 40 });
// => { 'name': 'moe', 'age': 40 }

var defaults = _.partialRight(_.assign, function(a, b) {
  return typeof a == 'undefined' ? b : a;
});

var food = { 'name': 'apple' };
defaults(food, { 'name': 'banana', 'type': 'fruit' });
// => { 'name': 'apple', 'type': 'fruit' }
```

* * *

### _.clone(value [, deep=false, callback, thisArg])

Creates a clone of `value`. If `deep` is `true`, nested objects will also be cloned, otherwise they will be assigned by reference. If a `callback` function is passed, it will be executed to produce the cloned values. If `callback` returns `undefined`, cloning will be handled by the method instead. The `callback` is bound to `thisArg` and invoked with one argument; *(value)*.

#### Arguments

1. `value` *(Mixed)*: The value to clone.
2. `[deep=false]` *(Boolean)*: A flag to indicate a deep clone.
3. `[callback]` *(Function)*: The function to customize cloning values.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the cloned `value`.

#### Example

```js
var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

var shallow = _.clone(stooges);
shallow[0] === stooges[0];
// => true

var deep = _.clone(stooges, true);
deep[0] === stooges[0];
// => false

_.mixin({
  'clone': _.partialRight(_.clone, function(value) {
    return _.isElement(value) ? value.cloneNode(false) : undefined;
  })
});

var clone = _.clone(document.body);
clone.childNodes.length;
// => 0
```

* * *

### _.cloneDeep(value [, callback, thisArg])

Creates a deep clone of `value`. If a `callback` function is passed, it will be executed to produce the cloned values. If `callback` returns `undefined`, cloning will be handled by the method instead. The `callback` is bound to `thisArg` and invoked with one argument; *(value)*.

Note: This method is loosely based on the structured clone algorithm. Functions and DOM nodes are **not** cloned. The enumerable properties of `arguments` objects and objects created by constructors other than `Object` are cloned to plain `Object` objects. See http://www.w3.org/TR/html5/infrastructure.html#internal-structured-cloning-algorithm.

#### Arguments

1. `value` *(Mixed)*: The value to deep clone.
2. `[callback]` *(Function)*: The function to customize cloning values.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the deep cloned `value`.

#### Example

```js
var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

var deep = _.cloneDeep(stooges);
deep[0] === stooges[0];
// => false

var view = {
  'label': 'docs',
  'node': element
};

var clone = _.cloneDeep(view, function(value) {
  return _.isElement(value) ? value.cloneNode(true) : undefined;
});

clone.node == view.node;
// => false
```

* * *

### _.defaults(object [, source1, source2, ...])

Assigns own enumerable properties of source object(s) to the destination object for all destination properties that resolve to `undefined`. Once a property is set, additional defaults of the same property will be ignored.

#### Arguments

1. `object` *(Object)*: The destination object.
2. `[source1, source2, ...]` *(Object)*: The source objects.

#### Returns

*(Object)*: Returns the destination object.

#### Example

```js
var food = { 'name': 'apple' };
_.defaults(food, { 'name': 'banana', 'type': 'fruit' });
// => { 'name': 'apple', 'type': 'fruit' }
```

* * *

### _.findKey(object [, callback=identity, thisArg])

This method is similar to `_.find`, except that it returns the key of the element that passes the callback check, instead of the element itself.

#### Arguments

1. `object` *(Object)*: The object to search.
2. `[callback=identity]` *(Function|Object|String)*: The function called per iteration. If a property name or object is passed, it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the key of the found element, else `undefined`.

#### Example

```js
_.findKey({ 'a': 1, 'b': 2, 'c': 3, 'd': 4 }, function(num) {
  return num % 2 == 0;
});
// => 'b'
```

* * *

### _.forIn(object [, callback=identity, thisArg])

Iterates over `object`'s own and inherited enumerable properties, executing the `callback` for each property. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, key, object)*. Callbacks may exit iteration early by explicitly returning `false`.

#### Arguments

1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns `object`.

#### Example

```js
function Dog(name) {
  this.name = name;
}

Dog.prototype.bark = function() {
  alert('Woof, woof!');
};

_.forIn(new Dog('Dagny'), function(value, key) {
  alert(key);
});
// => alerts 'name' and 'bark' (order is not guaranteed)
```

* * *

### _.forOwn(object [, callback=identity, thisArg])

Iterates over an object's own enumerable properties, executing the `callback` for each property. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, key, object)*. Callbacks may exit iteration early by explicitly returning `false`.

#### Arguments

1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns `object`.

#### Example

```js
_.forOwn({ '0': 'zero', '1': 'one', 'length': 2 }, function(num, key) {
  alert(key);
});
// => alerts '0', '1', and 'length' (order is not guaranteed)
```

* * *

### _.functions(object)

Creates a sorted array of all enumerable properties, own and inherited, of `object` that have function values.

#### Aliases

*methods*

#### Arguments

1. `object` *(Object)*: The object to inspect.

#### Returns

*(Array)*: Returns a new array of property names that have function values.

#### Example

```js
_.functions(_);
// => ['all', 'any', 'bind', 'bindAll', 'clone', 'compact', 'compose', ...]
```

* * *

### _.has(object, property)

Checks if the specified object `property` exists and is a direct property, instead of an inherited property.

#### Arguments

1. `object` *(Object)*: The object to check.
2. `property` *(String)*: The property to check for.

#### Returns

*(Boolean)*: Returns `true` if key is a direct property, else `false`.

#### Example

```js
_.has({ 'a': 1, 'b': 2, 'c': 3 }, 'b');
// => true
```

* * *

### _.invert(object)

Creates an object composed of the inverted keys and values of the given `object`.

#### Arguments

1. `object` *(Object)*: The object to invert.

#### Returns

*(Object)*: Returns the created inverted object.

#### Example

```js
_.invert({ 'first': 'moe', 'second': 'larry' });
// => { 'moe': 'first', 'larry': 'second' }
```

* * *

### _.isArguments(value)

Checks if `value` is an `arguments` object.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is an `arguments` object, else `false`.

#### Example

```js
(function() { return _.isArguments(arguments); })(1, 2, 3);
// => true

_.isArguments([1, 2, 3]);
// => false
```

* * *

### _.isArray(value)

Checks if `value` is an array.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is an array, else `false`.

#### Example

```js
(function() { return _.isArray(arguments); })();
// => false

_.isArray([1, 2, 3]);
// => true
```

* * *

### _.isBoolean(value)

Checks if `value` is a boolean value.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a boolean value, else `false`.

#### Example

```js
_.isBoolean(null);
// => false
```

* * *

### _.isDate(value)

Checks if `value` is a date.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a date, else `false`.

#### Example

```js
_.isDate(new Date);
// => true
```

* * *

### _.isElement(value)

Checks if `value` is a DOM element.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a DOM element, else `false`.

#### Example

```js
_.isElement(document.body);
// => true
```

* * *

### _.isEmpty(value)

Checks if `value` is empty. Arrays, strings, or `arguments` objects with a length of `0` and objects with no own enumerable properties are considered "empty".

#### Arguments

1. `value` *(Array|Object|String)*: The value to inspect.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is empty, else `false`.

#### Example

```js
_.isEmpty([1, 2, 3]);
// => false

_.isEmpty({});
// => true

_.isEmpty('');
// => true
```

* * *

### _.isEqual(a, b [, callback, thisArg])

Performs a deep comparison between two values to determine if they are equivalent to each other. If `callback` is passed, it will be executed to compare values. If `callback` returns `undefined`, comparisons will be handled by the method instead. The `callback` is bound to `thisArg` and invoked with two arguments; *(a, b)*.

#### Arguments

1. `a` *(Mixed)*: The value to compare.
2. `b` *(Mixed)*: The other value to compare.
3. `[callback]` *(Function)*: The function to customize comparing values.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Boolean)*: Returns `true`, if the values are equivalent, else `false`.

#### Example

```js
var moe = { 'name': 'moe', 'age': 40 };
var copy = { 'name': 'moe', 'age': 40 };

moe == copy;
// => false

_.isEqual(moe, copy);
// => true

var words = ['hello', 'goodbye'];
var otherWords = ['hi', 'goodbye'];

_.isEqual(words, otherWords, function(a, b) {
  var reGreet = /^(?:hello|hi)$/i,
      aGreet = _.isString(a) && reGreet.test(a),
      bGreet = _.isString(b) && reGreet.test(b);

  return (aGreet || bGreet) ? (aGreet == bGreet) : undefined;
});
// => true
```

* * *

### _.isFinite(value)

Checks if `value` is, or can be coerced to, a finite number.

Note: This is not the same as native `isFinite`, which will return true for booleans and empty strings. See http://es5.github.com/#x15.1.2.5.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is finite, else `false`.

#### Example

```js
_.isFinite(-101);
// => true

_.isFinite('10');
// => true

_.isFinite(true);
// => false

_.isFinite('');
// => false

_.isFinite(Infinity);
// => false
```

* * *

### _.isFunction(value)

Checks if `value` is a function.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a function, else `false`.

#### Example

```js
_.isFunction(_);
// => true
```

* * *

### _.isNaN(value)

Checks if `value` is `NaN`.

Note: This is not the same as native `isNaN`, which will return `true` for `undefined` and other values. See http://es5.github.com/#x15.1.2.4.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is `NaN`, else `false`.

#### Example

```js
_.isNaN(NaN);
// => true

_.isNaN(new Number(NaN));
// => true

isNaN(undefined);
// => true

_.isNaN(undefined);
// => false
```

* * *

### _.isNull(value)

Checks if `value` is `null`.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is `null`, else `false`.

#### Example

```js
_.isNull(null);
// => true

_.isNull(undefined);
// => false
```

* * *

### _.isNumber(value)

Checks if `value` is a number.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a number, else `false`.

#### Example

```js
_.isNumber(8.4 * 5);
// => true
```

* * *

### _.isObject(value)

Checks if `value` is the language type of Object. *(e.g. arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`)*

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is an object, else `false`.

#### Example

```js
_.isObject({});
// => true

_.isObject([1, 2, 3]);
// => true

_.isObject(1);
// => false
```

* * *

### _.isPlainObject(value)

Checks if a given `value` is an object created by the `Object` constructor.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if `value` is a plain object, else `false`.

#### Example

```js
function Stooge(name, age) {
  this.name = name;
  this.age = age;
}

_.isPlainObject(new Stooge('moe', 40));
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'name': 'moe', 'age': 40 });
// => true
```

* * *

### _.isRegExp(value)

Checks if `value` is a regular expression.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a regular expression, else `false`.

#### Example

```js
_.isRegExp(/moe/);
// => true
```

* * *

### _.isString(value)

Checks if `value` is a string.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is a string, else `false`.

#### Example

```js
_.isString('moe');
// => true
```

* * *

### _.isUndefined(value)

Checks if `value` is `undefined`.

#### Arguments

1. `value` *(Mixed)*: The value to check.

#### Returns

*(Boolean)*: Returns `true`, if the `value` is `undefined`, else `false`.

#### Example

```js
_.isUndefined(void 0);
// => true
```

* * *

### _.keys(object)

Creates an array composed of the own enumerable property names of `object`.

#### Arguments

1. `object` *(Object)*: The object to inspect.

#### Returns

*(Array)*: Returns a new array of property names.

#### Example

```js
_.keys({ 'one': 1, 'two': 2, 'three': 3 });
// => ['one', 'two', 'three'] (order is not guaranteed)
```

* * *

### _.merge(object [, source1, source2, ..., callback, thisArg])

Recursively merges own enumerable properties of the source object(s), that don't resolve to `undefined`, into the destination object. Subsequent sources will overwrite property assignments of previous sources. If a `callback` function is passed, it will be executed to produce the merged values of the destination and source properties. If `callback` returns `undefined`, merging will be handled by the method instead. The `callback` is bound to `thisArg` and invoked with two arguments; *(objectValue, sourceValue)*.

#### Arguments

1. `object` *(Object)*: The destination object.
2. `[source1, source2, ...]` *(Object)*: The source objects.
3. `[callback]` *(Function)*: The function to customize merging properties.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns the destination object.

#### Example

```js
var names = {
  'stooges': [
    { 'name': 'moe' },
    { 'name': 'larry' }
  ]
};

var ages = {
  'stooges': [
    { 'age': 40 },
    { 'age': 50 }
  ]
};

_.merge(names, ages);
// => { 'stooges': [{ 'name': 'moe', 'age': 40 }, { 'name': 'larry', 'age': 50 }] }

var food = {
  'fruits': ['apple'],
  'vegetables': ['beet']
};

var otherFood = {
  'fruits': ['banana'],
  'vegetables': ['carrot']
};

_.merge(food, otherFood, function(a, b) {
  return _.isArray(a) ? a.concat(b) : undefined;
});
// => { 'fruits': ['apple', 'banana'], 'vegetables': ['beet', 'carrot] }
```

* * *

### _.omit(object, callback|[prop1, prop2, ..., thisArg])

Creates a shallow clone of `object` excluding the specified properties. Property names may be specified as individual arguments or as arrays of property names. If a `callback` function is passed, it will be executed for each property in the `object`, omitting the properties `callback` returns truthy for. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, key, object)*.

#### Arguments

1. `object` *(Object)*: The source object.
2. `callback|[prop1, prop2, ...]` *(Function|String)*: The properties to omit or the function called per iteration.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns an object without the omitted properties.

#### Example

```js
_.omit({ 'name': 'moe', 'age': 40 }, 'age');
// => { 'name': 'moe' }

_.omit({ 'name': 'moe', 'age': 40 }, function(value) {
  return typeof value == 'number';
});
// => { 'name': 'moe' }
```

* * *

### _.pairs(object)

Creates a two dimensional array of the given object's key-value pairs, i.e. `[[key1, value1], [key2, value2]]`.

#### Arguments

1. `object` *(Object)*: The object to inspect.

#### Returns

*(Array)*: Returns new array of key-value pairs.

#### Example

```js
_.pairs({ 'moe': 30, 'larry': 40 });
// => [['moe', 30], ['larry', 40]] (order is not guaranteed)
```

* * *

### _.pick(object, callback|[prop1, prop2, ..., thisArg])

Creates a shallow clone of `object` composed of the specified properties. Property names may be specified as individual arguments or as arrays of property names. If `callback` is passed, it will be executed for each property in the `object`, picking the properties `callback` returns truthy for. The `callback` is bound to `thisArg` and invoked with three arguments; *(value, key, object)*.

#### Arguments

1. `object` *(Object)*: The source object.
2. `callback|[prop1, prop2, ...]` *(Array|Function|String)*: The function called per iteration or properties to pick, either as individual arguments or arrays.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Object)*: Returns an object composed of the picked properties.

#### Example

```js
_.pick({ 'name': 'moe', '_userid': 'moe1' }, 'name');
// => { 'name': 'moe' }

_.pick({ 'name': 'moe', '_userid': 'moe1' }, function(value, key) {
  return key.charAt(0) != '_';
});
// => { 'name': 'moe' }
```

* * *

### _.transform(collection [, callback=identity, accumulator, thisArg])

An alternative to `_.reduce`, this method transforms an `object` to a new `accumulator` object which is the result of running each of its elements through the `callback`, with each `callback` execution potentially mutating the `accumulator` object. The `callback` is bound to `thisArg` and invoked with four arguments; *(accumulator, value, key, object)*. Callbacks may exit iteration early by explicitly returning `false`.

#### Arguments

1. `collection` *(Array|Object)*: The collection to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[accumulator]` *(Mixed)*: The custom accumulator value.
4. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Mixed)*: Returns the accumulated value.

#### Example

```js
var squares = _.transform([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], function(result, num) {
  num *= num;
  if (num % 2) {
    return result.push(num) < 3;
  }
});
// => [1, 9, 25]

var mapped = _.transform({ 'a': 1, 'b': 2, 'c': 3 }, function(result, num, key) {
  result[key] = num * 3;
});
// => { 'a': 3, 'b': 6, 'c': 9 }
```

* * *

### _.values(object)

Creates an array composed of the own enumerable property values of `object`.

#### Arguments

1. `object` *(Object)*: The object to inspect.

#### Returns

*(Array)*: Returns a new array of property values.

#### Example

```js
_.values({ 'one': 1, 'two': 2, 'three': 3 });
// => [1, 2, 3] (order is not guaranteed)
```
