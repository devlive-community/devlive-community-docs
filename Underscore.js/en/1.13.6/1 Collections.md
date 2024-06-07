[TOC]

### each

`_.each(list, iteratee, [context])` Alias: **forEach** [source](https://underscorejs.org/docs/modules/each.html)  

Iterates over a **list** of elements, yielding each in turn to an **iteratee** function. The **iteratee** is bound to the **context** object, if one is passed. Each invocation of **iteratee** is called with three arguments: `(element, index, list)`. If **list** is a JavaScript object, **iteratee**'s arguments will be `(value, key, list)`. Returns the **list** for chaining.

```js
_.each([1, 2, 3], alert);
=> alerts each number in turn...
_.each({one: 1, two: 2, three: 3}, alert);
=> alerts each number value in turn...
```

_Note: Collection functions work on arrays, objects, and array-like objects such as_ `arguments`, `NodeList` _and similar. But it works by duck-typing, so avoid passing objects with a numeric `length` property. It's also good to note that an `each` loop cannot be broken out of — to break, use **\_.find** instead._

### map

`_.map(list, iteratee, [context])` Alias: **collect** [source](https://underscorejs.org/docs/modules/map.html)  

Produces a new array of values by mapping each value in **list** through a transformation function ([**iteratee**](#iteratee)). The iteratee is passed three arguments: the `value`, then the `index` (or `key`) of the iteration, and finally a reference to the entire `list`.

```js
_.map([1, 2, 3], function(num){ return num * 3; });
=> [3, 6, 9]
_.map({one: 1, two: 2, three: 3}, function(num, key){ return num * 3; });
=> [3, 6, 9]
_.map([[1, 2], [3, 4]], _.first);
=> [1, 3]
```

### reduce

`_.reduce(list, iteratee, [memo], [context])` Aliases: **inject**, **foldl** [source](https://underscorejs.org/docs/modules/reduce.html)  

Also known as **inject** and **foldl**, reduce boils down a **list** of values into a single value. **Memo** is the initial state of the reduction, and each successive step of it should be returned by **iteratee**. The iteratee is passed four arguments: the `memo`, then the `value` and `index` (or key) of the iteration, and finally a reference to the entire `list`.

If no memo is passed to the initial invocation of reduce, the iteratee is not invoked on the first element of the list. The first element is instead passed as the memo in the invocation of the iteratee on the next element in the list.

```js
var sum = _.reduce([1, 2, 3], function(memo, num){ return memo + num; }, 0);
=> 6
```

### reduceRight

`_.reduceRight(list, iteratee, [memo], [context])` Alias: **foldr** [source](https://underscorejs.org/docs/modules/reduceRight.html)  

The right-associative version of **reduce**. **Foldr** is not as useful in JavaScript as it would be in a language with lazy evaluation.

```js
var list = [[0, 1], [2, 3], [4, 5]];
var flat = _.reduceRight(list, function(a, b) { return a.concat(b); }, []);
=> [4, 5, 2, 3, 0, 1]
```

### find

`_.find(list, predicate, [context])` Alias: **detect** [source](https://underscorejs.org/docs/modules/find.html)  

Looks through each value in the **list**, returning the first one that passes a truth test (**predicate**), or `undefined` if no value passes the test. The function returns as soon as it finds an acceptable element, and doesn't traverse the entire list. **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

```js
var even = _.find([1, 2, 3, 4, 5, 6], function(num){ return num % 2 == 0; });
=> 2
```

### filter

`_.filter(list, predicate, [context])` Alias: **select** [source](https://underscorejs.org/docs/modules/filter.html)  

Looks through each value in the **list**, returning an array of all the values that pass a truth test (**predicate**). **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

```js
var evens = _.filter([1, 2, 3, 4, 5, 6], function(num){ return num % 2 == 0; });
=> [2, 4, 6]
```

### findWhere

`_.findWhere(list, properties)` [source](https://underscorejs.org/docs/modules/findWhere.html)  

Looks through the **list** and returns the _first_ value that [matches](#matches) all of the key-value pairs listed in **properties**.

If no match is found, or if **list** is empty, _undefined_ will be returned.

```js
_.findWhere(publicServicePulitzers, {newsroom: "The New York Times"});
=> {year: 1918, newsroom: "The New York Times",
reason: "For its public service in publishing in full so many official reports,
documents and speeches by European statesmen relating to the progress and
conduct of the war."}
```

### where

`_.where(list, properties)` [source](https://underscorejs.org/docs/modules/where.html)  

Looks through each value in the **list**, returning an array of all the values that [matches](#matches) the key-value pairs listed in **properties**.

```js
_.where(listOfPlays, {author: "Shakespeare", year: 1611});
=> [{title: "Cymbeline", author: "Shakespeare", year: 1611},
{title: "The Tempest", author: "Shakespeare", year: 1611}]
```

### reject

`_.reject(list, predicate, [context])` [source](https://underscorejs.org/docs/modules/reject.html)  

Returns the values in **list** without the elements that the truth test (**predicate**) passes. The opposite of **filter**. **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

```js
var odds = _.reject([1, 2, 3, 4, 5, 6], function(num){ return num % 2 == 0; });
=> [1, 3, 5]
```

### every

`_.every(list, [predicate], [context])` Alias: **all** [source](https://underscorejs.org/docs/modules/every.html)  

Returns _true_ if all of the values in the **list** pass the **predicate** truth test. Short-circuits and stops traversing the list if a false element is found. **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

```js
_.every([2, 4, 5], function(num) { return num % 2 == 0; });
=> false
```

### some

`_.some(list, [predicate], [context])` Alias: **any** [source](https://underscorejs.org/docs/modules/some.html)  

Returns _true_ if any of the values in the **list** pass the **predicate** truth test. Short-circuits and stops traversing the list if a true element is found. **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

```js
_.some([null, 0, 'yes', false]);
=> true
```

### contains

`_.contains(list, value, [fromIndex])` Aliases: **include**, **includes** [source](https://underscorejs.org/docs/modules/contains.html)  

Returns _true_ if the **value** is present in the **list**. Uses **indexOf** internally, if **list** is an Array. Use **fromIndex** to start your search at a given index.

```js
_.contains([1, 2, 3], 3);
=> true
```

### invoke

`_.invoke(list, methodName, *arguments)` [source](https://underscorejs.org/docs/modules/invoke.html)  

Calls the method named by **methodName** on each value in the **list**. Any extra arguments passed to **invoke** will be forwarded on to the method invocation.

```js
_.invoke([[5, 1, 7], [3, 2, 1]], 'sort');
=> [[1, 5, 7], [1, 2, 3]]
```

### pluck

`_.pluck(list, propertyName)` [source](https://underscorejs.org/docs/modules/pluck.html)  

A convenient version of what is perhaps the most common use-case for **map**: extracting a list of property values.

```js
var stooges = [{name: 'moe', age: 40}, {name: 'larry', age: 50}, {name: 'curly', age: 60}];
_.pluck(stooges, 'name');
=> ["moe", "larry", "curly"]
```

### max

`_.max(list, [iteratee], [context])` [source](https://underscorejs.org/docs/modules/max.html)  

Returns the maximum value in **list**. If an [**iteratee**](#iteratee) function is provided, it will be used on each value to generate the criterion by which the value is ranked. _\-Infinity_ is returned if **list** is empty, so an [isEmpty](#isEmpty) guard may be required. This function can currently only compare numbers reliably. This function uses operator < ([note](#relational-operator-note)).

```js
var stooges = [{name: 'moe', age: 40}, {name: 'larry', age: 50}, {name: 'curly', age: 60}];
_.max(stooges, function(stooge){ return stooge.age; });
=> {name: 'curly', age: 60};
```

### min

`_.min(list, [iteratee], [context])` [source](https://underscorejs.org/docs/modules/min.html)  

Returns the minimum value in **list**. If an [**iteratee**](#iteratee) function is provided, it will be used on each value to generate the criterion by which the value is ranked. _Infinity_ is returned if **list** is empty, so an [isEmpty](#isEmpty) guard may be required. This function can currently only compare numbers reliably. This function uses operator < ([note](#relational-operator-note)).

```js
var numbers = [10, 5, 100, 2, 1000];
_.min(numbers);
=> 2
```

### sortBy

`_.sortBy(list, iteratee, [context])` [source](https://underscorejs.org/docs/modules/sortBy.html)  

Returns a (stably) sorted copy of **list**, ranked in ascending order by the results of running each value through [**iteratee**](#iteratee). iteratee may also be the string name of the property to sort by (eg. length). This function uses operator < ([note](#relational-operator-note)).

```js
_.sortBy([1, 2, 3, 4, 5, 6], function(num){ return Math.sin(num); });
=> [5, 4, 6, 3, 1, 2]

var stooges = [{name: 'moe', age: 40}, {name: 'larry', age: 50}, {name: 'curly', age: 60}];
_.sortBy(stooges, 'name');
=> [{name: 'curly', age: 60}, {name: 'larry', age: 50}, {name: 'moe', age: 40}];
```

### groupBy

`_.groupBy(list, iteratee, [context])` [source](https://underscorejs.org/docs/modules/groupBy.html)  

Splits a collection into sets, grouped by the result of running each value through **iteratee**. If **iteratee** is a string instead of a function, groups by the property named by **iteratee** on each of the values.

```js
_.groupBy([1.3, 2.1, 2.4], function(num){ return Math.floor(num); });
=> {1: [1.3], 2: [2.1, 2.4]}

_.groupBy(['one', 'two', 'three'], 'length');
=> {3: ["one", "two"], 5: ["three"]}
```

### indexBy

`_.indexBy(list, iteratee, [context])` [source](https://underscorejs.org/docs/modules/indexBy.html)  

Given a **list**, and an [**iteratee**](#iteratee) function that returns a key for each element in the list (or a property name), returns an object with an index of each item. Just like [groupBy](#groupBy), but for when you know your keys are unique.

```js
var stooges = [{name: 'moe', age: 40}, {name: 'larry', age: 50}, {name: 'curly', age: 60}];
_.indexBy(stooges, 'age');
=> {
  "40": {name: 'moe', age: 40},
  "50": {name: 'larry', age: 50},
  "60": {name: 'curly', age: 60}
}
```

### countBy

`_.countBy(list, iteratee, [context])` [source](https://underscorejs.org/docs/modules/countBy.html)  

Sorts a list into groups and returns a count for the number of objects in each group. Similar to groupBy, but instead of returning a list of values, returns a count for the number of values in that group.

```js
_.countBy([1, 2, 3, 4, 5], function(num) {
  return num % 2 == 0 ? 'even': 'odd';
});
=> {odd: 3, even: 2}
```

### shuffle

`_.shuffle(list)` [source](https://underscorejs.org/docs/modules/shuffle.html)  

Returns a shuffled copy of the **list**, using a version of the [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle).

```js
_.shuffle(\[1, 2, 3, 4, 5, 6]);
=> [4, 1, 6, 3, 5, 2]
```

### sample

`_.sample(list, [n])` [source](https://underscorejs.org/docs/modules/sample.html)  

Produce a random sample from the **list**. Pass a number to return **n** random elements from the list. Otherwise a single random item will be returned.

```js
_.sample([1, 2, 3, 4, 5, 6]);
=> 4

_.sample([1, 2, 3, 4, 5, 6], 3);
=> [1, 6, 2]
```

### toArray

`_.toArray(list)` [source](https://underscorejs.org/docs/modules/toArray.html)  

Creates a real Array from the **list** (anything that can be iterated over). Useful for transmuting the **arguments** object.

```js
(function(){ return _.toArray(arguments).slice(1); })(1, 2, 3, 4);
=> [2, 3, 4]
```

### size

`_.size(list)` [source](https://underscorejs.org/docs/modules/size.html)  

Return the number of values in the **list**.

```js
_.size([1, 2, 3, 4, 5]);
=> 5

_.size({one: 1, two: 2, three: 3});
=> 3
```

### partition

`_.partition(list, predicate)` [source](https://underscorejs.org/docs/modules/partition.html)  

Split **list** into two arrays: one whose elements all satisfy **predicate** and one whose elements all do not satisfy **predicate**. **predicate** is transformed through [**iteratee**](#iteratee) to facilitate shorthand syntaxes.

```js
_.partition([0, 1, 2, 3, 4, 5], isOdd);
=> [[1, 3, 5], [0, 2, 4]]
```

### compact

`_.compact(list)` [source](https://underscorejs.org/docs/modules/compact.html)  

Returns a copy of the **list** with all falsy values removed. In JavaScript, _false_, _null_, _0_, _""_, _undefined_ and _NaN_ are all falsy.

```js
_.compact([0, 1, false, 2, '', 3]);
=> [1, 2, 3]
```
