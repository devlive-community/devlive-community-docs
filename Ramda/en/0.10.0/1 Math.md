[TOC]

### add

-----------------------------------------------------------------------------------------------------

`Number → Number → Number`

Added in v0.1.0

Adds two values.

See also [subtract](#subtract).

```js
R.add(2, 3);       //=>  5
R.add(7)(10);      //=> 17
```

### divide

--------------------------------------------------------------------------------------------------------------

`Number → Number → Number`

Parameters

*   aThe first value.

*   bThe second value.

> Returns Number The result of `a / b`.

Added in v0.1.0

Divides two numbers. Equivalent to `a / b`.

See also [multiply](#multiply).

```js
R.divide(71, 100); //=> 0.71

const half = R.divide(R.__, 2);
half(42); //=> 21

const reciprocal = R.divide(1);
reciprocal(4);   //=> 0.25
```

### multiply

--------------------------------------------------------------------------------------------------------------------

`Number → Number → Number`

Parameters

*   aThe first value.
*   bThe second value.

> Returns Number The result of `a * b`.

Added in v0.1.0

Multiplies two numbers. Equivalent to `a * b` but curried.

See also [divide](#divide).

```js
const double = R.multiply(2);
const triple = R.multiply(3);
double(3);       //=>  6
triple(4);       //=> 12
R.multiply(2, 5);  //=> 10
```

### product

---

`[Number] → Number`

Parameters

*   listAn array of numbers

> Returns Number The product of all the numbers in the list.

Added in v0.1.0

Multiplies together all the elements of a list.

See also [reduce](#reduce).

```js
R.product([2,4,6,8,100,1]); //=> 38400
```

### subtract

---

`Number → Number → Number`

Parameters

*   aThe first value.
*   bThe second value.

> Returns Number The result of `a - b`.

Added in v0.1.0

Subtracts its second argument from its first argument.

See also [add](#add).

```js
R.subtract(10, 8); //=> 2

const minus5 = R.subtract(R.__, 5);
minus5(17); //=> 12

const complementaryAngle = R.subtract(90);
complementaryAngle(30); //=> 60
complementaryAngle(72); //=> 18
```

### sum

---

`[Number] → Number`

Parameters

*   listAn array of numbers

> Returns Number The sum of all the numbers in the list.

Added in v0.1.0

Adds together all the elements of a list.

See also [reduce](#reduce).

```js
R.sum([2,4,6,8,100,1]); //=> 121
```

### modulo

---

`Number → Number → Number`

Parameters

*   aThe value to the divide.
*   bThe pseudo-modulus

> Returns Number The result of `b % a`.

Added in v0.1.1

Divides the first parameter by the second and returns the remainder. Note that this function preserves the JavaScript-style behavior for modulo. For mathematical modulo see [`mathMod`](#mathMod).

See also [mathMod](#mathMod).

```js
R.modulo(17, 3); //=> 2
// JS behavior:
R.modulo(-17, 3); //=> -2
R.modulo(17, -3); //=> 2

const isOdd = R.modulo(R.__, 2);
isOdd(42); //=> 0
isOdd(21); //=> 1
```

### mathMod

---

`Number → Number → Number`

Parameters

*   mThe dividend.
*   pthe modulus.

> Returns Number The result of `b mod a`.

Added in v0.3.0

`mathMod` behaves like the modulo operator should mathematically, unlike the `%` operator (and by extension, [`R.modulo`](#modulo)). So while `-17 % 5` is `-2`, `mathMod(-17, 5)` is `3`. `mathMod` requires Integer arguments, and returns NaN when the modulus is zero or negative.

See also [modulo](#modulo).

```js
R.mathMod(-17, 5);  //=> 3
R.mathMod(17, 5);   //=> 2
R.mathMod(17, -5);  //=> NaN
R.mathMod(17, 0);   //=> NaN
R.mathMod(17.2, 5); //=> NaN
R.mathMod(17, 5.3); //=> NaN

const clock = R.mathMod(R.__, 12);
clock(15); //=> 3
clock(24); //=> 0

const seventeenMod = R.mathMod(17);
seventeenMod(3);  //=> 2
seventeenMod(4);  //=> 1
seventeenMod(10); //=> 7
```

### de

---

`Number → Number`

Added in v0.9.0

Decrements its argument.

See also [inc](#inc).

```js
R.dec(42); //=> 41
```

### inc

---

`Number → Number`

Added in v0.9.0

Increments its argument.

See also [dec](#dec).

```js
R.inc(42); //=> 43
```

### negate

---

`Number → Number`

Added in v0.9.0

Negates its argument.

```js
R.negate(42); //=> -42
```
