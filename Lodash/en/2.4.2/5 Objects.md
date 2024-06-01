[TOC]

### _.assign(object, [source], [callback], [thisArg])

Assigns own enumerable properties of source object(s) to the destination
object. Subsequent sources will overwrite property assignments of previous
sources. If a callback is provided it will be executed to produce the
assigned values. The callback is bound to `thisArg` and invoked with two
arguments; (objectValue, sourceValue).

#### Aliases
*_.extend*

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[source]` *(...Object)*: The source objects.
3. `[callback]` *(Function)*: The function to customize assigning values.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns the destination object.

#### Example
```js
_.assign({ 'name': 'fred' }, { 'employer': 'slate' });
// => { 'name': 'fred', 'employer': 'slate' }

var defaults = _.partialRight(_.assign, function(a, b) {
  return typeof a == 'undefined' ? b : a;
});

var object = { 'name': 'barney' };
defaults(object, { 'name': 'fred', 'employer': 'slate' });
// => { 'name': 'barney', 'employer': 'slate' }
```
* * *

### _.clone(value, [isDeep=false], [callback], [thisArg])

Creates a clone of `value`. If `isDeep` is `true` nested objects will also
be cloned, otherwise they will be assigned by reference. If a callback
is provided it will be executed to produce the cloned values. If the
callback returns `undefined` cloning will be handled by the method instead.
The callback is bound to `thisArg` and invoked with one argument; (value).

#### Arguments
1. `value` *(&#42;)*: The value to clone.
2. `[isDeep=false]` *(boolean)*: Specify a deep clone.
3. `[callback]` *(Function)*: The function to customize cloning values.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the cloned value.

#### Example
```js
var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

var shallow = _.clone(characters);
shallow[0] === characters[0];
// => true

var deep = _.clone(characters, true);
deep[0] === characters[0];
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

### _.cloneDeep(value, [callback], [thisArg])

Creates a deep clone of `value`. If a callback is provided it will be
executed to produce the cloned values. If the callback returns `undefined`
cloning will be handled by the method instead. The callback is bound to
`thisArg` and invoked with one argument; (value).
<br>
<br>
Note: This method is loosely based on the structured clone algorithm. Functions
and DOM nodes are **not** cloned. The enumerable properties of `arguments` objects and
objects created by constructors other than `Object` are cloned to plain `Object` objects.
See http://www.w3.org/TR/html5/infrastructure.html#internal-structured-cloning-algorithm.

#### Arguments
1. `value` *(&#42;)*: The value to deep clone.
2. `[callback]` *(Function)*: The function to customize cloning values.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the deep cloned value.

#### Example
```js
var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

var deep = _.cloneDeep(characters);
deep[0] === characters[0];
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

### _.create(prototype, [properties])

Creates an object that inherits from the given `prototype` object. If a
`properties` object is provided its own enumerable properties are assigned
to the created object.

#### Arguments
1. `prototype` *(Object)*: The object to inherit from.
2. `[properties]` *(Object)*: The properties to assign to the object.

#### Returns
*(Object)*:  Returns the new object.

#### Example
```js
function Shape() {
  this.x = 0;
  this.y = 0;
}

function Circle() {
  Shape.call(this);
}

Circle.prototype = _.create(Shape.prototype, { 'constructor': Circle });

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true
```
* * *

### _.defaults(object, [source])

Assigns own enumerable properties of source object(s) to the destination
object for all destination properties that resolve to `undefined`. Once a
property is set, additional defaults of the same property will be ignored.

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[source]` *(...Object)*: The source objects.

#### Returns
*(Object)*:  Returns the destination object.

#### Example
```js
var object = { 'name': 'barney' };
_.defaults(object, { 'name': 'fred', 'employer': 'slate' });
// => { 'name': 'barney', 'employer': 'slate' }
```
* * *

### _.findKey(object, [callback=identity], [thisArg])

This method is like `_.findIndex` except that it returns the key of the
first element that passes the callback check, instead of the element itself.
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
1. `object` *(Object)*: The object to search.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(string|undefined)*:  Returns the key of the found element, else `undefined`.

#### Example
```js
var characters = {
  'barney': {  'age': 36, 'blocked': false },
  'fred': {    'age': 40, 'blocked': true },
  'pebbles': { 'age': 1,  'blocked': false }
};

_.findKey(characters, function(chr) {
  return chr.age < 40;
});
// => 'barney' (property order is not guaranteed across environments)

// using "_.where" callback shorthand
_.findKey(characters, { 'age': 1 });
// => 'pebbles'

// using "_.pluck" callback shorthand
_.findKey(characters, 'blocked');
// => 'fred'
```
* * *

### _.findLastKey(object, [callback=identity], [thisArg])

This method is like `_.findKey` except that it iterates over elements
of a `collection` in the opposite order.
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
1. `object` *(Object)*: The object to search.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(string|undefined)*:  Returns the key of the found element, else `undefined`.

#### Example
```js
var characters = {
  'barney': {  'age': 36, 'blocked': true },
  'fred': {    'age': 40, 'blocked': false },
  'pebbles': { 'age': 1,  'blocked': true }
};

_.findLastKey(characters, function(chr) {
  return chr.age < 40;
});
// => returns `pebbles`, assuming `_.findKey` returns `barney`

// using "_.where" callback shorthand
_.findLastKey(characters, { 'age': 40 });
// => 'fred'

// using "_.pluck" callback shorthand
_.findLastKey(characters, 'blocked');
// => 'pebbles'
```
* * *

### _.forIn(object, [callback=identity], [thisArg])

Iterates over own and inherited enumerable properties of an object,
executing the callback for each property. The callback is bound to `thisArg`
and invoked with three arguments; (value, key, object). Callbacks may exit
iteration early by explicitly returning `false`.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
function Shape() {
  this.x = 0;
  this.y = 0;
}

Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
};

