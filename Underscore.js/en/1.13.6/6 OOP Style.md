[TOC]

You can use Underscore in either an object-oriented or a functional style, depending on your preference. The following two lines of code are identical ways to double a list of numbers. [source](https://underscorejs.org/docs/modules/underscore.html), [source](https://underscorejs.org/docs/modules/mixin.html)

```js
_.map([1, 2, 3], function(n){ return n * 2; });
_([1, 2, 3]).map(function(n){ return n * 2; });
```