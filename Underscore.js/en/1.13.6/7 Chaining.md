[TOC]

Calling `chain` will cause all future method calls to return wrapped objects. When you've finished the computation, call `value` to retrieve the final value. Here's an example of chaining together a **map/flatten/reduce**, in order to get the word count of every word in a song.

```js
var lyrics = [
  {line: 1, words: "I'm a lumberjack and I'm okay"},
  {line: 2, words: "I sleep all night and I work all day"},
  {line: 3, words: "He's a lumberjack and he's okay"},
  {line: 4, words: "He sleeps all night and he works all day"}
];

_.chain(lyrics)
  .map(function(line) { return line.words.split(' '); })
  .flatten()
  .reduce(function(counts, word) {
    counts[word] = (counts[word] || 0) + 1;
    return counts;
  }, {})
  .value();

=> {lumberjack: 2, all: 4, night: 2 ... }
```

In addition, the [Array prototype's methods](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/prototype) are proxied through the chained Underscore object, so you can slip a `reverse` or a `push` into your chain, and continue to modify the array.

### chain

`_.chain(obj)` [source](https://underscorejs.org/docs/modules/chain.html)  

Returns a wrapped object. Calling methods on this object will continue to return wrapped objects until `value` is called.

```js
var stooges = [{name: 'curly', age: 25}, {name: 'moe', age: 21}, {name: 'larry', age: 23}];
var youngest = _.chain(stooges)
  .sortBy(function(stooge){ return stooge.age; })
  .map(function(stooge){ return stooge.name + ' is ' + stooge.age; })
  .first()
  .value();
=> "moe is 21"
```

### value

`_.chain(obj).value()` [source](https://underscorejs.org/docs/modules/underscore.html)  

Extracts the value of a wrapped object.

```js
_.chain([1, 2, 3]).reverse().value();
=> [3, 2, 1]
```