_.forIn(new Shape, function(value, key) {
  console.log(key);
});
// => logs 'x', 'y', and 'move' (property order is not guaranteed across environments)
```
* * *

### _.forInRight(object, [callback=identity], [thisArg])

This method is like `_.forIn` except that it iterates over elements
of a `collection` in the opposite order.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
function Shape() {
  this.x = 0;
  this.y = 0;
}

Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
};

_.forInRight(new Shape, function(value, key) {
  console.log(key);
});
// => logs 'move', 'y', and 'x' assuming `_.forIn ` logs 'x', 'y', and 'move'
```
* * *

### _.forOwn(object, [callback=identity], [thisArg])

Iterates over own enumerable properties of an object, executing the callback
for each property. The callback is bound to `thisArg` and invoked with three
arguments; (value, key, object). Callbacks may exit iteration early by
explicitly returning `false`.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
_.forOwn({ '0': 'zero', '1': 'one', 'length': 2 }, function(num, key) {
  console.log(key);
});
// => logs '0', '1', and 'length' (property order is not guaranteed across environments)
```
* * *

### _.forOwnRight(object, [callback=identity], [thisArg])

This method is like `_.forOwn` except that it iterates over elements
of a `collection` in the opposite order.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
_.forOwnRight({ '0': 'zero', '1': 'one', 'length': 2 }, function(num, key) {
  console.log(key);
});
// => logs 'length', '1', and '0' assuming `_.forOwn` logs '0', '1', and 'length'
```
* * *

### _.functions(object)

Creates a sorted array of property names of all enumerable properties,
own and inherited, of `object` that have function values.

#### Aliases
*_.methods*

#### Arguments
1. `object` *(Object)*: The object to inspect.

#### Returns
*(Array)*:  Returns an array of property names that have function values.

#### Example
```js
_.functions(_);
// => ['all', 'any', 'bind', 'bindAll', 'clone', 'compact', 'compose', ...]
```
* * *

### _.has(object, key)

Checks if the specified property name exists as a direct property of `object`,
instead of an inherited property.

#### Arguments
1. `object` *(Object)*: The object to inspect.
2. `key` *(string)*: The name of the property to check.

#### Returns
*(boolean)*:  Returns `true` if key is a direct property, else `false`.

#### Example
```js
_.has({ 'a': 1, 'b': 2, 'c': 3 }, 'b');
// => true
```
* * *

### _.invert(object)

Creates an object composed of the inverted keys and values of the given object.

#### Arguments
1. `object` *(Object)*: The object to invert.

#### Returns
*(Object)*:  Returns the created inverted object.

#### Example
```js
_.invert({ 'first': 'fred', 'second': 'barney' });
// => { 'fred': 'first', 'barney': 'second' }
```
* * *

### _.isArguments(value)

Checks if `value` is an `arguments` object.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is an `arguments` object, else `false`.

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
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is an array, else `false`.

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
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a boolean value, else `false`.

#### Example
```js
_.isBoolean(null);
// => false
```
* * *

