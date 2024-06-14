[TOC]

### _.add(augend, addend)

Adds two numbers.

#### Arguments
1. `augend` *(number)*: The first number to add.
2. `addend` *(number)*: The second number to add.

#### Returns
*(number)*:  Returns the sum.

#### Example
```js
_.add(6, 4);
// => 10
```

### _.ceil(n, [precision=0])

Calculates `n` rounded up to `precision`.

#### Arguments
1. `n` *(number)*: The number to round up.
2. `[precision=0]` *(number)*: The precision to round up to.

#### Returns
*(number)*:  Returns the rounded up number.

#### Example
```js
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

### _.floor(n, [precision=0])

Calculates `n` rounded down to `precision`.

#### Arguments
1. `n` *(number)*: The number to round down.
2. `[precision=0]` *(number)*: The precision to round down to.

#### Returns
*(number)*:  Returns the rounded down number.

#### Example
```js
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

### _.max(collection, [iteratee], [thisArg])

Gets the maximum value of `collection`. If `collection` is empty or falsey
`-Infinity` is returned. If an iteratee function is provided it's invoked
for each value in `collection` to generate the criterion by which the value
is ranked. The `iteratee` is bound to `thisArg` and invoked with three
arguments: (value, index, collection).
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
2. `[iteratee]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(&#42;)*:  Returns the maximum value.

#### Example
```js
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => -Infinity

var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

_.max(users, function(chr) {
  return chr.age;
});
// => { 'user': 'fred', 'age': 40 }

// using the `_.property` callback shorthand
_.max(users, 'age');
// => { 'user': 'fred', 'age': 40 }
```

### _.min(collection, [iteratee], [thisArg])

Gets the minimum value of `collection`. If `collection` is empty or falsey
`Infinity` is returned. If an iteratee function is provided it's invoked
for each value in `collection` to generate the criterion by which the value
is ranked. The `iteratee` is bound to `thisArg` and invoked with three
arguments: (value, index, collection).
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
2. `[iteratee]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(&#42;)*:  Returns the minimum value.

#### Example
```js
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => Infinity

var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];

_.min(users, function(chr) {
  return chr.age;
});
// => { 'user': 'barney', 'age': 36 }

// using the `_.property` callback shorthand
_.min(users, 'age');
// => { 'user': 'barney', 'age': 36 }
```

### _.round(n, [precision=0])

Calculates `n` rounded to `precision`.

#### Arguments
1. `n` *(number)*: The number to round.
2. `[precision=0]` *(number)*: The precision to round to.

#### Returns
*(number)*:  Returns the rounded number.

#### Example
```js
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

### _.sum(collection, [iteratee], [thisArg])

Gets the sum of the values in `collection`.

#### Arguments
1. `collection` *(Array|Object|string)*: The collection to iterate over.
2. `[iteratee]` *(Function|Object|string)*: The function invoked per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `iteratee`.

#### Returns
*(number)*:  Returns the sum.

#### Example
```js
_.sum([4, 6]);
// => 10

_.sum({ 'a': 4, 'b': 6 });
// => 10

var objects = [
  { 'n': 4 },
  { 'n': 6 }
];

_.sum(objects, function(object) {
  return object.n;
});
// => 10

// using the `_.property` callback shorthand
_.sum(objects, 'n');
// => 10
```
