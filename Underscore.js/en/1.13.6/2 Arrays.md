[TOC]

_Note: All array functions will also work on the **arguments** object. However, Underscore functions are not designed to work on "sparse" arrays._

### first

`_.first(array, [n])` Aliases: **head**, **take** [source](https://underscorejs.org/docs/modules/first.html)  

Returns the first element of an **array**. Passing **n** will return the first **n** elements of the array.

```js
_.first([5, 4, 3, 2, 1]);
=> 5
```

### initial

`_.initial(array, [n])` [source](https://underscorejs.org/docs/modules/initial.html)  

Returns everything but the last entry of the array. Especially useful on the arguments object. Pass **n** to exclude the last **n** elements from the result.

```js
_.initial([5, 4, 3, 2, 1]);
=> [5, 4, 3, 2]
```

### last

`_.last(array, [n])` [source](https://underscorejs.org/docs/modules/last.html)  

Returns the last element of an **array**. Passing **n** will return the last **n** elements of the array.

```js
_.last([5, 4, 3, 2, 1]);
=> 1
```

### rest

`_.rest(array, [index])` Aliases: **tail**, **drop** [source](https://underscorejs.org/docs/modules/rest.html)  

Returns the **rest** of the elements in an array. Pass an **index** to return the values of the array from that index onward.

```js
_.rest([5, 4, 3, 2, 1]);
=> [4, 3, 2, 1]
```

### flatten

`_.flatten(array, [depth])` [source](https://underscorejs.org/docs/modules/flatten.html)  

Flattens a nested **array**. If you pass true or 1 as the **depth**, the array will only be flattened a single level. Passing a greater number will cause the flattening to descend deeper into the nesting hierarchy. Omitting the **depth** argument, or passing false or Infinity, flattens the array all the way to the deepest nesting level.

```js
_.flatten([1, [2], [3, [[4]]]]);
=> [1, 2, 3, 4];

_.flatten([1, [2], [3, [[4]]]], true);
=> [1, 2, 3, [[4]]];

_.flatten([1, [2], [3, [[4]]]], 2);
=> [1, 2, 3, [4]];
```

### without

`_.without(array, *values)` [source](https://underscorejs.org/docs/modules/without.html)  

Returns a copy of the **array** with all instances of the **values** removed.

```js
_.without([1, 2, 1, 0, 3, 1, 4], 0, 1);
=> [2, 3, 4]
```

### union

`_.union(*arrays)` [source](https://underscorejs.org/docs/modules/union.html)  

Computes the union of the passed-in **arrays**: the list of unique items, in order, that are present in one or more of the **arrays**.

```js
_.union([1, 2, 3], [101, 2, 1, 10], [2, 1]);
=> [1, 2, 3, 101, 10]
```

### intersection

`_.intersection(*arrays)` [source](https://underscorejs.org/docs/modules/intersection.html)  

Computes the list of values that are the intersection of all the **arrays**. Each value in the result is present in each of the **arrays**.

```js
_.intersection([1, 2, 3], [101, 2, 1, 10], [2, 1]);
=> [1, 2]
```

### difference

`_.difference(array, *others)` [source](https://underscorejs.org/docs/modules/difference.html)  

Similar to **without**, but returns the values from **array** that are not present in the **other** arrays.

```js
_.difference([1, 2, 3, 4, 5], [5, 2, 10]);
=> [1, 3, 4]
```

### uniq

`_.uniq(array, [isSorted], [iteratee])` Alias: **unique** [source](https://underscorejs.org/docs/modules/uniq.html)  

Produces a duplicate-free version of the **array**, using _\===_ to test object equality. In particular only the first occurrence of each value is kept. If you know in advance that the **array** is sorted, passing _true_ for **isSorted** will run a much faster algorithm. If you want to compute unique items based on a transformation, pass an [**iteratee**](#iteratee) function.

```js
_.uniq([1, 2, 1, 4, 1, 3]);
=> [1, 2, 4, 3]
```

### zip

`_.zip(*arrays)` [source](https://underscorejs.org/docs/modules/zip.html)  

Merges together the values of each of the **arrays** with the values at the corresponding position. Useful when you have separate data sources that are coordinated through matching array indexes.

```js
_.zip(['moe', 'larry', 'curly'], [30, 40, 50], [true, false, false]);
=> [["moe", 30, true], ["larry", 40, false], ["curly", 50, false]]
```

### unzip

`_.unzip(array)` Alias: **transpose** [source](https://underscorejs.org/docs/modules/unzip.html)  

The opposite of [zip](#zip). Given an **array** of arrays, returns a series of new arrays, the first of which contains all of the first elements in the input arrays, the second of which contains all of the second elements, and so on. If you're working with a matrix of nested arrays, this can be used to transpose the matrix.

```js
_.unzip([["moe", 30, true], ["larry", 40, false], ["curly", 50, false]]);
=> [['moe', 'larry', 'curly'], [30, 40, 50], [true, false, false]]
```

### object

`_.object(list, [values])` [source](https://underscorejs.org/docs/modules/object.html)  

Converts arrays into objects. Pass either a single list of `[key, value]` pairs, or a list of keys, and a list of values. Passing by pairs is the reverse of [pairs](#pairs). If duplicate keys exist, the last value wins.

```js
_.object(['moe', 'larry', 'curly'], [30, 40, 50]);
=> {moe: 30, larry: 40, curly: 50}

_.object([['moe', 30], ['larry', 40], ['curly', 50]]);
=> {moe: 30, larry: 40, curly: 50}
```

### chunk

`_.chunk(array, length)` [source](https://underscorejs.org/docs/modules/chunk.html)  

Chunks an **array** into multiple arrays, each containing **length** or fewer items.

```js
var partners = _.chunk(_.shuffle(kindergarten), 2);
=> [["Tyrone", "Elie"], ["Aidan", "Sam"], ["Katrina", "Billie"], ["Little Timmy"]]
```

### indexOf

`_.indexOf(array, value, [isSorted])` [source](https://underscorejs.org/docs/modules/indexOf.html)  

Returns the index at which **value** can be found in the **array**, or _\-1_ if value is not present in the **array**. If you're working with a large array, and you know that the array is already sorted, pass true for **isSorted** to use a faster binary search ... or, pass a number as the third argument in order to look for the first matching value in the array after the given index. If isSorted is true, this function uses operator < ([note](#relational-operator-note)).

```js
_.indexOf([1, 2, 3], 2);
=> 1
```

### lastIndexOf

`_.lastIndexOf(array, value, [fromIndex])` [source](https://underscorejs.org/docs/modules/lastIndexOf.html)  

Returns the index of the last occurrence of **value** in the **array**, or _\-1_ if value is not present. Pass **fromIndex** to start your search at a given index.

```js
_.lastIndexOf([1, 2, 3, 1, 2, 3\=], 2);
=> 4
```

### sortedIndex

`_.sortedIndex(array, value, [iteratee], [context])` [source](https://underscorejs.org/docs/modules/sortedIndex.html)  

Uses a binary search to determine the smallest index at which the **value** _should_ be inserted into the **array** in order to maintain the **array**'s sorted order. If an [**iteratee**](#iteratee) function is provided, it will be used to compute the sort ranking of each value, including the **value** you pass. The iteratee may also be the string name of the property to sort by (eg. length). This function uses operator < ([note](#relational-operator-note)).

```js
_.sortedIndex([10, 20, 30, 40, 50], 35);
=> 3

var stooges = [{name: 'moe', age: 40}, {name: 'curly', age: 60}];
_.sortedIndex(stooges, {name: 'larry', age: 50}, 'age');
=> 1
```

### findIndex

`_.findIndex(array, predicate, [context])` [source](https://underscorejs.org/docs/modules/findIndex.html)  

Similar to [\_.indexOf](#indexOf), returns the first index where the **predicate** truth test passes; otherwise returns _\-1_.

```js
_.findIndex([4, 6, 8, 12], isPrime);
=> -1 // not found
_.findIndex([4, 6, 7, 12], isPrime);
=> 2
```

### findLastIndex

`_.findLastIndex(array, predicate, [context])` [source](https://underscorejs.org/docs/modules/findLastIndex.html)  

Like [\_.findIndex](#findIndex) but iterates the array in reverse, returning the index closest to the end where the **predicate** truth test passes.

```js
var users = [{'id': 1, 'name': 'Bob', 'last': 'Brown'},
{'id': 2, 'name': 'Ted', 'last': 'White'},
{'id': 3, 'name': 'Frank', 'last': 'James'},
{'id': 4, 'name': 'Ted', 'last': 'Jones'}];
_.findLastIndex(users, {
name: 'Ted'
});
=> 3
```

### range

`_.range([start], stop, [step])` [source](https://underscorejs.org/docs/modules/range.html)  

A function to create flexibly-numbered lists of integers, handy for each and map loops. **start**, if omitted, defaults to _0_; **step** defaults to _1_ if **start** is before **stop**, otherwise _\-1_. Returns a list of integers from **start** (inclusive) to **stop** (exclusive), incremented (or decremented) by **step**.

```js
_.range(10);
=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
_.range(1, 11);
=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
_.range(0, 30, 5);
=> [0, 5, 10, 15, 20, 25]
_.range(0, -10, -1);
=> [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
_.range(0);
=> []
```