### _.isDate(value)

Checks if `value` is a date.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a date, else `false`.

#### Example
```js
_.isDate(new Date);
// => true
```
* * *

### _.isElement(value)

Checks if `value` is a DOM element.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a DOM element, else `false`.

#### Example
```js
_.isElement(document.body);
// => true
```
* * *

### _.isEmpty(value)

Checks if `value` is empty. Arrays, strings, or `arguments` objects with a
length of `0` and objects with no own enumerable properties are considered
"empty".

#### Arguments
1. `value` *(Array|Object|string)*: The value to inspect.

#### Returns
*(boolean)*:  Returns `true` if the `value` is empty, else `false`.

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

### _.isEqual(a, b, [callback], [thisArg])

Performs a deep comparison between two values to determine if they are
equivalent to each other. If a callback is provided it will be executed
to compare values. If the callback returns `undefined` comparisons will
be handled by the method instead. The callback is bound to `thisArg` and
invoked with two arguments; (a, b).

#### Arguments
1. `a` *(&#42;)*: The value to compare.
2. `b` *(&#42;)*: The other value to compare.
3. `[callback]` *(Function)*: The function to customize comparing values.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(boolean)*:  Returns `true` if the values are equivalent, else `false`.

#### Example
```js
var object = { 'name': 'fred' };
var copy = { 'name': 'fred' };

object == copy;
// => false

_.isEqual(object, copy);
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
<br>
<br>
Note: This is not the same as native `isFinite` which will return true for
booleans and empty strings. See http://es5.github.io/#x15.1.2.5.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is finite, else `false`.

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
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a function, else `false`.

#### Example
```js
_.isFunction(_);
// => true
```
* * *

### _.isNaN(value)

Checks if `value` is `NaN`.
<br>
<br>
Note: This is not the same as native `isNaN` which will return `true` for
`undefined` and other non-numeric values. See http://es5.github.io/#x15.1.2.4.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is `NaN`, else `false`.

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
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is `null`, else `false`.

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
<br>
<br>
Note: `NaN` is considered a number. See http://es5.github.io/#x8.5.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a number, else `false`.

#### Example
```js
_.isNumber(8.4 * 5);
// => true
```
* * *

### _.isObject(value)

Checks if `value` is the language type of Object.
(e.g. arrays, functions, objects, regexes, `new Number(0)`, and `new String('')`)

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is an object, else `false`.

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

Checks if `value` is an object created by the `Object` constructor.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if `value` is a plain object, else `false`.

#### Example
```js
function Shape() {
  this.x = 0;
  this.y = 0;
}

_.isPlainObject(new Shape);
// => false

_.isPlainObject([1, 2, 3]);
// => false

_.isPlainObject({ 'x': 0, 'y': 0 });
// => true
```
* * *

### _.isRegExp(value)

Checks if `value` is a regular expression.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a regular expression, else `false`.

#### Example
```js
_.isRegExp(/fred/);
// => true
```
* * *

### _.isString(value)

Checks if `value` is a string.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is a string, else `false`.

#### Example
```js
_.isString('fred');
// => true
```
* * *

### _.isUndefined(value)

Checks if `value` is `undefined`.

#### Arguments
1. `value` *(&#42;)*: The value to check.

#### Returns
*(boolean)*:  Returns `true` if the `value` is `undefined`, else `false`.

#### Example
```js
_.isUndefined(void 0);
// => true
```
* * *

### _.keys(object)

Creates an array composed of the own enumerable property names of an object.

#### Arguments
1. `object` *(Object)*: The object to inspect.

#### Returns
*(Array)*:  Returns an array of property names.

#### Example
```js
_.keys({ 'one': 1, 'two': 2, 'three': 3 });
// => ['one', 'two', 'three'] (property order is not guaranteed across environments)
```
* * *

### _.mapValues(object, [callback=identity], [thisArg])

Creates an object with the same keys as `object` and values generated by
running each own enumerable property of `object` through the callback.
The callback is bound to `thisArg` and invoked with three arguments;
(value, key, object).
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
1. `object` *(Object)*: The object to iterate over.
2. `[callback=identity]` *(Function|Object|string)*: The function called per iteration. If a property name or object is provided it will be used to create a "_.pluck" or "_.where" style callback, respectively.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns a new object with values of the results of each `callback` execution.

#### Example
```js
_.mapValues({ 'a': 1, 'b': 2, 'c': 3} , function(num) { return num * 3; });
// => { 'a': 3, 'b': 6, 'c': 9 }

var characters = {
  'fred': { 'name': 'fred', 'age': 40 },
  'pebbles': { 'name': 'pebbles', 'age': 1 }
};

// using "_.pluck" callback shorthand
_.mapValues(characters, 'age');
// => { 'fred': 40, 'pebbles': 1 }
```
* * *

### _.merge(object, [source], [callback], [thisArg])

Recursively merges own enumerable properties of the source object(s), that
don't resolve to `undefined` into the destination object. Subsequent sources
will overwrite property assignments of previous sources. If a callback is
provided it will be executed to produce the merged values of the destination
and source properties. If the callback returns `undefined` merging will
be handled by the method instead. The callback is bound to `thisArg` and
invoked with two arguments; (objectValue, sourceValue).

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[source]` *(...Object)*: The source objects.
3. `[callback]` *(Function)*: The function to customize merging properties.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns the destination object.

#### Example
```js
var names = {
  'characters': [
    { 'name': 'barney' },
    { 'name': 'fred' }
  ]
};

var ages = {
  'characters': [
    { 'age': 36 },
    { 'age': 40 }
  ]
};

_.merge(names, ages);
// => { 'characters': [{ 'name': 'barney', 'age': 36 }, { 'name': 'fred', 'age': 40 }] }

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

### _.omit(object, [callback], [thisArg])

Creates a shallow clone of `object` excluding the specified properties.
Property names may be specified as individual arguments or as arrays of
property names. If a callback is provided it will be executed for each
property of `object` omitting the properties the callback returns truey
for. The callback is bound to `thisArg` and invoked with three arguments;
(value, key, object).

#### Arguments
1. `object` *(Object)*: The source object.
2. `[callback]` *(Function|...string|string&#91;&#93;)*: The properties to omit or the function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns an object without the omitted properties.

#### Example
```js
_.omit({ 'name': 'fred', 'age': 40 }, 'age');
// => { 'name': 'fred' }

_.omit({ 'name': 'fred', 'age': 40 }, function(value) {
  return typeof value == 'number';
});
// => { 'name': 'fred' }
```
* * *

### _.pairs(object)

Creates a two dimensional array of an object's key-value pairs,
i.e. `[[key1, value1], [key2, value2]]`.

#### Arguments
1. `object` *(Object)*: The object to inspect.

#### Returns
*(Array)*:  Returns new array of key-value pairs.

#### Example
```js
_.pairs({ 'barney': 36, 'fred': 40 });
// => [['barney', 36], ['fred', 40]] (property order is not guaranteed across environments)
```
* * *

### _.pick(object, [callback], [thisArg])

Creates a shallow clone of `object` composed of the specified properties.
Property names may be specified as individual arguments or as arrays of
property names. If a callback is provided it will be executed for each
property of `object` picking the properties the callback returns truey
for. The callback is bound to `thisArg` and invoked with three arguments;
(value, key, object).

#### Arguments
1. `object` *(Object)*: The source object.
2. `[callback]` *(Function|...string|string&#91;&#93;)*: The function called per iteration or property names to pick, specified as individual property names or arrays of property names.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Object)*:  Returns an object composed of the picked properties.

#### Example
```js
_.pick({ 'name': 'fred', '_userid': 'fred1' }, 'name');
// => { 'name': 'fred' }

_.pick({ 'name': 'fred', '_userid': 'fred1' }, function(value, key) {
  return key.charAt(0) != '_';
});
// => { 'name': 'fred' }
```
* * *

### _.transform(object, [callback=identity], [accumulator], [thisArg])

An alternative to `_.reduce` this method transforms `object` to a new
`accumulator` object which is the result of running each of its own
enumerable properties through a callback, with each callback execution
potentially mutating the `accumulator` object. The callback is bound to
`thisArg` and invoked with four arguments; (accumulator, value, key, object).
Callbacks may exit iteration early by explicitly returning `false`.

#### Arguments
1. `object` *(Array|Object)*: The object to iterate over.
2. `[callback=identity]` *(Function)*: The function called per iteration.
3. `[accumulator]` *(&#42;)*: The custom accumulator value.
4. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(&#42;)*:  Returns the accumulated value.

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
*(Array)*:  Returns an array of property values.

#### Example
```js
_.values({ 'one': 1, 'two': 2, 'three': 3 });
// => [1, 2, 3] (property order is not guaranteed across environments)
```
* * *
