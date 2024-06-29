[TOC]

### `_.assign(object, [sources])`

Assigns own enumerable string keyed properties of source objects to the
destination object. Source objects are applied from left to right.
Subsequent sources overwrite property assignments of previous sources.
<br>
<br>
**Note:** This method mutates `object` and is loosely based on
[`Object.assign`](https://mdn.io/Object/assign).

#### Since
0.10.0

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assign({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'c': 3 }
```

### `_.assignIn(object, [sources])`

This method is like `_.assign` except that it iterates over own and
inherited source properties.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.0.0

#### Aliases
*_.extend*

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function Foo() {
  this.a = 1;
}

function Bar() {
  this.c = 3;
}

Foo.prototype.b = 2;
Bar.prototype.d = 4;

_.assignIn({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'b': 2, 'c': 3, 'd': 4 }
```

### `_.assignInWith(object, sources, [customizer])`

This method is like `_.assignIn` except that it accepts `customizer`
which is invoked to produce the assigned values. If `customizer` returns
`undefined`, assignment is handled by the method instead. The `customizer`
is invoked with five arguments: *(objValue, srcValue, key, object, source)*.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.0.0

#### Aliases
*_.extendWith*

#### Arguments
1. `object` *(Object)*: The destination object.
2. `sources` *(...Object)*: The source objects.
3. `[customizer]` *(Function)*: The function to customize assigned values.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignInWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### `_.assignWith(object, sources, [customizer])`

This method is like `_.assign` except that it accepts `customizer`
which is invoked to produce the assigned values. If `customizer` returns
`undefined`, assignment is handled by the method instead. The `customizer`
is invoked with five arguments: *(objValue, srcValue, key, object, source)*.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The destination object.
2. `sources` *(...Object)*: The source objects.
3. `[customizer]` *(Function)*: The function to customize assigned values.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}

var defaults = _.partialRight(_.assignWith, customizer);

defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### `_.at(object, [paths])`

Creates an array of values corresponding to `paths` of `object`.

#### Since
1.0.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[paths]` *(...(string|string&#91;&#93;))*: The property paths to pick.

#### Returns
*(Array)*: Returns the picked values.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

### `_.create(prototype, [properties])`

Creates an object that inherits from the `prototype` object. If a
`properties` object is given, its own enumerable string keyed properties
are assigned to the created object.

#### Since
2.3.0

#### Arguments
1. `prototype` *(Object)*: The object to inherit from.
2. `[properties]` *(Object)*: The properties to assign to the object.

#### Returns
*(Object)*: Returns the new object.

#### Example
```js
function Shape() {
  this.x = 0;
  this.y = 0;
}

function Circle() {
  Shape.call(this);
}

Circle.prototype = _.create(Shape.prototype, {
  'constructor': Circle
});

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true
```

### `_.defaults(object, [sources])`

Assigns own and inherited enumerable string keyed properties of source
objects to the destination object for all destination properties that
resolve to `undefined`. Source objects are applied from left to right.
Once a property is set, additional values of the same property are ignored.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### `_.defaultsDeep(object, [sources])`

This method is like `_.defaults` except that it recursively assigns
default properties.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
3.10.0

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

### `_.findKey(object, [predicate=_.identity])`

This method is like `_.find` except that it returns the key of the first
element `predicate` returns truthy for instead of the element itself.

#### Since
1.1.0

#### Arguments
1. `object` *(Object)*: The object to inspect.
2. `[predicate=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(&#42;)*: Returns the key of the matched element, else `undefined`.

#### Example
```js
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (iteration order is not guaranteed)

// The `_.matches` iteratee shorthand.
_.findKey(users, { 'age': 1, 'active': true });
// => 'pebbles'

// The `_.matchesProperty` iteratee shorthand.
_.findKey(users, ['active', false]);
// => 'fred'

// The `_.property` iteratee shorthand.
_.findKey(users, 'active');
// => 'barney'
```

### `_.findLastKey(object, [predicate=_.identity])`

This method is like `_.findKey` except that it iterates over elements of
a collection in the opposite order.

#### Since
2.0.0

#### Arguments
1. `object` *(Object)*: The object to inspect.
2. `[predicate=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(&#42;)*: Returns the key of the matched element, else `undefined`.

#### Example
```js
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(o) { return o.age < 40; });
// => returns 'pebbles' assuming `_.findKey` returns 'barney'

// The `_.matches` iteratee shorthand.
_.findLastKey(users, { 'age': 36, 'active': true });
// => 'barney'

// The `_.matchesProperty` iteratee shorthand.
_.findLastKey(users, ['active', false]);
// => 'fred'

// The `_.property` iteratee shorthand.
_.findLastKey(users, 'active');
// => 'pebbles'
```

### `_.forIn(object, [iteratee=_.identity])`

Iterates over own and inherited enumerable string keyed properties of an
object and invokes `iteratee` for each property. The iteratee is invoked
with three arguments: *(value, key, object)*. Iteratee functions may exit
iteration early by explicitly returning `false`.

#### Since
0.3.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forIn(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'a', 'b', then 'c' (iteration order is not guaranteed).
```

### `_.forInRight(object, [iteratee=_.identity])`

This method is like `_.forIn` except that it iterates over properties of
`object` in the opposite order.

#### Since
2.0.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forInRight(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'c', 'b', then 'a' assuming `_.forIn` logs 'a', 'b', then 'c'.
```

### `_.forOwn(object, [iteratee=_.identity])`

Iterates over own enumerable string keyed properties of an object and
invokes `iteratee` for each property. The iteratee is invoked with three
arguments: *(value, key, object)*. Iteratee functions may exit iteration
early by explicitly returning `false`.

#### Since
0.3.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwn(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'a' then 'b' (iteration order is not guaranteed).
```

### `_.forOwnRight(object, [iteratee=_.identity])`

This method is like `_.forOwn` except that it iterates over properties of
`object` in the opposite order.

#### Since
2.0.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.forOwnRight(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'b' then 'a' assuming `_.forOwn` logs 'a' then 'b'.
```

### `_.functions(object)`

Creates an array of function property names from own enumerable properties
of `object`.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The object to inspect.

#### Returns
*(Array)*: Returns the function names.

#### Example
```js
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functions(new Foo);
// => ['a', 'b']
```

### `_.functionsIn(object)`

Creates an array of function property names from own and inherited
enumerable properties of `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The object to inspect.

#### Returns
*(Array)*: Returns the function names.

#### Example
```js
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}

Foo.prototype.c = _.constant('c');

_.functionsIn(new Foo);
// => ['a', 'b', 'c']
```

### `_.get(object, path, [defaultValue])`

Gets the value at `path` of `object`. If the resolved value is
`undefined`, the `defaultValue` is returned in its place.

#### Since
3.7.0

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path of the property to get.
3. `[defaultValue]` *(&#42;)*: The value returned for `undefined` resolved values.

#### Returns
*(&#42;)*: Returns the resolved value.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.get(object, 'a[0].b.c');
// => 3

_.get(object, ['a', '0', 'b', 'c']);
// => 3

_.get(object, 'a.b.c', 'default');
// => 'default'
```

### `_.has(object, path)`

Checks if `path` is a direct property of `object`.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path to check.

#### Returns
*(boolean)*: Returns `true` if `path` exists, else `false`.

#### Example
```js
var object = { 'a': { 'b': 2 } };
var other = _.create({ 'a': _.create({ 'b': 2 }) });

_.has(object, 'a');
// => true

_.has(object, 'a.b');
// => true

_.has(object, ['a', 'b']);
// => true

_.has(other, 'a');
// => false
```

### `_.hasIn(object, path)`

Checks if `path` is a direct or inherited property of `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path to check.

#### Returns
*(boolean)*: Returns `true` if `path` exists, else `false`.

#### Example
```js
var object = _.create({ 'a': _.create({ 'b': 2 }) });

_.hasIn(object, 'a');
// => true

_.hasIn(object, 'a.b');
// => true

_.hasIn(object, ['a', 'b']);
// => true

_.hasIn(object, 'b');
// => false
```

### `_.invert(object)`

Creates an object composed of the inverted keys and values of `object`.
If `object` contains duplicate values, subsequent values overwrite
property assignments of previous values.

#### Since
0.7.0

#### Arguments
1. `object` *(Object)*: The object to invert.

#### Returns
*(Object)*: Returns the new inverted object.

#### Example
```js
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }
```

### `_.invertBy(object, [iteratee=_.identity])`

This method is like `_.invert` except that the inverted object is generated
from the results of running each element of `object` thru `iteratee`. The
corresponding inverted value of each inverted key is an array of keys
responsible for generating the inverted value. The iteratee is invoked
with one argument: *(value)*.

#### Since
4.1.0

#### Arguments
1. `object` *(Object)*: The object to invert.
2. `[iteratee=_.identity]` *(Function)*: The iteratee invoked per element.

#### Returns
*(Object)*: Returns the new inverted object.

#### Example
```js
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invertBy(object);
// => { '1': ['a', 'c'], '2': ['b'] }

_.invertBy(object, function(value) {
  return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] }
```

### `_.invoke(object, path, [args])`

Invokes the method at `path` of `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path of the method to invoke.
3. `[args]` *(...&#42;)*: The arguments to invoke the method with.

#### Returns
*(&#42;)*: Returns the result of the invoked method.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };

_.invoke(object, 'a[0].b.c.slice', 1, 3);
// => [2, 3]
```

### `_.keys(object)`

Creates an array of the own enumerable property names of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects. See the
[ES spec](http://ecma-international.org/ecma-262/7.0/#sec-object.keys)
for more details.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*: Returns the array of property names.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)

_.keys('hi');
// => ['0', '1']
```

### `_.keysIn(object)`

Creates an array of the own and inherited enumerable property names of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects.

#### Since
3.0.0

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*: Returns the array of property names.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.keysIn(new Foo);
// => ['a', 'b', 'c'] (iteration order is not guaranteed)
```

### `_.mapKeys(object, [iteratee=_.identity])`

The opposite of `_.mapValues`; this method creates an object with the
same values as `object` and keys generated by running each own enumerable
string keyed property of `object` thru `iteratee`. The iteratee is invoked
with three arguments: *(value, key, object)*.

#### Since
3.8.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(Object)*: Returns the new mapped object.

#### Example
```js
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

### `_.mapValues(object, [iteratee=_.identity])`

Creates an object with the same keys as `object` and values generated
by running each own enumerable string keyed property of `object` thru
`iteratee`. The iteratee is invoked with three arguments:<br>
*(value, key, object)*.

#### Since
2.4.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.

#### Returns
*(Object)*: Returns the new mapped object.

#### Example
```js
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)

// The `_.property` iteratee shorthand.
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
```

### `_.merge(object, [sources])`

This method is like `_.assign` except that it recursively merges own and
inherited enumerable string keyed properties of source objects into the
destination object. Source properties that resolve to `undefined` are
skipped if a destination value exists. Array and plain object properties
are merged recursively. Other objects and value types are overridden by
assignment. Source objects are applied from left to right. Subsequent
sources overwrite property assignments of previous sources.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
0.5.0

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

### `_.mergeWith(object, sources, customizer)`

This method is like `_.merge` except that it accepts `customizer` which
is invoked to produce the merged values of the destination and source
properties. If `customizer` returns `undefined`, merging is handled by the
method instead. The `customizer` is invoked with six arguments:<br>
*(objValue, srcValue, key, object, source, stack)*.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The destination object.
2. `sources` *(...Object)*: The source objects.
3. `customizer` *(Function)*: The function to customize assigned values.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
function customizer(objValue, srcValue) {
  if (_.isArray(objValue)) {
    return objValue.concat(srcValue);
  }
}

var object = { 'a': [1], 'b': [2] };
var other = { 'a': [3], 'b': [4] };

_.mergeWith(object, other, customizer);
// => { 'a': [1, 3], 'b': [2, 4] }
```

### `_.omit(object, [paths])`

The opposite of `_.pick`; this method creates an object composed of the
own and inherited enumerable property paths of `object` that are not omitted.
<br>
<br>
**Note:** This method is considerably slower than `_.pick`.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The source object.
2. `[paths]` *(...(string|string&#91;&#93;))*: The property paths to omit.

#### Returns
*(Object)*: Returns the new object.

#### Example
```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

### `_.omitBy(object, [predicate=_.identity])`

The opposite of `_.pickBy`; this method creates an object composed of
the own and inherited enumerable string keyed properties of `object` that
`predicate` doesn't return truthy for. The predicate is invoked with two
arguments: *(value, key)*.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The source object.
2. `[predicate=_.identity]` *(Function)*: The function invoked per property.

#### Returns
*(Object)*: Returns the new object.

#### Example
```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

### `_.pick(object, [paths])`

Creates an object composed of the picked `object` properties.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The source object.
2. `[paths]` *(...(string|string&#91;&#93;))*: The property paths to pick.

#### Returns
*(Object)*: Returns the new object.

#### Example
```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

### `_.pickBy(object, [predicate=_.identity])`

Creates an object composed of the `object` properties `predicate` returns
truthy for. The predicate is invoked with two arguments: *(value, key)*.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The source object.
2. `[predicate=_.identity]` *(Function)*: The function invoked per property.

#### Returns
*(Object)*: Returns the new object.

#### Example
```js
var object = { 'a': 1, 'b': '2', 'c': 3 };

_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

### `_.result(object, path, [defaultValue])`

This method is like `_.get` except that if the resolved value is a
function it's invoked with the `this` binding of its parent object and
its result is returned.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path of the property to resolve.
3. `[defaultValue]` *(&#42;)*: The value returned for `undefined` resolved values.

#### Returns
*(&#42;)*: Returns the resolved value.

#### Example
```js
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a[0].b.c3', 'default');
// => 'default'

_.result(object, 'a[0].b.c3', _.constant('default'));
// => 'default'
```

### `_.set(object, path, value)`

Sets the value at `path` of `object`. If a portion of `path` doesn't exist,
it's created. Arrays are created for missing index properties while objects
are created for all other missing properties. Use `_.setWith` to customize
`path` creation.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
3.7.0

#### Arguments
1. `object` *(Object)*: The object to modify.
2. `path` *(Array|string)*: The path of the property to set.
3. `value` *(&#42;)*: The value to set.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

### `_.setWith(object, path, value, [customizer])`

This method is like `_.set` except that it accepts `customizer` which is
invoked to produce the objects of `path`.  If `customizer` returns `undefined`
path creation is handled by the method instead. The `customizer` is invoked
with three arguments: *(nsValue, key, nsObject)*.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The object to modify.
2. `path` *(Array|string)*: The path of the property to set.
3. `value` *(&#42;)*: The value to set.
4. `[customizer]` *(Function)*: The function to customize assigned values.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
var object = {};

_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

### `_.toPairs(object)`

Creates an array of own enumerable string keyed-value pairs for `object`
which can be consumed by `_.fromPairs`. If `object` is a map or set, its
entries are returned.

#### Since
4.0.0

#### Aliases
*_.entries*

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*: Returns the key-value pairs.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (iteration order is not guaranteed)
```

### `_.toPairsIn(object)`

Creates an array of own and inherited enumerable string keyed-value pairs
for `object` which can be consumed by `_.fromPairs`. If `object` is a map
or set, its entries are returned.

#### Since
4.0.0

#### Aliases
*_.entriesIn*

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*: Returns the key-value pairs.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 3]] (iteration order is not guaranteed)
```

### `_.transform(object, [iteratee=_.identity], [accumulator])`

An alternative to `_.reduce`; this method transforms `object` to a new
`accumulator` object which is the result of running each of its own
enumerable string keyed properties thru `iteratee`, with each invocation
potentially mutating the `accumulator` object. If `accumulator` is not
provided, a new object with the same `[[Prototype]]` will be used. The
iteratee is invoked with four arguments: *(accumulator, value, key, object)*.
Iteratee functions may exit iteration early by explicitly returning `false`.

#### Since
1.3.0

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[accumulator]` *(&#42;)*: The custom accumulator value.

#### Returns
*(&#42;)*: Returns the accumulated value.

#### Example
```js
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
}, []);
// => [4, 9]

_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] }
```

### `_.unset(object, path)`

Removes the property at `path` of `object`.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.0.0

#### Arguments
1. `object` *(Object)*: The object to modify.
2. `path` *(Array|string)*: The path of the property to unset.

#### Returns
*(boolean)*: Returns `true` if the property is deleted, else `false`.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };

_.unset(object, ['a', '0', 'b', 'c']);
// => true

console.log(object);
// => { 'a': [{ 'b': {} }] };
```

### `_.update(object, path, updater)`

This method is like `_.set` except that accepts `updater` to produce the
value to set. Use `_.updateWith` to customize `path` creation. The `updater`
is invoked with one argument: *(value)*.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.6.0

#### Arguments
1. `object` *(Object)*: The object to modify.
2. `path` *(Array|string)*: The path of the property to set.
3. `updater` *(Function)*: The function to produce the updated value.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.update(object, 'a[0].b.c', function(n) { return n * n; });
console.log(object.a[0].b.c);
// => 9

_.update(object, 'x[0].y.z', function(n) { return n ? n + 1 : 0; });
console.log(object.x[0].y.z);
// => 0
```

### `_.updateWith(object, path, updater, [customizer])`

This method is like `_.update` except that it accepts `customizer` which is
invoked to produce the objects of `path`.  If `customizer` returns `undefined`
path creation is handled by the method instead. The `customizer` is invoked
with three arguments: *(nsValue, key, nsObject)*.
<br>
<br>
**Note:** This method mutates `object`.

#### Since
4.6.0

#### Arguments
1. `object` *(Object)*: The object to modify.
2. `path` *(Array|string)*: The path of the property to set.
3. `updater` *(Function)*: The function to produce the updated value.
4. `[customizer]` *(Function)*: The function to customize assigned values.

#### Returns
*(Object)*: Returns `object`.

#### Example
```js
var object = {};

_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

### `_.values(object)`

Creates an array of the own enumerable string keyed property values of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects.

#### Since
0.1.0

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*: Returns the array of property values.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.values(new Foo);
// => [1, 2] (iteration order is not guaranteed)

_.values('hi');
// => ['h', 'i']
```

### `_.valuesIn(object)`

Creates an array of the own and inherited enumerable string keyed property
values of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects.

#### Since
3.0.0

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*: Returns the array of property values.

#### Example
```js
function Foo() {
  this.a = 1;
  this.b = 2;
}

Foo.prototype.c = 3;

_.valuesIn(new Foo);
// => [1, 2, 3] (iteration order is not guaranteed)
```
