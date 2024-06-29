[TOC]

### `_.add(augend, addend)`

Adds two numbers.

#### Since
3.4.0

#### Arguments
1. `augend` *(number)*: The first number in an addition.
2. `addend` *(number)*: The second number in an addition.

#### Returns
*(number)*: Returns the total.

#### Example
```js
_.add(6, 4);
// => 10
```

### `_.ceil(number, [precision=0])`

Computes `number` rounded up to `precision`.

#### Since
3.10.0

#### Arguments
1. `number` *(number)*: The number to round up.
2. `[precision=0]` *(number)*: The precision to round up to.

#### Returns
*(number)*: Returns the rounded up number.

#### Example
```js
_.ceil(4.006);
// => 5

_.ceil(6.004, 2);
// => 6.01

_.ceil(6040, -2);
// => 6100
```

### `_.divide(dividend, divisor)`

Divide two numbers.

#### Since
4.7.0

#### Arguments
1. `dividend` *(number)*: The first number in a division.
2. `divisor` *(number)*: The second number in a division.

#### Returns
*(number)*: Returns the quotient.

#### Example
```js
_.divide(6, 4);
// => 1.5
```

### `_.floor(number, [precision=0])`

Computes `number` rounded down to `precision`.

#### Since
3.10.0

#### Arguments
1. `number` *(number)*: The number to round down.
2. `[precision=0]` *(number)*: The precision to round down to.

#### Returns
*(number)*: Returns the rounded down number.

#### Example
```js
_.floor(4.006);
// => 4

_.floor(0.046, 2);
// => 0.04

_.floor(4060, -2);
// => 4000
```

### `_.max(array)`

Computes the maximum value of `array`. If `array` is empty or falsey,
`undefined` is returned.

#### Since
0.1.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.

#### Returns
*(&#42;)*: Returns the maximum value.

#### Example
```js
_.max([4, 2, 8, 6]);
// => 8

_.max([]);
// => undefined
```

### `_.maxBy(array, [iteratee=_.identity])`

This method is like `_.max` except that it accepts `iteratee` which is
invoked for each element in `array` to generate the criterion by which
the value is ranked. The iteratee is invoked with one argument: *(value)*.

#### Since
4.0.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The iteratee invoked per element.

#### Returns
*(&#42;)*: Returns the maximum value.

#### Example
```js
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }

// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

### `_.mean(array)`

Computes the mean of the values in `array`.

#### Since
4.0.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.

#### Returns
*(number)*: Returns the mean.

#### Example
```js
_.mean([4, 2, 8, 6]);
// => 5
```

### `_.meanBy(array, [iteratee=_.identity])`

This method is like `_.mean` except that it accepts `iteratee` which is
invoked for each element in `array` to generate the value to be averaged.
The iteratee is invoked with one argument: *(value)*.

#### Since
4.7.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The iteratee invoked per element.

#### Returns
*(number)*: Returns the mean.

#### Example
```js
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.meanBy(objects, function(o) { return o.n; });
// => 5

// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

### `_.min(array)`

Computes the minimum value of `array`. If `array` is empty or falsey,
`undefined` is returned.

#### Since
0.1.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.

#### Returns
*(&#42;)*: Returns the minimum value.

#### Example
```js
_.min([4, 2, 8, 6]);
// => 2

_.min([]);
// => undefined
```

### `_.minBy(array, [iteratee=_.identity])`

This method is like `_.min` except that it accepts `iteratee` which is
invoked for each element in `array` to generate the criterion by which
the value is ranked. The iteratee is invoked with one argument: *(value)*.

#### Since
4.0.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The iteratee invoked per element.

#### Returns
*(&#42;)*: Returns the minimum value.

#### Example
```js
var objects = [{ 'n': 1 }, { 'n': 2 }];

_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }

// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

### `_.multiply(multiplier, multiplicand)`

Multiply two numbers.

#### Since
4.7.0

#### Arguments
1. `multiplier` *(number)*: The first number in a multiplication.
2. `multiplicand` *(number)*: The second number in a multiplication.

#### Returns
*(number)*: Returns the product.

#### Example
```js
_.multiply(6, 4);
// => 24
```

### `_.round(number, [precision=0])`

Computes `number` rounded to `precision`.

#### Since
3.10.0

#### Arguments
1. `number` *(number)*: The number to round.
2. `[precision=0]` *(number)*: The precision to round to.

#### Returns
*(number)*: Returns the rounded number.

#### Example
```js
_.round(4.006);
// => 4

_.round(4.006, 2);
// => 4.01

_.round(4060, -2);
// => 4100
```

### `_.subtract(minuend, subtrahend)`

Subtract two numbers.

#### Since
4.0.0

#### Arguments
1. `minuend` *(number)*: The first number in a subtraction.
2. `subtrahend` *(number)*: The second number in a subtraction.

#### Returns
*(number)*: Returns the difference.

#### Example
```js
_.subtract(6, 4);
// => 2
```

### `_.sum(array)`

Computes the sum of the values in `array`.

#### Since
3.4.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.

#### Returns
*(number)*: Returns the sum.

#### Example
```js
_.sum([4, 2, 8, 6]);
// => 20
```

### `_.sumBy(array, [iteratee=_.identity])`

This method is like `_.sum` except that it accepts `iteratee` which is
invoked for each element in `array` to generate the value to be summed.
The iteratee is invoked with one argument: *(value)*.

#### Since
4.0.0

#### Arguments
1. `array` *(Array)*: The array to iterate over.
2. `[iteratee=_.identity]` *(Function)*: The iteratee invoked per element.

#### Returns
*(number)*: Returns the sum.

#### Example
```js
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];

_.sumBy(objects, function(o) { return o.n; });
// => 20

// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```
