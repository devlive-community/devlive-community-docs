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
