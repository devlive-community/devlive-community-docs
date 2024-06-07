[TOC]

### keys

`_.keys(object)` [source](https://underscorejs.org/docs/modules/keys.html)  

Retrieve all the names of the **object**'s own enumerable properties.

```js
_.keys({one: 1, two: 2, three: 3});
=> ["one", "two", "three"]
```

### allKeys

`_.allKeys(object)` [source](https://underscorejs.org/docs/modules/allKeys.html)  

Retrieve _all_ the names of **object**'s own and inherited properties.

```js
function Stooge(name) {
this.name = name;
}
Stooge.prototype.silly = true;
_.allKeys(new Stooge("Moe"));
=> ["name", "silly"]
```

### values

`_.values(object)` [source](https://underscorejs.org/docs/modules/values.html)  

Return all of the values of the **object**'s own properties.

```js
_.values({one: 1, two: 2, three: 3});
=> [1, 2, 3]
```

### mapObject

`_.mapObject(object, iteratee, [context])` [source](https://underscorejs.org/docs/modules/mapObject.html)  

Like [map](#map), but for objects. Transform the value of each property in turn.

```js
_.mapObject({start: 5, end: 12}, function(val, key) {
return val + 5;
});
=> {start: 10, end: 17}
```

### pairs

`_.pairs(object)` [source](https://underscorejs.org/docs/modules/pairs.html)  

Convert an object into a list of \[key, value\] pairs. The opposite of [object](#object).

```js
_.pairs({one: 1, two: 2, three: 3});
=> [["one", 1], ["two", 2], ["three", 3]]
```

### invert

`_.invert(object)` [source](https://underscorejs.org/docs/modules/invert.html)  

Returns a copy of the **object** where the keys have become the values and the values the keys. For this to work, all of your object's values should be unique and string serializable.

```js
_.invert({Moe: "Moses", Larry: "Louis", Curly: "Jerome"});
=> {Moses: "Moe", Louis: "Larry", Jerome: "Curly"};
```

### create

`_.create(prototype, props)` [source](https://underscorejs.org/docs/modules/create.html)  

Creates a new object with the given prototype, optionally attaching **props** as _own_ properties. Basically, Object.create, but without all of the property descriptor jazz.

```js
var moe = _.create(Stooge.prototype, {name: "Moe"});
```

### functions

`_.functions(object)` Alias: **methods** [source](https://underscorejs.org/docs/modules/functions.html)  

Returns a sorted list of the names of every method in an object — that is to say, the name of every function property of the object.

```js
_.functions(_);
=> ["all", "any", "bind", "bindAll", "clone", "compact", "compose" ...
```

### findKey

`_.findKey(object, predicate, [context])` [source](https://underscorejs.org/docs/modules/findKey.html)  

Similar to [\_.findIndex](#findIndex) but for keys in objects. Returns the _key_ where the **predicate** truth test passes or _undefined_. **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

### extend

`_.extend(destination, *sources)` [source](https://underscorejs.org/docs/modules/extend.html)  

Shallowly copy all of the properties **in** the **source** objects over to the **destination** object, and return the **destination** object. Any nested objects or arrays will be copied by reference, not duplicated. It's in-order, so the last source will override properties of the same name in previous arguments.

```js
_.extend({name: 'moe'}, {age: 50});
=> {name: 'moe', age: 50}
```

### extendOwn

`_.extendOwn(destination, *sources)` Alias: **assign** [source](https://underscorejs.org/docs/modules/extendOwn.html)  

Like **extend**, but only copies _own_ properties over to the destination object.

### pick

`_.pick(object, *keys)` [source](https://underscorejs.org/docs/modules/pick.html)  

Return a copy of the **object**, filtered to only have values for the allowed **keys** (or array of valid keys). Alternatively accepts a predicate indicating which keys to pick.

```js
_.pick({name: 'moe', age: 50, userid: 'moe1'}, 'name', 'age');
=> {name: 'moe', age: 50}
_.pick({name: 'moe', age: 50, userid: 'moe1'}, function(value, key, object) {
return _.isNumber(value);
});
=> {age: 50}
```

### omit

`_.omit(object, *keys)` [source](https://underscorejs.org/docs/modules/omit.html)  

Return a copy of the **object**, filtered to omit the disallowed **keys** (or array of keys). Alternatively accepts a predicate indicating which keys to omit.

```js
_.omit({name: 'moe', age: 50, userid: 'moe1'}, 'userid');
=> {name: 'moe', age: 50}
_.omit({name: 'moe', age: 50, userid: 'moe1'}, function(value, key, object) {
return _.isNumber(value);
});
=> {name: 'moe', userid: 'moe1'}
```

### defaults

`_.defaults(object, *defaults)` [source](https://underscorejs.org/docs/modules/defaults.html)  

Returns **object** after filling in its undefined properties with the first value present in the following list of **defaults** objects.

```js
var iceCream = {flavor: "chocolate"};
_.defaults(iceCream, {flavor: "vanilla", sprinkles: "lots"});
=> {flavor: "chocolate", sprinkles: "lots"}
```

### clone

`_.clone(object)` [source](https://underscorejs.org/docs/modules/clone.html)  

Create a shallow-copied clone of the provided _plain_ **object**. Any nested objects or arrays will be copied by reference, not duplicated.

```js
_.clone({name: 'moe'});
=> {name: 'moe'};
```

### tap

`_.tap(object, interceptor)` [source](https://underscorejs.org/docs/modules/tap.html)  

Invokes **interceptor** with the **object**, and then returns **object**. The primary purpose of this method is to "tap into" a method chain, in order to perform operations on intermediate results within the chain.

```js
_.chain([1,2,3,200])
.filter(function(num) { return num % 2 == 0; })
.tap(alert)
.map(function(num) { return num * num })
.value();
=> // [2, 200] (alerted)
=> [4, 40000]
```

### toPath

`_.toPath(path)` [source](https://underscorejs.org/docs/modules/toPath.html)  

Ensures that **path** is an array. If **path** is a string, it is wrapped in a single-element array; if it is an array already, it is returned unmodified.

```js
_.toPath('key');
=> ['key']
_.toPath(['a', 0, 'b']);
=> ['a', 0, 'b'] // (same array)
```

`_.toPath` is used internally in `has`, `get`, `invoke`, `property`, `propertyOf` and `result`, as well as in [**iteratee**](#iteratee) and all functions that depend on it, in order to normalize deep property paths. You can override \_.toPath if you want to customize this behavior, for example to enable Lodash-like string path shorthands. Be advised that altering \_.toPath will unavoidably cause some keys to become unreachable; override at your own risk.

```js
// Support dotted path shorthands.
var originalToPath = _.toPath;
_.mixin({
toPath: function(path) {
return _.isString(path) ? path.split('.') : originalToPath(path);
}
});
_.get({a: [{b: 5}]}, 'a.0.b');
=> 5
```

### get

`_.get(object, path, [default])` [source](https://underscorejs.org/docs/modules/get.html)  

Returns the specified property of **object**. **path** may be specified as a simple key, or as an array of object keys or array indexes, for deep property fetching. If the property does not exist or is undefined, the optional **default** is returned.

```js
_.get({a: 10}, 'a');
=> 10
_.get({a: [{b: 2}]}, ['a', 0, 'b']);
=> 2
_.get({a: 10}, 'b', 100);
=> 100
```

### has

`_.has(object, key)` [source](https://underscorejs.org/docs/modules/has.html)  

Does the object contain the given key? Identical to object.hasOwnProperty(key), but uses a safe reference to the hasOwnProperty function, in case it's been [overridden accidentally](https://www.pixelstech.net/article/1326986170-An-Object-is-not-a-Hash).

```js
_.has({a: 1, b: 2, c: 3}, "b");
=> true
```

### property

`_.property(path)` [source](https://underscorejs.org/docs/modules/property.html)  

Returns a function that will return the specified property of any passed-in object. path may be specified as a simple key, or as an array of object keys or array indexes, for deep property fetching.

```js
var stooge = {name: 'moe'};
'moe' === _.property('name')(stooge);
=> true

var stooges = {moe: {fears: {worst: 'Spiders'}}, curly: {fears: {worst: 'Moe'}}};
var curlysWorstFear = _.property(['curly', 'fears', 'worst']);
curlysWorstFear(stooges);
=> 'Moe'
```

### propertyOf

`_.propertyOf(object)` [source](https://underscorejs.org/docs/modules/propertyOf.html)  

Inverse of _.property. Takes an object and returns a function which will return the value of a provided property.

```js
var stooge = {name: 'moe'};
_.propertyOf(stooge)('name');
=> 'moe'
```

### matcher

`_.matcher(attrs)` Alias: **matches** [source](https://underscorejs.org/docs/modules/matcher.html)  

Returns a predicate function that will tell you if a passed in object contains all of the key/value properties present in **attrs**.

```js
var ready = _.matcher({selected: true, visible: true});
var readyToGoList = _.filter(list, ready);
```

### isEqual

`_.isEqual(object, other)` [source](https://underscorejs.org/docs/modules/isEqual.html)  

Performs an optimized deep comparison between the two objects, to determine if they should be considered equal.

```js
var stooge = {name: 'moe', luckyNumbers: [13, 27, 34]};
var clone  = {name: 'moe', luckyNumbers: [13, 27, 34]};
stooge == clone;
=> false
_.isEqual(stooge, clone);
=> true
```

### isMatch

`_.isMatch(object, properties)` [source](https://underscorejs.org/docs/modules/isMatch.html)  

Tells you if the keys and values in **properties** are contained in **object**.

```js
var stooge = {name: 'moe', age: 32};
_.isMatch(stooge, {age: 32});
=> true
```

### isEmpty

`_.isEmpty(collection)` [source](https://underscorejs.org/docs/modules/isEmpty.html)  

Returns _true_ if **collection** has no elements. For strings and array-like objects \_.isEmpty checks if the length property is 0. For other objects, it returns _true_ if the object has no enumerable own-properties. Note that primitive numbers, booleans and symbols are always empty by this definition.

```js
_.isEmpty([1, 2, 3]);
=> false
_.isEmpty({});
=> true
```

### isElement

`_.isElement(object)` [source](https://underscorejs.org/docs/modules/isElement.html)  

Returns _true_ if **object** is a DOM element.

```js
_.isElement(jQuery('body')[0]);
=> true
```

### isArray

`_.isArray(object)` [source](https://underscorejs.org/docs/modules/isArray.html)  

Returns _true_ if **object** is an Array.

```js
(function(){ return _.isArray(arguments); })();
=> false
_.isArray([1,2,3]);
=> true
```

### isObject

`_.isObject(value)` [source](https://underscorejs.org/docs/modules/isObject.html)  

Returns _true_ if **value** is an Object. Note that JavaScript arrays and functions are objects, while (normal) strings and numbers are not.

```js
_.isObject({});
=> true
_.isObject(1);
=> false
```

### isArguments

`_.isArguments(object)` [source](https://underscorejs.org/docs/modules/isArguments.html)  

Returns _true_ if **object** is an Arguments object.

```js
(function(){ return _.isArguments(arguments); })(1, 2, 3);
=> true
_.isArguments([1,2,3]);
=> false
```

### isFunction

`_.isFunction(object)` [source](https://underscorejs.org/docs/modules/isFunction.html)  

Returns _true_ if **object** is a Function.

```js
_.isFunction(alert);
=> true
```

### isString

`_.isString(object)` [source](https://underscorejs.org/docs/modules/isString.html)  

Returns _true_ if **object** is a String.

```js
_.isString("moe");
=> true
```

### isNumber

`_.isNumber(object)` [source](https://underscorejs.org/docs/modules/isNumber.html)  

Returns _true_ if **object** is a Number (including NaN).

```js
_.isNumber(8.4 * 5);
=> true
```

### isFinite

`_.isFinite(object)` [source](https://underscorejs.org/docs/modules/isFinite.html)  

Returns _true_ if **object** is a finite Number.

```js
_.isFinite(-101);
=> true

_.isFinite(-Infinity);
=> false
```

### isBoolean

`_.isBoolean(object)` [source](https://underscorejs.org/docs/modules/isBoolean.html)  

Returns _true_ if **object** is either _true_ or _false_.

```js
_.isBoolean(null);
=> false
```

### isDate

`_.isDate(object)` [source](https://underscorejs.org/docs/modules/isDate.html)  

Returns _true_ if **object** is a Date.

```js
_.isDate(new Date());
=> true
```

### isRegExp

`_.isRegExp(object)` [source](https://underscorejs.org/docs/modules/isRegExp.html)  

Returns _true_ if **object** is a RegExp.

```js
_.isRegExp(/moe/);
=> true
```

### isError

`_.isError(object)` [source](https://underscorejs.org/docs/modules/isError.html)  

Returns _true_ if **object** inherits from an Error.

```js
try {
  throw new TypeError("Example");
} catch (o_O) {
  _.isError(o_O);
}
=> true
```

### isSymbol

`_.isSymbol(object)` [source](https://underscorejs.org/docs/modules/isSymbol.html)  

Returns _true_ if **object** is a [Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol).

```js
_.isSymbol(Symbol());
=> true
```

### isMap

`_.isMap(object)` [source](https://underscorejs.org/docs/modules/isMap.html)  

Returns _true_ if **object** is a [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map).

```js
_.isMap(new Map());
=> true
```

### isWeakMap

`_.isWeakMap(object)` [source](https://underscorejs.org/docs/modules/isWeakMap.html)  

Returns _true_ if **object** is a [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap).

```js
_.isWeakMap(new WeakMap());
=> true
```

### isSet

`_.isSet(object)` [source](https://underscorejs.org/docs/modules/isSet.html)  

Returns _true_ if **object** is a [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set).

```js
_.isSet(new Set());
=> true
```

### isWeakSet

`_.isWeakSet(object)` [source](https://underscorejs.org/docs/modules/isWeakSet.html)  

Returns _true_ if **object** is a [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet).

```js
_.isWeakSet(WeakSet());
=> true
```

### isArrayBuffer

`_.isArrayBuffer(object)` [source](https://underscorejs.org/docs/modules/isArrayBuffer.html)  

Returns _true_ if **object** is an [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer).

```js
_.isArrayBuffer(new ArrayBuffer(8));
=> true
```

### isDataView

`_.isDataView(object)` [source](https://underscorejs.org/docs/modules/isDataView.html)  

Returns _true_ if **object** is a [DataView](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView).

```js
_.isDataView(new DataView(new ArrayBuffer(8)));
=> true
```

### isTypedArray

`_.isTypedArray(object)` [source](https://underscorejs.org/docs/modules/isTypedArray.html)  

Returns _true_ if **object** is a [TypedArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray).

```js
_.isTypedArray(new Int8Array(8));
=> true
```

### isNaN

`_.isNaN(object)` [source](https://underscorejs.org/docs/modules/isNaN.html)  

Returns _true_ if **object** is _NaN_.  

Note: this is not the same as the native **isNaN** function, which will also return true for many other not-number values, such as undefined.

```js
_.isNaN(NaN);
=> true
isNaN(undefined);
=> true
_.isNaN(undefined);
=> false
```

### isNull

`_.isNull(object)` [source](https://underscorejs.org/docs/modules/isNull.html)  

Returns _true_ if the value of **object** is _null_.

```js
_.isNull(null);
=> true
_.isNull(undefined);
=> false
```

### isUndefined

`_.isUndefined(value)` [source](https://underscorejs.org/docs/modules/isUndefined.html)  

Returns _true_ if **value** is _undefined_.

```js
_.isUndefined(window.missingVariable);
=> true
```
