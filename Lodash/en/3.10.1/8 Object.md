[TOC]

### _.assign(object, [sources], [customizer], [thisArg])

Assigns own enumerable properties of source object(s) to the destination
object. Subsequent sources overwrite property assignments of previous sources.
If `customizer` is provided it's invoked to produce the assigned values.
The `customizer` is bound to `thisArg` and invoked with five arguments:<br>
(objectValue, sourceValue, key, object, source).
<br>
<br>
**Note:** This method mutates `object` and is based on
[`Object.assign`](http://ecma-international.org/ecma-262/6.0/#sec-object.assign).

#### Aliases
*_.extend*

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.
3. `[customizer]` *(Function)*: The function to customize assigned values.
4. `[thisArg]` *(&#42;)*: The `this` binding of `customizer`.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
_.assign({ 'user': 'barney' }, { 'age': 40 }, { 'user': 'fred' });
// => { 'user': 'fred', 'age': 40 }

// using a customizer callback
var defaults = _.partialRight(_.assign, function(value, other) {
  return _.isUndefined(value) ? other : value;
});

defaults({ 'user': 'barney' }, { 'age': 36 }, { 'user': 'fred' });
// => { 'user': 'barney', 'age': 36 }
```

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

Circle.prototype = _.create(Shape.prototype, {
  'constructor': Circle
});

var circle = new Circle;
circle instanceof Circle;
// => true

circle instanceof Shape;
// => true
```

### _.defaults(object, [sources])

Assigns own enumerable properties of source object(s) to the destination
object for all destination properties that resolve to `undefined`. Once a
property is set, additional values of the same property are ignored.
<br>
<br>
**Note:** This method mutates `object`.

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
_.defaults({ 'user': 'barney' }, { 'age': 36 }, { 'user': 'fred' });
// => { 'user': 'barney', 'age': 36 }
```

### _.defaultsDeep(object, [sources])

This method is like `_.defaults` except that it recursively assigns
default properties.
<br>
<br>
**Note:** This method mutates `object`.

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
_.defaultsDeep({ 'user': { 'name': 'barney' } }, { 'user': { 'name': 'fred', 'age': 36 } });
// => { 'user': { 'name': 'barney', 'age': 36 } }
```

### _.findKey(object, [predicate=_.identity], [thisArg])

This method is like `_.find` except that it returns the key of the first
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
1. `object` *(Object)*: The object to search.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(string|undefined)*:  Returns the key of the matched element, else `undefined`.

#### Example
```js
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findKey(users, function(chr) {
  return chr.age < 40;
});
// => 'barney' (iteration order is not guaranteed)

// using the `_.matches` callback shorthand
_.findKey(users, { 'age': 1, 'active': true });
// => 'pebbles'

// using the `_.matchesProperty` callback shorthand
_.findKey(users, 'active', false);
// => 'fred'

// using the `_.property` callback shorthand
_.findKey(users, 'active');
// => 'barney'
```

### _.findLastKey(object, [predicate=_.identity], [thisArg])

This method is like `_.findKey` except that it iterates over elements of
a collection in the opposite order.
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
1. `object` *(Object)*: The object to search.
2. `[predicate=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(string|undefined)*:  Returns the key of the matched element, else `undefined`.

#### Example
```js
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};

_.findLastKey(users, function(chr) {
  return chr.age < 40;
});
// => returns `pebbles` assuming `_.findKey` returns `barney`

// using the `_.matches` callback shorthand
_.findLastKey(users, { 'age': 36, 'active': true });
// => 'barney'

// using the `_.matchesProperty` callback shorthand
_.findLastKey(users, 'active', false);
// => 'fred'

// using the `_.property` callback shorthand
_.findLastKey(users, 'active');
// => 'pebbles'
```

### _.forIn(object, [iteratee=_.identity], [thisArg])

Iterates over own and inherited enumerable properties of an object invoking
`iteratee` for each property. The `iteratee` is bound to `thisArg` and invoked
with three arguments: (value, key, object). Iteratee functions may exit
iteration early by explicitly returning `false`.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns `object`.

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
// => logs 'a', 'b', and 'c' (iteration order is not guaranteed)
```

### _.forInRight(object, [iteratee=_.identity], [thisArg])

This method is like `_.forIn` except that it iterates over properties of
`object` in the opposite order.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns `object`.

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
// => logs 'c', 'b', and 'a' assuming `_.forIn ` logs 'a', 'b', and 'c'
```

### _.forOwn(object, [iteratee=_.identity], [thisArg])

Iterates over own enumerable properties of an object invoking `iteratee`
for each property. The `iteratee` is bound to `thisArg` and invoked with
three arguments: (value, key, object). Iteratee functions may exit iteration
early by explicitly returning `false`.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns `object`.

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
// => logs 'a' and 'b' (iteration order is not guaranteed)
```

### _.forOwnRight(object, [iteratee=_.identity], [thisArg])

This method is like `_.forOwn` except that it iterates over properties of
`object` in the opposite order.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns `object`.

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
// => logs 'b' and 'a' assuming `_.forOwn` logs 'a' and 'b'
```

### _.functions(object)

Creates an array of function property names from all enumerable properties,
own and inherited, of `object`.

#### Aliases
*_.methods*

#### Arguments
1. `object` *(Object)*: The object to inspect.

#### Returns
*(Array)*:  Returns the new array of property names.

#### Example
```js
_.functions(_);
// => ['after', 'ary', 'assign', ...]
```

### _.get(object, path, [defaultValue])

Gets the property value at `path` of `object`. If the resolved value is
`undefined` the `defaultValue` is used in its place.

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path of the property to get.
3. `[defaultValue]` *(&#42;)*: The value returned if the resolved value is `undefined`.

#### Returns
*(&#42;)*:  Returns the resolved value.

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

### _.has(object, path)

Checks if `path` is a direct property.

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path to check.

#### Returns
*(boolean)*:  Returns `true` if `path` is a direct property, else `false`.

#### Example
```js
var object = { 'a': { 'b': { 'c': 3 } } };

_.has(object, 'a');
// => true

_.has(object, 'a.b.c');
// => true

_.has(object, ['a', 'b', 'c']);
// => true
```

### _.invert(object, [multiValue])

Creates an object composed of the inverted keys and values of `object`.
If `object` contains duplicate values, subsequent values overwrite property
assignments of previous values unless `multiValue` is `true`.

#### Arguments
1. `object` *(Object)*: The object to invert.
2. `[multiValue]` *(boolean)*: Allow multiple values per key.

#### Returns
*(Object)*:  Returns the new inverted object.

#### Example
```js
var object = { 'a': 1, 'b': 2, 'c': 1 };

_.invert(object);
// => { '1': 'c', '2': 'b' }

// with `multiValue`
_.invert(object, true);
// => { '1': ['a', 'c'], '2': ['b'] }
```

### _.keys(object)

Creates an array of the own enumerable property names of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects. See the
[ES spec](http://ecma-international.org/ecma-262/6.0/#sec-object.keys)
for more details.

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*:  Returns the array of property names.

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

### _.keysIn(object)

Creates an array of the own and inherited enumerable property names of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects.

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*:  Returns the array of property names.

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

### _.mapKeys(object, [iteratee=_.identity], [thisArg])
`
<a href="#_mapkeysobject-iteratee_identity-thisarg">#</a> [&#x24C8;](https://github.com/lodash/lodash/blob/3.10.1/lodash.src.js#L9945 "View in source") [&#x24C9;][1] [&#x24C3;](https://www.npmjs.com/package/lodash.mapkeys "See the npm package")

The opposite of `_.mapValues`; this method creates an object with the
same values as `object` and keys generated by running each own enumerable
property of `object` through `iteratee`.

#### Arguments
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns the new mapped object.

#### Example
```js
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

### _.mapValues(object, [iteratee=_.identity], [thisArg])

Creates an object with the same keys as `object` and values generated by
running each own enumerable property of `object` through `iteratee`. The
iteratee function is bound to `thisArg` and invoked with three arguments:<br>
(value, key, object).
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
1. `object` *(Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(Object)*:  Returns the new mapped object.

#### Example
```js
_.mapValues({ 'a': 1, 'b': 2 }, function(n) {
  return n * 3;
});
// => { 'a': 3, 'b': 6 }

var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};

