[TOC]

### clone

-------------------------------------------------------------------------------------------------------------

`{*} → {*}`

Parameters

*   valueThe object or array to clone

> Returns * A deeply cloned copy of `val`

Added in v0.1.0

Creates a deep copy of the source that can be used in place of the source object without retaining any references to it. The source object may contain (nested) `Array`s and `Object`s, `Number`s, `String`s, `Boolean`s and `Date`s. `Function`s are assigned by reference rather than copied.

Dispatches to a `clone` method if present.

Note that if the source object has multiple nodes that share a reference, the returned object will have the same structure, but the references will be pointed to the location within the cloned value.

```js
const objects = [{}, {}, {}];
const objectsClone = R.clone(objects);
objects === objectsClone; //=> false
objects[0] === objectsClone[0]; //=> false
```

### values

----------------------------------------------------------------------------------------------------------------

`{k: v} → [v]`

Parameters

*   objThe object to extract values from

> Returns Array An array of the values of the object's own properties.

Added in v0.1.0

Returns a list of all the enumerable own properties of the supplied object. Note that the order of the output array is not guaranteed across different JS platforms.

See also [valuesIn](#valuesIn), [keys](#keys), [toPairs](#toPairs).

```js
R.values({a: 1, b: 2, c: 3}); //=> [1, 2, 3]
```

### eqProps

-------------------------------------------------------------------------------------------------------------------

`k → {k: v} → {k: v} → Boolean`

Parameters

*   propThe name of the property to compare
*   obj1
*   obj2

> Returns Boolean

Added in v0.1.0

Reports whether two objects have the same value, in [`R.equals`](#equals) terms, for the specified property. Useful as a curried predicate.

```js
const o1 = { a: 1, b: 2, c: 3, d: 4 };
const o2 = { a: 10, b: 20, c: 3, d: 40 };
R.eqProps('a', o1, o2); //=> false
R.eqProps('c', o1, o2); //=> true
```

### keys

----------------------------------------------------------------------------------------------------------

`{k: v} → [k]`

Parameters

*   objThe object to extract properties from

> Returns Array An array of the object's own properties.

Added in v0.1.0

Returns a list containing the names of all the enumerable own properties of the supplied object. Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

See also [keysIn](#keysIn), [values](#values), [toPairs](#toPairs).

```js
R.keys({a: 1, b: 2, c: 3}); //=> ['a', 'b', 'c']
```

### omit

----------------------------------------------------------------------------------------------------------

`[String] → {String: *} → {String: *}`

Parameters

*   namesan array of String property names to omit from the new object
*   objThe object to copy from

> Returns Object A new object with properties from `names` not on it.

Added in v0.1.0

Returns a partial copy of an object omitting the keys specified.

See also [pick](#pick).

```js
R.omit(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, c: 3}
```

### pick

----------------------------------------------------------------------------------------------------------

`[k] → {k: v} → {k: v}`

Parameters

*   namesan array of String property names to copy onto a new object
*   objThe object to copy from

> Returns Object A new object with only properties from `names` on it.

Added in v0.1.0

Returns a partial copy of an object containing only the keys specified. If the key does not exist, the property is ignored.

See also [omit](#omit), [props](#props).

```js
R.pick(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1, d: 4}
R.pick(['a', 'e', 'f'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1}
```

### pickAll

-------------------------------------------------------------------------------------------------------------------

`[k] → {k: v} → {k: v}`

Parameters

*   namesan array of String property names to copy onto a new object
*   objThe object to copy from

> Returns Object A new object with only properties from `names` on it.

Added in v0.1.0

Similar to `pick` except that this one includes a `key: undefined` pair for properties that don't exist.

See also [pick](#pick).

```js
R.pickAll(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1, d: 4}
R.pickAll(['a', 'e', 'f'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1, e: undefined, f: undefined}
```

### project

---

`[k] → [{k: v}] → [{k: v}]`

Parameters

*   propsThe property names to project
*   objsThe objects to query

> Returns Array An array of objects with just the `props` properties.

Added in v0.1.0

Reasonable analog to SQL `select` statement.

See also [pluck](#pluck), [props](#props), [prop](#prop).

```js
const abby = {name: 'Abby', age: 7, hair: 'blond', grade: 2};
const fred = {name: 'Fred', age: 12, hair: 'brown', grade: 7};
const kids = [abby, fred];
R.project(['name', 'grade'], kids); //=> [{name: 'Abby', grade: 2}, {name: 'Fred', grade: 7}]
```

### prop

---

`Idx → {s: a} → a | Undefined`

`Idx = String | Int | Symbol`

Parameters

*   pThe property name or array index
*   objThe object to query

> Returns * The value at `obj.p`.

Added in v0.1.0

Returns a function that when supplied an object returns the indicated property of that object, if it exists.

See also [path](#path), [props](#props), [pluck](#pluck), [project](#project), [nth](#nth).

```js
R.prop('x', {x: 100}); //=> 100
R.prop('x', {}); //=> undefined
R.prop(0, [100]); //=> 100
R.compose(R.inc, R.prop('x'))({ x: 3 }) //=> 4
```

### props

---

`[k] → {k: v} → [v]`

Parameters

*   psThe property names to fetch
*   objThe object to query

> Returns Array The corresponding values or partially applied function.

Added in v0.1.0

Acts as multiple `prop`: array of keys in, array of values out. Preserves order.

See also [prop](#prop), [pluck](#pluck), [project](#project).

```js
R.props(['x', 'y'], {x: 1, y: 2}); //=> [1, 2]
R.props(['c', 'a', 'b'], {b: 2, a: 1}); //=> [undefined, 1, 2]

const fullName = R.compose(R.join(' '), R.props(['first', 'last']));
fullName({last: 'Bullet-Tooth', age: 33, first: 'Tony'}); //=> 'Tony Bullet-Tooth'
```

### keysIn

---

`{k: v} → [k]`

Parameters

*   objThe object to extract properties from

> Returns Array An array of the object's own and prototype properties.

Added in v0.2.0

Returns a list containing the names of all the properties of the supplied object, including prototype properties. Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

See also [keys](#keys), [valuesIn](#valuesIn).

```js
const F = function() { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.keysIn(f); //=> ['x', 'y']
```

### path

---

`[Idx] → {a} → a | Undefined`

`Idx = String | NonNegativeInt`

`Idx = String | Int | Symbol`

Parameters

*   pathThe path to use.
*   objThe object or array to retrieve the nested property from.

> Returns * The data at `path`.

Added in v0.2.0

Retrieves the value at a given path. The nodes of the path can be arbitrary strings or non-negative integers. For anything else, the value is unspecified. Integer paths are meant to index arrays, strings are meant for objects.

See also [prop](#prop), [nth](#nth), [assocPath](#assocPath), [dissocPath](#dissocPath).

```js
R.path(['a', 'b'], {a: {b: 2}}); //=> 2
R.path(['a', 'b'], {c: {b: 2}}); //=> undefined
R.path(['a', 'b', 0], {a: {b: [1, 2, 3]}}); //=> 1
R.path(['a', 'b', -2], {a: {b: [1, 2, 3]}}); //=> 2
R.path([2], {'2': 2}); //=> 2
R.path([-2], {'-2': 'a'}); //=> undefined
```

### valuesIn

---

`{k: v} → [v]`

Parameters

*   objThe object to extract values from

> Returns Array An array of the values of the object's own and prototype properties.

Added in v0.2.0

Returns a list of all the properties, including prototype properties, of the supplied object. Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

See also [values](#values), [keysIn](#keysIn).

```js
const F = function() { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.valuesIn(f); //=> ['X', 'Y']
```

### toPairs

---

`{String: *} → [[String,*]]`

Parameters

*   objThe object to extract from

> Returns Array An array of key, value arrays from the object's own properties.

Added in v0.4.0

Converts an object into an array of key, value arrays. Only the object's own properties are used. Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

See also [fromPairs](#fromPairs), [keys](#keys), [values](#values).

```js
R.toPairs({a: 1, b: 2, c: 3}); //=> [['a', 1], ['b', 2], ['c', 3]]
```

### toPairsIn

---

`{String: *} → [[String,*]]`

Parameters

*   objThe object to extract from

> Returns Array An array of key, value arrays from the object's own and prototype properties.

Added in v0.4.0

Converts an object into an array of key, value arrays. The object's own properties and prototype properties are used. Note that the order of the output array is not guaranteed to be consistent across different JS platforms.

```js
const F = function() { this.x = 'X'; };
F.prototype.y = 'Y';
const f = new F();
R.toPairsIn(f); //=> [['x','X'], ['y','Y']]
```

### propOr

---

`a → String → Object → a`

Parameters

*   valThe default value.
*   pThe name of the property to return.
*   objThe object to query.

> Returns * The value of given property of the supplied object or the default value.

Added in v0.6.0

Return the specified property of the given non-null object if the property is present and it's value is not `null`, `undefined` or `NaN`.

Otherwise the first argument is returned.

```js
const alice = {
    name: 'ALICE',
    age: 101
};
const favorite = R.prop('favoriteLibrary');
const favoriteWithDefault = R.propOr('Ramda', 'favoriteLibrary');

favorite(alice);  //=> undefined
favoriteWithDefault(alice);  //=> 'Ramda'
```

### has

---

`s → {s: x} → Boolean`

Parameters

*   propThe name of the property to check for.
*   objThe object to query.

> Returns Boolean Whether the property exists.

Added in v0.7.0

Returns whether or not an object has an own property with the specified name

```js
const hasName = R.has('name');
hasName({name: 'alice'});   //=> true
hasName({name: 'bob'});     //=> true
hasName({});                //=> false

const point = {x: 0, y: 0};
const pointHas = R.has(R.__, point);
pointHas('x');  //=> true
pointHas('y');  //=> true
pointHas('z');  //=> false
```

### hasIn

---

`s → {s: x} → Boolean`

Parameters

*   propThe name of the property to check for.
*   objThe object to query.

> Returns Boolean Whether the property exists.

Added in v0.7.0

Returns whether or not an object or its prototype chain has a property with the specified name

```js
function Rectangle(width, height) {
    this.width = width;
    this.height = height;
}
Rectangle.prototype.area = function() {
    return this.width * this.height;
};

const square = new Rectangle(2, 2);
R.hasIn('width', square);  //=> true
R.hasIn('area', square);  //=> true
```

### assoc

---

`Idx → a → {k: v} → {k: v}`

`Idx = String | Int`

Parameters

*   propThe property name to set
*   valThe new value
*   objThe object to clone

> Returns Object A new object equivalent to the original except for the changed property.

Added in v0.8.0

Makes a shallow clone of an object, setting or overriding the specified property with the given value. Note that this copies and flattens prototype properties onto the new object as well. All non-primitive properties are copied by reference.

See also [dissoc](#dissoc), [pick](#pick).

```js
R.assoc('c', 3, {a: 1, b: 2}); //=> {a: 1, b: 2, c: 3}
```

### assocPath

---

`[Idx] → a → {a} → {a}`

`Idx = String | Int | Symbol`

Parameters

*   paththe path to set
*   valThe new value
*   objThe object to clone

> Returns Object A new object equivalent to the original except along the specified path.

Added in v0.8.0

Makes a shallow clone of an object, setting or overriding the nodes required to create the given path, and placing the specific value at the tail end of that path. Note that this copies and flattens prototype properties onto the new object as well. All non-primitive properties are copied by reference.

See also [dissocPath](#dissocPath).

```js
R.assocPath(['a', 'b', 'c'], 42, {a: {b: {c: 0}}}); //=> {a: {b: {c: 42}}}

// Any missing or non-object keys in path will be overridden
R.assocPath(['a', 'b', 'c'], 42, {a: 5}); //=> {a: {b: {c: 42}}}
```

### lens

---

`(s → a) → ((a, s) → s) → Lens s a`

`Lens s a = Functor f => (a → f a) → s → f s`

Parameters

*   getter
*   setter

> Returns Lens

Added in v0.8.0

Returns a lens for the given getter and setter functions. The getter "gets" the value of the focus; the setter "sets" the value of the focus. The setter should not mutate the data structure.

See also [view](#view), [set](#set), [over](#over), [lensIndex](#lensIndex), [lensProp](#lensProp).

```js
const xLens = R.lens(R.prop('x'), R.assoc('x'));

R.view(xLens, {x: 1, y: 2});            //=> 1
R.set(xLens, 4, {x: 1, y: 2});          //=> {x: 4, y: 2}
R.over(xLens, R.negate, {x: 1, y: 2});  //=> {x: -1, y: 2}
```

### pickBy

---

`((v, k) → Boolean) → {k: v} → {k: v}`

Parameters

*   predA predicate to determine whether or not a key should be included on the output object.
*   objThe object to copy from

> Returns Object A new object with only properties that satisfy `pred` on it.

Added in v0.8.0

Returns a partial copy of an object containing only the keys that satisfy the supplied predicate.

See also [pick](#pick), [filter](#filter).

```js
const isUpperCase = (val, key) => key.toUpperCase() === key;
R.pickBy(isUpperCase, {a: 1, b: 2, A: 3, B: 4}); //=> {A: 3, B: 4}
```

### evolve

---

`{k: (v → v)} → {k: v} → {k: v}`

Parameters

*   transformationsThe object specifying transformation functions to apply to the object.
*   objectThe object to be transformed.

> Returns Object The transformed object.

Added in v0.9.0

Creates a new object by recursively evolving a shallow copy of `object`, according to the `transformation` functions. All non-primitive properties are copied by reference.

A `transformation` function will not be invoked if its corresponding key does not exist in the evolved object.

```js
const tomato = {firstName: '  Tomato ', data: {elapsed: 100, remaining: 1400}, id:123};
const transformations = {
    firstName: R.trim,
    lastName: R.trim, // Will not get invoked.
    data: {elapsed: R.add(1), remaining: R.add(-1)}
};
R.evolve(transformations, tomato); //=> {firstName: 'Tomato', data: {elapsed: 101, remaining: 1399}, id:123}
```

### invert

---

`{s: x} → {x: [ s, … ]}`

Parameters

*   objThe object or array to invert

> Returns Object out A new object with keys in an array.

Added in v0.9.0

Same as [`R.invertObj`](#invertObj), however this accounts for objects with duplicate values by putting the values into an array.

See also [invertObj](#invertObj).

```js
const raceResultsByFirstName = {
    first: 'alice',
    second: 'jake',
    third: 'alice',
};
R.invert(raceResultsByFirstName);
//=> { 'alice': ['first', 'third'], 'jake':['second'] }
```

### invertObj

---

`{s: x} → {x: s}`

Parameters

*   objThe object or array to invert

> Returns Object out A new object

Added in v0.9.0

Returns a new object with the keys of the given object as values, and the values of the given object, which are coerced to strings, as keys. Note that the last key found is preferred when handling the same value.

See also [invert](#invert).

```js
const raceResults = {
    first: 'alice',
    second: 'jake'
};
R.invertObj(raceResults);
//=> { 'alice': 'first', 'jake':'second' }

// Alternatively:
const raceResults = ['alice', 'jake'];
R.invertObj(raceResults);
//=> { 'alice': '0', 'jake':'1' }
```

### mapObjIndexed

---

`((*, String, Object) → *) → Object → Object`

Added in v0.9.0

An Object-specific version of [`map`](#map). The function is applied to three arguments: _(value, key, obj)_. If only the value is significant, use [`map`](#map) instead.

See also [map](#map).

```js
const xyz = { x: 1, y: 2, z: 3 };
const prependKeyAndDouble = (num, key, obj) => key + (num * 2);

R.mapObjIndexed(prependKeyAndDouble, xyz); //=> { x: 'x2', y: 'y4', z: 'z6' }
```

### dissoc

---

`String → {k: v} → {k: v}`

Parameters

*   propThe name of the property to dissociate
*   objThe object to clone

> Returns Object A new object equivalent to the original but without the specified property

Added in v0.10.0

Returns a new object that does not contain a `prop` property.

See also [assoc](#assoc), [omit](#omit).

```js
R.dissoc('b', {a: 1, b: 2, c: 3}); //=> {a: 1, c: 3}
```

### dissocPath

---

`[Idx] → {k: v} → {k: v}`

`Idx = String | Int | Symbol`

Parameters

*   pathThe path to the value to omit
*   objThe object to clone

> Returns Object A new object without the property at path

Added in v0.11.0

Makes a shallow clone of an object, omitting the property at the given path. Note that this copies and flattens prototype properties onto the new object as well. All non-primitive properties are copied by reference.

See also [assocPath](#assocPath).

```js
R.dissocPath(['a', 'b', 'c'], {a: {b: {c: 42}}}); //=> {a: {b: {}}}
```

### lensIndex

---

`Number → Lens s a`

`Lens s a = Functor f => (a → f a) → s → f s`

Added in v0.14.0

Returns a lens whose focus is the specified index.

See also [view](#view), [set](#set), [over](#over), [nth](#nth).

```js
const headLens = R.lensIndex(0);

R.view(headLens, ['a', 'b', 'c']);            //=> 'a'
R.set(headLens, 'x', ['a', 'b', 'c']);        //=> ['x', 'b', 'c']
R.over(headLens, R.toUpper, ['a', 'b', 'c']); //=> ['A', 'b', 'c']
```

### lensProp

---

`String → Lens s a`

`Lens s a = Functor f => (a → f a) → s → f s`

Added in v0.14.0

Returns a lens whose focus is the specified property.

See also [view](#view), [set](#set), [over](#over).

```js
const xLens = R.lensProp('x');

R.view(xLens, {x: 1, y: 2});            //=> 1
R.set(xLens, 4, {x: 1, y: 2});          //=> {x: 4, y: 2}
R.over(xLens, R.negate, {x: 1, y: 2});  //=> {x: -1, y: 2}
```

### whereEq

---

`{String: *} → {String: *} → Boolean`

Parameters

*   spec
*   testObj

> Returns Boolean

Added in v0.14.0

Takes a spec object and a test object; returns true if the test satisfies the spec, false otherwise. An object satisfies the spec if, for each of the spec's own properties, accessing that property of the object gives the same value (in [`R.equals`](#equals) terms) as accessing that property of the spec.

`whereEq` is a specialization of [`where`](#where).

See also [propEq](#propEq), [where](#where).

```js
// pred :: Object -> Boolean
const pred = R.whereEq({a: 1, b: 2});

pred({a: 1});              //=> false
pred({a: 1, b: 2});        //=> true
pred({a: 1, b: 2, c: 3});  //=> true
pred({a: 1, b: 1});        //=> false
```

### over

---

`Lens s a → (a → a) → s → s`

`Lens s a = Functor f => (a → f a) → s → f s`

Added in v0.16.0

Returns the result of "setting" the portion of the given data structure focused by the given lens to the result of applying the given function to the focused value.

See also [view](#view), [set](#set), [lens](#lens), [lensIndex](#lensIndex), [lensProp](#lensProp), [lensPath](#lensPath).

```js
const headLens = R.lensIndex(0);

R.over(headLens, R.toUpper, ['foo', 'bar', 'baz']); //=> ['FOO', 'bar', 'baz']
```

### set

---

`Lens s a → a → s → s`

`Lens s a = Functor f => (a → f a) → s → f s`

Added in v0.16.0

Returns the result of "setting" the portion of the given data structure focused by the given lens to the given value.

See also [view](#view), [over](#over), [lens](#lens), [lensIndex](#lensIndex), [lensProp](#lensProp), [lensPath](#lensPath).

```js
const xLens = R.lensProp('x');

R.set(xLens, 4, {x: 1, y: 2});  //=> {x: 4, y: 2}
R.set(xLens, 8, {x: 1, y: 2});  //=> {x: 8, y: 2}
```

### view

---

`Lens s a → s → a`

`Lens s a = Functor f => (a → f a) → s → f s`

Added in v0.16.0

Returns a "view" of the given data structure, determined by the given lens. The lens's focus determines which portion of the data structure is visible.

See also [set](#set), [over](#over), [lens](#lens), [lensIndex](#lensIndex), [lensProp](#lensProp), [lensPath](#lensPath).

```js
const xLens = R.lensProp('x');

R.view(xLens, {x: 1, y: 2});  //=> 1
R.view(xLens, {x: 4, y: 2});  //=> 4
```

### objOf

---

`String → a → {String:a}`

Added in v0.18.0

Creates an object containing a single key:value pair.

See also [pair](#pair).

```js
const matchPhrases = R.compose(
  R.objOf('must'),
  R.map(R.objOf('match_phrase'))
);
matchPhrases(['foo', 'bar', 'baz']); //=> {must: [{match_phrase: 'foo'}, {match_phrase: 'bar'}, {match_phrase: 'baz'}]}
```

### pathOr

---

`a → [Idx] → {a} → a`

`Idx = String | Int | Symbol`

Parameters

*   dThe default value.
*   pThe path to use.
*   objThe object to retrieve the nested property from.

> Returns * The data at `path` of the supplied object or the default value.

Added in v0.18.0

If the given, non-null object has a value at the given path, returns the value at that path. Otherwise returns the provided default value.

```js
R.pathOr('N/A', ['a', 'b'], {a: {b: 2}}); //=> 2
R.pathOr('N/A', ['a', 'b'], {c: {b: 2}}); //=> "N/A"
```

### lensPath

---

`[Idx] → Lens s a`

`Idx = String | Int | Symbol`

`Lens s a = Functor f => (a → f a) → s → f s`

Parameters

*   pathThe path to use.

> Returns Lens

Added in v0.19.0

Returns a lens whose focus is the specified path.

See also [view](#view), [set](#set), [over](#over).

```js
const xHeadYLens = R.lensPath(['x', 0, 'y']);

R.view(xHeadYLens, {x: [{y: 2, z: 3}, {y: 4, z: 5}]});
//=> 2
R.set(xHeadYLens, 1, {x: [{y: 2, z: 3}, {y: 4, z: 5}]});
//=> {x: [{y: 1, z: 3}, {y: 4, z: 5}]}
R.over(xHeadYLens, R.negate, {x: [{y: 2, z: 3}, {y: 4, z: 5}]});
//=> {x: [{y: -2, z: 3}, {y: 4, z: 5}]}
```

### mergeWith

---

`((a, a) → a) → {a} → {a} → {a}`

Added in v0.19.0

Creates a new object with the own properties of the two provided objects. If a key exists in both objects, the provided function is applied to the values associated with the key in each object, with the result being used as the value associated with the key in the returned object.

See also [mergeDeepWith](#mergeDeepWith), [merge](#merge), [mergeWithKey](#mergeWithKey).

```js
R.mergeWith(R.concat,
            { a: true, values: [10, 20] },
            { b: true, values: [15, 35] });
//=> { a: true, b: true, values: [10, 20, 15, 35] }
```

### mergeWithKey

---

`((String, a, a) → a) → {a} → {a} → {a}`

Added in v0.19.0

Creates a new object with the own properties of the two provided objects. If a key exists in both objects, the provided function is applied to the key and the values associated with the key in each object, with the result being used as the value associated with the key in the returned object.

See also [mergeDeepWithKey](#mergeDeepWithKey), [merge](#merge), [mergeWith](#mergeWith).

```js
let concatValues = (k, l, r) => k == 'values' ? R.concat(l, r) : r
R.mergeWithKey(concatValues,
               { a: true, thing: 'foo', values: [10, 20] },
               { b: true, thing: 'bar', values: [15, 35] });
//=> { a: true, b: true, thing: 'bar', values: [10, 20, 15, 35] }
```

### forEachObjIndexed

---

`((a, String, StrMap a) → Any) → StrMap a → StrMap a`

Parameters

*   fnThe function to invoke. Receives three argument, `value`, `key`, `obj`.
*   objThe object to iterate over.

> Returns Object The original object.

Added in v0.23.0

Iterate over an input `object`, calling a provided function `fn` for each key and value in the object.

`fn` receives three argument: _(value, key, obj)_.

```js
const printKeyConcatValue = (value, key) => console.log(key + ':' + value);
R.forEachObjIndexed(printKeyConcatValue, {x: 1, y: 2}); //=> {x: 1, y: 2}
// logs x:1
// logs y:2
```


