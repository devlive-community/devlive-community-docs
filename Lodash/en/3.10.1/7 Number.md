[TOC]

### _.inRange(n, [start=0], end)

Checks if `n` is between `start` and up to but not including, `end`. If
`end` is not specified it's set to `start` with `start` then set to `0`.

#### Arguments
1. `n` *(number)*: The number to check.
2. `[start=0]` *(number)*: The start of the range.
3. `end` *(number)*: The end of the range.

#### Returns
*(boolean)*:  Returns `true` if `n` is in the range, else `false`.

#### Example
```js
_.inRange(3, 2, 4);
// => true

_.inRange(4, 8);
// => true

_.inRange(4, 2);
// => false

_.inRange(2, 2);
// => false

_.inRange(1.2, 2);
// => true

_.inRange(5.2, 4);
// => false
```

### _.random([min=0], [max=1], [floating])

Produces a random number between `min` and `max` (inclusive). If only one
argument is provided a number between `0` and the given number is returned.
If `floating` is `true`, or either `min` or `max` are floats, a floating-point
number is returned instead of an integer.

#### Arguments
1. `[min=0]` *(number)*: The minimum possible value.
2. `[max=1]` *(number)*: The maximum possible value.
3. `[floating]` *(boolean)*: Specify returning a floating-point number.

#### Returns
*(number)*:  Returns the random number.

#### Example
```js
_.random(0, 5);
// => an integer between 0 and 5

_.random(5);
// => also an integer between 0 and 5

_.random(5, true);
// => a floating-point number between 0 and 5

_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```