// using the `_.property` callback shorthand
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
```

### _.merge(object, [sources], [customizer], [thisArg])

Recursively merges own enumerable properties of the source object(s), that
don't resolve to `undefined` into the destination object. Subsequent sources
overwrite property assignments of previous sources. If `customizer` is
provided it's invoked to produce the merged values of the destination and
source properties. If `customizer` returns `undefined` merging is handled
by the method instead. The `customizer` is bound to `thisArg` and invoked
with five arguments: (objectValue, sourceValue, key, object, source).

#### Arguments
1. `object` *(Object)*: The destination object.
2. `[sources]` *(...Object)*: The source objects.
3. `[customizer]` *(Function)*: The function to customize assigned values.
4. `[thisArg]` *(&#42;)*: The `this` binding of `customizer`.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
var users = {
  'data': [{ 'user': 'barney' }, { 'user': 'fred' }]
};

var ages = {
  'data': [{ 'age': 36 }, { 'age': 40 }]
};

_.merge(users, ages);
// => { 'data': [{ 'user': 'barney', 'age': 36 }, { 'user': 'fred', 'age': 40 }] }

// using a customizer callback
var object = {
  'fruits': ['apple'],
  'vegetables': ['beet']
};

var other = {
  'fruits': ['banana'],
  'vegetables': ['carrot']
};

_.merge(object, other, function(a, b) {
  if (_.isArray(a)) {
    return a.concat(b);
  }
});
// => { 'fruits': ['apple', 'banana'], 'vegetables': ['beet', 'carrot'] }
```

