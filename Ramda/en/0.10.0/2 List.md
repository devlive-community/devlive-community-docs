[TOC]

### all

-----------------------------------------------------------------------------------------------------

`(a → Boolean) → [a] → Boolean`

Parameters

* **fnThe** predicate function.
* **listThe** array to consider.

> Returns Boolean `true` if the predicate is satisfied by every element, `false` otherwise.

Added in v0.1.0

Returns `true` if all elements of the list match the predicate, `false` if there are any that don't.

Dispatches to the `all` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [any](#any), [none](#none), [transduce](#transduce).

```js
const equals3 = R.equals(3);
R.all(equals3)([3, 3, 3, 3]); //=> true
R.all(equals3)([3, 3, 1, 3]); //=> false
```

### any

-----------------------------------------------------------------------------------------------------

`(a → Boolean) → [a] → Boolean`

Parameters

*   fnThe predicate function.
*   listThe array to consider.

> Returns Boolean `true` if the predicate is satisfied by at least one element, `false` otherwise.

Added in v0.1.0

Returns `true` if at least one of the elements of the list match the predicate, `false` otherwise.

Dispatches to the `any` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [all](#all), [none](#none), [transduce](#transduce).

```js
const lessThan0 = R.flip(R.lt)(0);
const lessThan2 = R.flip(R.lt)(2);
R.any(lessThan0)([1, 2]); //=> false
R.any(lessThan2)([1, 2]); //=> true
```

### append

--------------------------------------------------------------------------------------------------------------

`a → [a] → [a]`

Parameters

*   elThe element to add to the end of the new list.
*   listThe list of elements to add a new item to. list.

> Returns Array A new list containing the elements of the old list followed by `el`.

Added in v0.1.0

Returns a new list containing the contents of the given list, followed by the given element.

See also [prepend](#prepend).

```js
R.append('tests', ['write', 'more']); //=> ['write', 'more', 'tests']
R.append('tests', []); //=> ['tests']
R.append(['tests'], ['write', 'more']); //=> ['write', 'more', ['tests']]
```

### concat

--------------------------------------------------------------------------------------------------------------

`[a] → [a] → [a]`

`String → String → String`

Parameters

*   firstListThe first list
*   secondListThe second list

> Returns Array A list consisting of the elements of `firstList` followed by the elements of `secondList`.

Added in v0.1.0

Returns the result of concatenating the given lists or strings.

Note: `R.concat` expects both arguments to be of the same type, unlike the native `Array.prototype.concat` method. It will throw an error if you `concat` an Array with a non-Array value.

Dispatches to the `concat` method of the first argument, if present. Can also concatenate two members of a [fantasy-land compatible semigroup](https://github.com/fantasyland/fantasy-land#semigroup).

```js
R.concat('ABC', 'DEF'); // 'ABCDEF'
R.concat([4, 5, 6], [1, 2, 3]); //=> [4, 5, 6, 1, 2, 3]
R.concat([], []); //=> []
```

### drop

--------------------------------------------------------------------------------------------------------

`Number → [a] → [a]`

`Number → String → String`

Parameters

*   n
*   list

> Returns * A copy of list without the first `n` elements

Added in v0.1.0

Returns all but the first `n` elements of the given list, string, or transducer/transformer (or object with a `drop` method).

Dispatches to the `drop` method of the second argument, if present.

See also [take](#take), [transduce](#transduce), [dropLast](#dropLast), [dropWhile](#dropWhile).

```js
R.drop(1, ['foo', 'bar', 'baz']); //=> ['bar', 'baz']
R.drop(2, ['foo', 'bar', 'baz']); //=> ['baz']
R.drop(3, ['foo', 'bar', 'baz']); //=> []
R.drop(4, ['foo', 'bar', 'baz']); //=> []
R.drop(3, 'ramda');               //=> 'da'
```

### zipWith

-----------------------------------------------------------------------------------------------------------------

`((a, b) → c) → [a] → [b] → [c]`

Parameters

*   fnThe function used to combine the two elements into one value.
*   list1The first array to consider.
*   list2The second array to consider.

> Returns Array The list made by combining same-indexed elements of `list1` and `list2` using `fn`.

Added in v0.1.0

Creates a new list out of the two supplied by applying the function to each equally-positioned pair in the lists. The returned list is truncated to the length of the shorter of the two input lists.

```js
const f = (x, y) => {
  // ...
};
R.zipWith(f, [1, 2, 3], ['a', 'b', 'c']);
//=> [f(1, 'a'), f(2, 'b'), f(3, 'c')]
```

### zip

-----------------------------------------------------------------------------------------------------

`[a] → [b] → [[a,b]]`

Parameters

*   list1The first array to consider.
*   list2The second array to consider.

> Returns Array The list made by pairing up same-indexed elements of `list1` and `list2`.

Added in v0.1.0

Creates a new list out of the two supplied by pairing up equally-positioned items from both lists. The returned list is truncated to the length of the shorter of the two input lists. Note: `zip` is equivalent to `zipWith(function(a, b) { return [a, b] })`.

```js
R.zip([1, 2, 3], ['a', 'b', 'c']); //=> [[1, 'a'], [2, 'b'], [3, 'c']]
```

### xprod

-----------------------------------------------------------------------------------------------------------

`[a] → [b] → [[a,b]]`

Parameters

*   asThe first list.
*   bsThe second list.

> Returns Array The list made by combining each possible pair from `as` and `bs` into pairs (`[a, b]`).

Added in v0.1.0

Creates a new list out of the two supplied by creating each possible pair from the lists.

```js
R.xprod([1, 2], ['a', 'b']); //=> [[1, 'a'], [1, 'b'], [2, 'a'], [2, 'b']]
```

### uniq

--------------------------------------------------------------------------------------------------------

`[a] → [a]`

Parameters

*   listThe array to consider.

> Returns Array The list of unique items.

Added in v0.1.0

Returns a new list containing only one copy of each element in the original list. [`R.equals`](#equals) is used to determine equality.

```js
R.uniq([1, 1, 2, 1]); //=> [1, 2]
R.uniq([1, '1']);     //=> [1, '1']
R.uniq([[42], [42]]); //=> [[42]]
```

### filter

--------------------------------------------------------------------------------------------------------------

`Filterable f => (a → Boolean) → f a → f a`

Parameters

*   pred
*   filterable

> Returns Array Filterable

Added in v0.1.0

Takes a predicate and a `Filterable`, and returns a new filterable of the same type containing the members of the given filterable which satisfy the given predicate. Filterable objects include plain objects or any object that has a filter method such as `Array`.

Dispatches to the `filter` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [reject](#reject), [transduce](#transduce), [addIndex](#addIndex).

```js
const isEven = n => n % 2 === 0;

R.filter(isEven, [1, 2, 3, 4]); //=> [2, 4]

R.filter(isEven, {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, d: 4}
```

### find

--------------------------------------------------------------------------------------------------------

`(a → Boolean) → [a] → a | undefined`

Parameters

*   fnThe predicate function used to determine if the element is the desired one.
*   listThe array to consider.

> Returns Object The element found, or `undefined`.

Added in v0.1.0

Returns the first element of the list which matches the predicate, or `undefined` if no element matches.

Dispatches to the `find` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [transduce](#transduce).

```js
const xs = [{a: 1}, {a: 2}, {a: 3}];
R.find(R.propEq(2, 'a'))(xs); //=> {a: 2}
R.find(R.propEq(4, 'a'))(xs); //=> undefined
```

### flatten

-----------------------------------------------------------------------------------------------------------------

`[a] → [b]`

Parameters

*   listThe array to consider.

> Returns Array The flattened list.

Added in v0.1.0

Returns a new list by pulling every item out of it (and all its sub-arrays) and putting them in a new array, depth-first.

See also [unnest](#unnest).

```js
R.flatten([1, 2, [3, 4], 5, [6, [7, 8, [9, [10, 11], 12]]]]);
//=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```

### head

--------------------------------------------------------------------------------------------------------

`[a] → a | Undefined`

`String → String | Undefined`

Added in v0.1.0

Returns the first element of the given list or string. In some libraries this function is named `first`.

See also [tail](#tail), [init](#init), [last](#last).

```js
R.head(['fi', 'fo', 'fum']); //=> 'fi'
R.head([]); //=> undefined

R.head('abc'); //=> 'a'
R.head(''); //=> undefined
```

### indexOf

-----------------------------------------------------------------------------------------------------------------

`a → [a] → Number`

Parameters

*   targetThe item to find.
*   xsThe array to search in.

> Returns Number the index of the target, or -1 if the target is not found.

Added in v0.1.0

Returns the position of the first occurrence of an item in an array, or -1 if the item is not included in the array. [`R.equals`](#equals) is used to determine equality.

See also [lastIndexOf](#lastIndexOf), [findIndex](#findIndex).

```js
R.indexOf(3, [1,2,3,4]); //=> 2
R.indexOf(10, [1,2,3,4]); //=> -1
```

### join

--------------------------------------------------------------------------------------------------------

`String → [a] → String`

Parameters

*   separatorThe string used to separate the elements.
*   xsThe elements to join into a string.

> Returns String str The string made by concatenating `xs` with `separator`.

Added in v0.1.0

Returns a string made by inserting the `separator` between each element and concatenating all the elements into a single string.

See also [split](#split).

```js
const spacer = R.join(' ');
spacer(['a', 2, 3.4]);   //=> 'a 2 3.4'
R.join('|', [1, 2, 3]);    //=> '1|2|3'
```

### lastIndexOf

-----------------------------------------------------------------------------------------------------------------------------

`a → [a] → Number`

Parameters

*   targetThe item to find.
*   xsThe array to search in.

> Returns Number the index of the target, or -1 if the target is not found.

Added in v0.1.0

Returns the position of the last occurrence of an item in an array, or -1 if the item is not included in the array. [`R.equals`](#equals) is used to determine equality.

See also [indexOf](#indexOf), [findLastIndex](#findLastIndex).

```js
R.lastIndexOf(3, [-1,3,3,0,1,2,3,4]); //=> 6
R.lastIndexOf(10, [1,2,3,4]); //=> -1
```

### map

-----------------------------------------------------------------------------------------------------

`Functor f => (a → b) → f a → f b`

Parameters

*   fnThe function to be called on every element of the input `list`.
*   listThe list to be iterated over.

> Returns Array The new list.

Added in v0.1.0

Takes a function and a [functor](https://github.com/fantasyland/fantasy-land#functor), applies the function to each of the functor's values, and returns a functor of the same shape.

Ramda provides suitable `map` implementations for `Array` and `Object`, so this function may be applied to `[1, 2, 3]` or `{x: 1, y: 2, z: 3}`.

Dispatches to the `map` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

Also treats functions as functors and will compose them together.

See also [transduce](#transduce), [addIndex](#addIndex), [pluck](#pluck), [project](#project).

```js
const double = x => x * 2;

R.map(double, [1, 2, 3]); //=> [2, 4, 6]

R.map(double, {x: 1, y: 2, z: 3}); //=> {x: 2, y: 4, z: 6}
```

### nth

-----------------------------------------------------------------------------------------------------

`Number → [a] → a | Undefined`

`Number → String → String | Undefined`

Added in v0.1.0

Returns the nth element of the given list or string. If n is negative the element at index length + n is returned.

```js
const list = ['foo', 'bar', 'baz', 'quux'];
R.nth(1, list); //=> 'bar'
R.nth(-1, list); //=> 'quux'
R.nth(-99, list); //=> undefined

R.nth(2, 'abc'); //=> 'c'
R.nth(3, 'abc'); //=> undefined
```

### pluck

---

`Functor f => k → f {k: v} → f v`

Parameters

*   keyThe key name to pluck off of each object.
*   fThe array or functor to consider.

> Returns Array The list of values for the given key.

Added in v0.1.0

Returns a new list by plucking the same named property off all objects in the list supplied.

`pluck` will work on any [functor](https://github.com/fantasyland/fantasy-land#functor) in addition to arrays, as it is equivalent to `R.map(R.prop(k), f)`.

See also [project](#project), [prop](#prop), [props](#props).

```js
var getAges = R.pluck('age');
getAges([{name: 'fred', age: 29}, {name: 'wilma', age: 27}]); //=> [29, 27]

R.pluck(0, [[1, 2], [3, 4]]);               //=> [1, 3]
R.pluck('val', {a: {val: 3}, b: {val: 5}}); //=> {a: 3, b: 5}
```

### prepend

---

`a → [a] → [a]`

Parameters

*   elThe item to add to the head of the output list.
*   listThe array to add to the tail of the output list.

> Returns Array A new array.

Added in v0.1.0

Returns a new list with the given element at the front, followed by the contents of the list.

See also [append](#append).

```js
R.prepend('fee', ['fi', 'fo', 'fum']); //=> ['fee', 'fi', 'fo', 'fum']
```

### range

---

`Number → Number → [Number]`

Parameters

*   fromThe first number in the list.
*   toOne more than the last number in the list.

> Returns Array The list of numbers in the set `[a, b)`.

Added in v0.1.0

Returns a list of numbers from `from` (inclusive) to `to` (exclusive).

```js
R.range(1, 5);    //=> [1, 2, 3, 4]
R.range(50, 53);  //=> [50, 51, 52]
```

### reduce

---

`((a, b) → a) → a → [b] → a`

Parameters

*   fnThe iterator function. Receives two values, the accumulator and the current element from the array.
*   accThe accumulator value.
*   listThe list to iterate over.

> Returns * The final, accumulated value.

Added in v0.1.0

Returns a single item by iterating through the list, successively calling the iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.

The iterator function receives two values: _(acc, value)_. It may use [`R.reduced`](#reduced) to shortcut the iteration.

The arguments' order of [`reduceRight`](#reduceRight)'s iterator function is _(value, acc)_.

Note: `R.reduce` does not skip deleted or unassigned indices (sparse arrays), unlike the native `Array.prototype.reduce` method. For more details on this behavior, see: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/reduce#Description](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#Description)

Be cautious of mutating and returning the accumulator. If you reuse it across invocations, it will continue to accumulate onto the same value. The general recommendation is to always return a new value. If you can't do so for performance reasons, then be sure to reinitialize the accumulator on each invocation.

Dispatches to the `reduce` method of the third argument, if present. When doing so, it is up to the user to handle the [`R.reduced`](#reduced) shortcuting, as this is not implemented by `reduce`.

See also [reduced](#reduced), [addIndex](#addIndex), [reduceRight](#reduceRight).

```js
R.reduce(R.subtract, 0, [1, 2, 3, 4]) // => ((((0 - 1) - 2) - 3) - 4) = -10
//          -               -10
//         / \              / \
//        -   4           -6   4
//       / \              / \
//      -   3   ==>     -3   3
//     / \              / \
//    -   2           -1   2
//   / \              / \
//  0   1            0   1
```

### reduceRight

---

`((a, b) → b) → b → [a] → b`

Parameters

*   fnThe iterator function. Receives two values, the current element from the array and the accumulator.
*   accThe accumulator value.
*   listThe list to iterate over.

> Returns * The final, accumulated value.

Added in v0.1.0

Returns a single item by iterating through the list, successively calling the iterator function and passing it an accumulator value and the current value from the array, and then passing the result to the next call.

Similar to [`reduce`](#reduce), except moves through the input list from the right to the left.

The iterator function receives two values: _(value, acc)_, while the arguments' order of `reduce`'s iterator function is _(acc, value)_. `reduceRight` may use [`reduced`](#reduced) to short circuit the iteration.

Note: `R.reduceRight` does not skip deleted or unassigned indices (sparse arrays), unlike the native `Array.prototype.reduceRight` method. For more details on this behavior, see: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/reduceRight#Description](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight#Description)

Be cautious of mutating and returning the accumulator. If you reuse it across invocations, it will continue to accumulate onto the same value. The general recommendation is to always return a new value. If you can't do so for performance reasons, then be sure to reinitialize the accumulator on each invocation.

See also [reduce](#reduce), [addIndex](#addIndex), [reduced](#reduced).

```js
R.reduceRight(R.subtract, 0, [1, 2, 3, 4]) // => (1 - (2 - (3 - (4 - 0)))) = -2
//    -               -2
//   / \              / \
//  1   -            1   3
//     / \              / \
//    2   -     ==>    2  -1
//       / \              / \
//      3   -            3   4
//         / \              / \
//        4   0            4   0
```

### reject

---

`Filterable f => (a → Boolean) → f a → f a`

Parameters

*   pred
*   filterable

> Returns Array

Added in v0.1.0

The complement of [`filter`](#filter).

Acts as a transducer if a transformer is given in list position. Filterable objects include plain objects or any object that has a filter method such as `Array`.

See also [filter](#filter), [transduce](#transduce), [addIndex](#addIndex).

```js
const isOdd = (n) => n % 2 !== 0;

R.reject(isOdd, [1, 2, 3, 4]); //=> [2, 4]

R.reject(isOdd, {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, d: 4}
```

### reverse

---

`[a] → [a]`

`String → String`

Added in v0.1.0

Returns a new list or string with the elements or characters in reverse order.

```js
R.reverse([1, 2, 3]);  //=> [3, 2, 1]
R.reverse([1, 2]);     //=> [2, 1]
R.reverse([1]);        //=> [1]
R.reverse([]);         //=> []

R.reverse('abc');      //=> 'cba'
R.reverse('ab');       //=> 'ba'
R.reverse('a');        //=> 'a'
R.reverse('');         //=> ''
```

### sort

---

`((a, a) → Number) → [a] → [a]`

Parameters

*   comparatorA sorting function :: a -> b -> Int
*   listThe list to sort

> Returns Array a new array with its elements sorted by the comparator function.

Added in v0.1.0

Returns a copy of the list, sorted according to the comparator function, which should accept two values at a time and return a negative number if the first value is smaller, a positive number if it's larger, and zero if they are equal. Please note that this is a **copy** of the list. It does not modify the original.

See also [ascend](#ascend), [descend](#descend).

```js
const diff = function(a, b) { return a - b; };
R.sort(diff, [4,2,7,5]); //=> [2, 4, 5, 7]
```

### tail

---

`[a] → [a]`

`String → String`

Added in v0.1.0

Returns all but the first element of the given list or string (or object with a `tail` method).

Dispatches to the `slice` method of the first argument, if present.

See also [head](#head), [init](#init), [last](#last).

```js
R.tail([1, 2, 3]);  //=> [2, 3]
R.tail([1, 2]);     //=> [2]
R.tail([1]);        //=> []
R.tail([]);         //=> []

R.tail('abc');  //=> 'bc'
R.tail('ab');   //=> 'b'
R.tail('a');    //=> ''
R.tail('');     //=> ''
```

### take

---

`Number → [a] → [a]`

`Number → String → String`

Added in v0.1.0

Returns the first `n` elements of the given list, string, or transducer/transformer (or object with a `take` method).

Dispatches to the `take` method of the second argument, if present.

See also [drop](#drop).

```js
R.take(1, ['foo', 'bar', 'baz']); //=> ['foo']
R.take(2, ['foo', 'bar', 'baz']); //=> ['foo', 'bar']
R.take(3, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(4, ['foo', 'bar', 'baz']); //=> ['foo', 'bar', 'baz']
R.take(3, 'ramda');               //=> 'ram'

const personnel = [
  'Dave Brubeck',
  'Paul Desmond',
  'Eugene Wright',
  'Joe Morello',
  'Gerry Mulligan',
  'Bob Bates',
  'Joe Dodge',
  'Ron Crotty'
];

const takeFive = R.take(5);
takeFive(personnel);
//=> ['Dave Brubeck', 'Paul Desmond', 'Eugene Wright', 'Joe Morello', 'Gerry Mulligan']
```

### takeWhile

---

`(a → Boolean) → [a] → [a]`

`(a → Boolean) → String → String`

Parameters

*   fnThe function called per iteration.
*   xsThe collection to iterate over.

> Returns Array A new array.

Added in v0.1.0

Returns a new list containing the first `n` elements of a given list, passing each value to the supplied predicate function, and terminating when the predicate function returns `false`. Excludes the element that caused the predicate function to fail. The predicate function is passed one argument: _(value)_.

Dispatches to the `takeWhile` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [dropWhile](#dropWhile), [transduce](#transduce), [addIndex](#addIndex).

```js
const isNotFour = x => x !== 4;

R.takeWhile(isNotFour, [1, 2, 3, 4, 3, 2, 1]); //=> [1, 2, 3]

R.takeWhile(x => x !== 'd' , 'Ramda'); //=> 'Ram'
```

### findLast

---

`(a → Boolean) → [a] → a | undefined`

Parameters

*   fnThe predicate function used to determine if the element is the desired one.
*   listThe array to consider.

> Returns Object The element found, or `undefined`.

Added in v0.1.1

Returns the last element of the list which matches the predicate, or `undefined` if no element matches.

Acts as a transducer if a transformer is given in list position.

See also [transduce](#transduce).

```js
const xs = [{a: 1, b: 0}, {a:1, b: 1}];
R.findLast(R.propEq(1, 'a'))(xs); //=> {a: 1, b: 1}
R.findLast(R.propEq(4, 'a'))(xs); //=> undefined
```

### findLastIndex

---

`(a → Boolean) → [a] → Number`

Parameters

*   fnThe predicate function used to determine if the element is the desired one.
*   listThe array to consider.

> Returns Number The index of the element found, or `-1`.

Added in v0.1.1

Returns the index of the last element of the list which matches the predicate, or `-1` if no element matches.

Acts as a transducer if a transformer is given in list position.

See also [transduce](#transduce), [lastIndexOf](#lastIndexOf).

```js
const xs = [{a: 1, b: 0}, {a:1, b: 1}];
R.findLastIndex(R.propEq(1, 'a'))(xs); //=> 1
R.findLastIndex(R.propEq(4, 'a'))(xs); //=> -1
```

### forEach

---

`(a → *) → [a] → [a]`

Parameters

*   fnThe function to invoke. Receives one argument, `value`.
*   listThe list to iterate over.

> Returns Array The original list.

Added in v0.1.1

Iterate over an input `list`, calling a provided function `fn` for each element in the list.

`fn` receives one argument: _(value)_.

Note: `R.forEach` does not skip deleted or unassigned indices (sparse arrays), unlike the native `Array.prototype.forEach` method. For more details on this behavior, see: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/forEach#Description](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#Description)

Also note that, unlike `Array.prototype.forEach`, Ramda's `forEach` returns the original array. In some libraries this function is named `each`.

Dispatches to the `forEach` method of the second argument, if present.

See also [addIndex](#addIndex).

```js
const printXPlusFive = x => console.log(x + 5);
R.forEach(printXPlusFive, [1, 2, 3]); //=> [1, 2, 3]
// logs 6
// logs 7
// logs 8
```

### repeat

---

`a → n → [a]`

Parameters

*   valueThe value to repeat.
*   nThe desired size of the output list.

> Returns Array A new array containing `n` `value`s.

Added in v0.1.1

Returns a fixed list of size `n` containing a specified identical value.

See also [times](#times).

```js
R.repeat('hi', 5); //=> ['hi', 'hi', 'hi', 'hi', 'hi']
    
const obj = {};
const repeatedObjs = R.repeat(obj, 5); //=> [{}, {}, {}, {}, {}]
repeatedObjs[0] === repeatedObjs[1]; //=> true
```

### findIndex

---

`(a → Boolean) → [a] → Number`

Parameters

*   fnThe predicate function used to determine if the element is the desired one.
*   listThe array to consider.

> Returns Number The index of the element found, or `-1`.

Added in v0.1.1

Returns the index of the first element of the list which matches the predicate, or `-1` if no element matches.

Acts as a transducer if a transformer is given in list position.

See also [transduce](#transduce), [indexOf](#indexOf).

```js
const xs = [{a: 1}, {a: 2}, {a: 3}];
R.findIndex(R.propEq(2, 'a'))(xs); //=> 1
R.findIndex(R.propEq(4, 'a'))(xs); //=> -1
```

### last

---

`[a] → a | Undefined`

`String → String | Undefined`

Added in v0.1.4

Returns the last element of the given list or string.

See also [init](#init), [head](#head), [tail](#tail).

```js
R.last(['fi', 'fo', 'fum']); //=> 'fum'
R.last([]); //=> undefined

R.last('abc'); //=> 'c'
R.last(''); //=> undefined
```

### partition

---

`Filterable f => (a → Boolean) → f a → [f a, f a]`

Parameters

*   predA predicate to determine which side the element belongs to.
*   filterablethe list (or other filterable) to partition.

> Returns Array An array, containing first the subset of elements that satisfy the predicate, and second the subset of elements that do not satisfy.

Added in v0.1.4

Takes a predicate and a list or other `Filterable` object and returns the pair of filterable objects of the same type of elements which do and do not satisfy, the predicate, respectively. Filterable objects include plain objects or any object that has a filter method such as `Array`.

See also [filter](#filter), [reject](#reject).

```js
R.partition(R.includes('s'), ['sss', 'ttt', 'foo', 'bars']);
// => [ [ 'sss', 'bars' ],  [ 'ttt', 'foo' ] ]

R.partition(R.includes('s'), { a: 'sss', b: 'ttt', foo: 'bars' });
// => [ { a: 'sss', foo: 'bars' }, { b: 'ttt' }  ]
```

### slice

---

`Number → Number → [a] → [a]`

`Number → Number → String → String`

Parameters

*   fromIndexThe start index (inclusive).
*   toIndexThe end index (exclusive).
*   list

> Returns *

Added in v0.1.4

Returns the elements of the given list or string (or object with a `slice` method) from `fromIndex` (inclusive) to `toIndex` (exclusive).

Dispatches to the `slice` method of the third argument, if present.

```js
R.slice(1, 3, ['a', 'b', 'c', 'd']);        //=> ['b', 'c']
R.slice(1, Infinity, ['a', 'b', 'c', 'd']); //=> ['b', 'c', 'd']
R.slice(0, -1, ['a', 'b', 'c', 'd']);       //=> ['a', 'b', 'c']
R.slice(-3, -1, ['a', 'b', 'c', 'd']);      //=> ['b', 'c']
R.slice(0, 3, 'ramda');                     //=> 'ram'
```

### uniqWith

---

`((a, a) → Boolean) → [a] → [a]`

Parameters

*   predA predicate used to test whether two items are equal.
*   listThe array to consider.

> Returns Array The list of unique items.

Added in v0.2.0

Returns a new list containing only one copy of each element in the original list, based upon the value returned by applying the supplied predicate to two list elements. Prefers the first item if two items compare equal based on the predicate.

Acts as a transducer if a transformer is given in list position.

```js
const strEq = R.eqBy(String);
R.uniqWith(strEq)([1, '1', 2, 1]); //=> [1, 2]
R.uniqWith(strEq)([{}, {}]);       //=> [{}]
R.uniqWith(strEq)([1, '1', 1]);    //=> [1]
R.uniqWith(strEq)(['1', 1, 1]);    //=> ['1']
```

### insert

---

`Number → a → [a] → [a]`

Parameters

*   indexThe position to insert the element
*   eltThe element to insert into the Array
*   listThe list to insert into

> Returns Array A new Array with `elt` inserted at `index`.

Added in v0.2.2

Inserts the supplied element into the list, at the specified `index`. _Note that this is not destructive_: it returns a copy of the list with the changes. No lists have been harmed in the application of this function.

```js
R.insert(2, 'x', [1,2,3,4]); //=> [1,2,'x',3,4]
```

### remove

---

`Number → Number → [a] → [a]`

Parameters

*   startThe position to start removing elements
*   countThe number of elements to remove
*   listThe list to remove from

> Returns Array A new Array with `count` elements from `start` removed.

Added in v0.2.2

Removes the sub-list of `list` starting at index `start` and containing `count` elements. _Note that this is not destructive_: it returns a copy of the list with the changes. No lists have been harmed in the application of this function.

See also [without](#without).

```js
R.remove(2, 3, [1,2,3,4,5,6,7,8]); //=> [1,2,6,7,8]
```

### times

---

`(Number → a) → Number → [a]`

Parameters

*   fnThe function to invoke. Passed one argument, the current value of `n`.
*   nA value between `0` and `n - 1`. Increments after each function call.

> Returns Array An array containing the return values of all calls to `fn`.

Added in v0.2.3

Calls an input function `n` times, returning an array containing the results of those function calls.

`fn` is passed one argument: The current value of `n`, which begins at `0` and is gradually incremented to `n - 1`.

See also [repeat](#repeat).

```js
R.times(R.identity, 5); //=> [0, 1, 2, 3, 4]
```

### chain

---

`Chain m => (a → m b) → m a → m b`

Parameters

*   fnThe function to map with
*   listThe list to map over

> Returns Array The result of flat-mapping `list` with `fn`

Added in v0.3.0

`chain` maps a function over a list and concatenates the results. `chain` is also known as `flatMap` in some libraries.

Dispatches to the `chain` method of the second argument, if present, according to the [FantasyLand Chain spec](https://github.com/fantasyland/fantasy-land#chain).

If second argument is a function, `chain(f, g)(x)` is equivalent to `f(g(x), x)`.

Acts as a transducer if a transformer is given in list position.

```js
const duplicate = n => [n, n];
R.chain(duplicate, [1, 2, 3]); //=> [1, 1, 2, 2, 3, 3]

R.chain(R.append, R.head)([1, 2, 3]); //=> [1, 2, 3, 1]
```

### fromPairs

---

`[[k,v]] → {k: v}`

Parameters

*   pairsAn array of two-element arrays that will be the keys and values of the output object.

> Returns Object The object made by pairing up `keys` and `values`.

Added in v0.3.0

Creates a new object from a list key-value pairs. If a key appears in multiple pairs, the rightmost pair is included in the object.

See also [toPairs](#toPairs), [pair](#pair).

```js
R.fromPairs([['a', 1], ['b', 2], ['c', 3]]); //=> {a: 1, b: 2, c: 3}
```

### length

---

`[a] → Number`

Parameters

*   listThe array to inspect.

> Returns Number The length of the array.

Added in v0.3.0

Returns the number of elements in the array by returning `list.length`.

```js
R.length([]); //=> 0
R.length([1, 2, 3]); //=> 3
```

### unnest

---

`Chain c => c (c a) → c a`

Added in v0.3.0

Shorthand for `R.chain(R.identity)`, which removes one level of nesting from any [Chain](https://github.com/fantasyland/fantasy-land#chain).

See also [flatten](#flatten), [chain](#chain).

```js
R.unnest([1, [2], [[3]]]); //=> [1, 2, [3]]
R.unnest([[1, 2], [3, 4], [5, 6]]); //=> [1, 2, 3, 4, 5, 6]
```

### zipObj

---

`[String] → [*] → {String: *}`

Parameters

*   keysThe array that will be properties on the output object.
*   valuesThe list of values on the output object.

> Returns Object The object made by pairing up same-indexed elements of `keys` and `values`.

Added in v0.3.0

Creates a new object out of a list of keys and a list of values. Key/value pairing is truncated to the length of the shorter of the two lists. Note: `zipObj` is equivalent to `pipe(zip, fromPairs)`.

```js
R.zipObj(['a', 'b', 'c'], [1, 2, 3]); //=> {a: 1, b: 2, c: 3}
```

### dropWhile

---

`(a → Boolean) → [a] → [a]`

`(a → Boolean) → String → String`

Parameters

*   fnThe function called per iteration.
*   xsThe collection to iterate over.

> Returns Array A new array.

Added in v0.9.0

Returns a new list excluding the leading elements of a given list which satisfy the supplied predicate function. It passes each value to the supplied predicate function, skipping elements while the predicate function returns `true`. The predicate function is applied to one argument: _(value)_.

Dispatches to the `dropWhile` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [takeWhile](#takeWhile), [transduce](#transduce), [addIndex](#addIndex).

```js
const lteTwo = x => x <= 2;

R.dropWhile(lteTwo, [1, 2, 3, 4, 3, 2, 1]); //=> [3, 4, 3, 2, 1]

R.dropWhile(x => x !== 'd' , 'Ramda'); //=> 'da'
```

### init

---

`[a] → [a]`

`String → String`

Added in v0.9.0

Returns all but the last element of the given list or string.

See also [last](#last), [head](#head), [tail](#tail).

```js
R.init([1, 2, 3]);  //=> [1, 2]
R.init([1, 2]);     //=> [1]
R.init([1]);        //=> []
R.init([]);         //=> []

R.init('abc');  //=> 'ab'
R.init('ab');   //=> 'a'
R.init('a');    //=> ''
R.init('');     //=> ''
```

### insertAll

---

`Number → [a] → [a] → [a]`

Parameters

*   indexThe position to insert the sub-list
*   eltsThe sub-list to insert into the Array
*   listThe list to insert the sub-list into

> Returns Array A new Array with `elts` inserted starting at `index`.

Added in v0.9.0

Inserts the sub-list into the list, at the specified `index`. _Note that this is not destructive_: it returns a copy of the list with the changes. No lists have been harmed in the application of this function.

```js
R.insertAll(2, ['x','y','z'], [1,2,3,4]); //=> [1,2,'x','y','z',3,4]
```

### mapAccum

---

`((acc, x) → (acc, y)) → acc → [x] → (acc, [y])`

Parameters

*   fnThe function to be called on every element of the input `list`.
*   accThe accumulator value.
*   listThe list to iterate over.

> Returns * The final, accumulated value.

Added in v0.10.0

The `mapAccum` function behaves like a combination of map and reduce; it applies a function to each element of a list, passing an accumulating parameter from left to right, and returning a final value of this accumulator together with the new list.

The iterator function receives two arguments, _acc_ and _value_, and should return a tuple _\[acc, value\]_.

See also [scan](#scan), [addIndex](#addIndex), [mapAccumRight](#mapAccumRight).

```js
const digits = ['1', '2', '3', '4'];
const appender = (a, b) => [a + b, a + b];

R.mapAccum(appender, 0, digits); //=> ['01234', ['01', '012', '0123', '01234']]
```

### mapAccumRight

---

`((acc, x) → (acc, y)) → acc → [x] → (acc, [y])`

Parameters

*   fnThe function to be called on every element of the input `list`.
*   accThe accumulator value.
*   listThe list to iterate over.

> Returns * The final, accumulated value.

Added in v0.10.0

The `mapAccumRight` function behaves like a combination of map and reduce; it applies a function to each element of a list, passing an accumulating parameter from right to left, and returning a final value of this accumulator together with the new list.

Similar to [`mapAccum`](#mapAccum), except moves through the input list from the right to the left.

The iterator function receives two arguments, _acc_ and _value_, and should return a tuple _\[acc, value\]_.

See also [addIndex](#addIndex), [mapAccum](#mapAccum).

```js
const digits = ['1', '2', '3', '4'];
const appender = (a, b) => [b + a, b + a];

R.mapAccumRight(appender, 5, digits); //=> ['12345', ['12345', '2345', '345', '45']]
```

### mergeAll

---

`[{k: v}] → {k: v}`

Parameters

*   listAn array of objects

> Returns Object A merged object.

Added in v0.10.0

Creates one new object with the own properties from a list of objects. If a key exists in more than one object, the value from the last object it exists in will be used.

See also [reduce](#reduce).

```js
R.mergeAll([{foo:1},{bar:2},{baz:3}]); //=> {foo:1,bar:2,baz:3}
R.mergeAll([{foo:1},{foo:2},{bar:2}]); //=> {foo:2,bar:2}
```

### scan

---

`((a, b) → a) → a → [b] → [a]`

Parameters

*   fnThe iterator function. Receives two values, the accumulator and the current element from the array
*   accThe accumulator value.
*   listThe list to iterate over.

> Returns Array A list of all intermediately reduced values.

Added in v0.10.0

Scan is similar to [`reduce`](#reduce), but returns a list of successively reduced values from the left.

Acts as a transducer if a transformer is given in list position.

See also [reduce](#reduce), [mapAccum](#mapAccum).

```js
const numbers = [1, 2, 3, 4];
const factorials = R.scan(R.multiply, 1, numbers); //=> [1, 1, 2, 6, 24]
```

### unfold

---

`(a → [b]) → * → [b]`

Parameters

*   fnThe iterator function. receives one argument, `seed`, and returns either false to quit iteration or an array of length two to proceed. The element at index 0 of this array will be added to the resulting array, and the element at index 1 will be passed to the next call to `fn`.
*   seedThe seed value.

> Returns Array The final list.

Added in v0.10.0

Builds a list from a seed value. Accepts an iterator function, which returns either false to stop iteration or an array of length 2 containing the value to add to the resulting list and the seed to be used in the next call to the iterator function.

The iterator function receives one argument: _(seed)_.

```js
const f = n => n > 50 ? false : [-n, n + 10];
R.unfold(f, 10); //=> [-10, -20, -30, -40, -50]
```