### _.omit(object, [predicate], [thisArg])

The opposite of `_.pick`; this method creates an object composed of the
own and inherited enumerable properties of `object` that are not omitted.

#### Arguments
1. `object` *(Object)*: The source object.
2. `[predicate]` *(Function|...(string|string&#91;&#93;)*: The function invoked per iteration or property names to omit, specified as individual property names or arrays of property names.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Object)*:  Returns the new object.

#### Example
```js
var object = { 'user': 'fred', 'age': 40 };

_.omit(object, 'age');
// => { 'user': 'fred' }

_.omit(object, _.isNumber);
// => { 'user': 'fred' }
```

### _.pairs(object)

Creates a two dimensional array of the key-value pairs for `object`,
e.g. `[[key1, value1], [key2, value2]]`.

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*:  Returns the new array of key-value pairs.

#### Example
```js
_.pairs({ 'barney': 36, 'fred': 40 });
// => [['barney', 36], ['fred', 40]] (iteration order is not guaranteed)
```

### _.pick(object, [predicate], [thisArg])

Creates an object composed of the picked `object` properties. Property
names may be specified as individual arguments or as arrays of property
names. If `predicate` is provided it's invoked for each property of `object`
picking the properties `predicate` returns truthy for. The predicate is
bound to `thisArg` and invoked with three arguments: (value, key, object).

#### Arguments
1. `object` *(Object)*: The source object.
2. `[predicate]` *(Function|...(string|string&#91;&#93;)*: The function invoked per iteration or property names to pick, specified as individual property names or arrays of property names.
3. `[thisArg]` *(&#42;)*: The `this` binding of `predicate`.

#### Returns
*(Object)*:  Returns the new object.

#### Example
```js
var object = { 'user': 'fred', 'age': 40 };

_.pick(object, 'user');
// => { 'user': 'fred' }

_.pick(object, _.isString);
// => { 'user': 'fred' }
```

### _.result(object, path, [defaultValue])

This method is like `_.get` except that if the resolved value is a function
it's invoked with the `this` binding of its parent object and its result
is returned.

#### Arguments
1. `object` *(Object)*: The object to query.
2. `path` *(Array|string)*: The path of the property to resolve.
3. `[defaultValue]` *(&#42;)*: The value returned if the resolved value is `undefined`.

#### Returns
*(&#42;)*:  Returns the resolved value.

#### Example
```js
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };

_.result(object, 'a[0].b.c1');
// => 3

_.result(object, 'a[0].b.c2');
// => 4

_.result(object, 'a.b.c', 'default');
// => 'default'

_.result(object, 'a.b.c', _.constant('default'));
// => 'default'
```

### _.set(object, path, value)

Sets the property value of `path` on `object`. If a portion of `path`
does not exist it's created.

#### Arguments
1. `object` *(Object)*: The object to augment.
2. `path` *(Array|string)*: The path of the property to set.
3. `value` *(&#42;)*: The value to set.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
var object = { 'a': [{ 'b': { 'c': 3 } }] };

_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4

_.set(object, 'x[0].y.z', 5);
console.log(object.x[0].y.z);
// => 5
```

### _.transform(object, [iteratee=_.identity], [accumulator], [thisArg])

An alternative to `_.reduce`; this method transforms `object` to a new
`accumulator` object which is the result of running each of its own enumerable
properties through `iteratee`, with each invocation potentially mutating
the `accumulator` object. The `iteratee` is bound to `thisArg` and invoked
with four arguments: (accumulator, value, key, object). Iteratee functions
may exit iteration early by explicitly returning `false`.

#### Arguments
1. `object` *(Array|Object)*: The object to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The function invoked per iteration.
3. `[accumulator]` *(&#42;)*: The custom accumulator value.
4. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(&#42;)*:  Returns the accumulated value.

#### Example
```js
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 == 0;
});
// => [4, 9]

_.transform({ 'a': 1, 'b': 2 }, function(result, n, key) {
  result[key] = n * 3;
});
// => { 'a': 3, 'b': 6 }
```

### _.values(object)

Creates an array of the own enumerable property values of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects.

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*:  Returns the array of property values.

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

### _.valuesIn(object)

Creates an array of the own and inherited enumerable property values
of `object`.
<br>
<br>
**Note:** Non-object values are coerced to objects.

#### Arguments
1. `object` *(Object)*: The object to query.

#### Returns
*(Array)*:  Returns the array of property values.

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

