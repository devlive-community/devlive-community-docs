[TOC]

### always

------------------------------------------------------------------------------------------------------------------

`a → (* → a)`

Parameters

* valThe value to wrap in a function

> Returns function A Function :: \* -> val.

Added in v0.1.0

Returns a function that always returns the given value. Note that for non-primitives the value returned is a reference to the original value.

This function is known as `const`, `constant`, or `K` (for K combinator) in other languages and libraries.

```js
const t = R.always('Tee');
t(); //=> 'Tee'
```

### comparator

------------------------------------------------------------------------------------------------------------------------------

`((a, b) → Boolean) → ((a, b) → Number)`

Parameters

*   predA predicate function of arity two which will return `true` if the first argument is less than the second, `false` otherwise

> Returns function A Function :: a -> b -> Int that returns \`-1\` if a < b, \`1\` if b < a, otherwise \`0\`

Added in v0.1.0

Makes a comparator function out of a function that reports whether the first element is less than the second.

```js
const byAge = R.comparator((a, b) => a.age < b.age);
const people = [
  { name: 'Emma', age: 70 },
  { name: 'Peter', age: 78 },
  { name: 'Mikhail', age: 62 },
];
const peopleByIncreasingAge = R.sort(byAge, people);
  //=> [{ name: 'Mikhail', age: 62 },{ name: 'Emma', age: 70 }, { name: 'Peter', age: 78 }]
```

### compose

---------------------------------------------------------------------------------------------------------------------

`((y → z), (x → y), …, (o → p), ((a, b, …, n) → o)) → ((a, b, …, n) → z)`

Parameters

*   ...functionsThe functions to compose

> Returns function

Added in v0.1.0

Performs right-to-left function composition. The last argument may have any arity; the remaining arguments must be unary.

**Note:** The result of compose is not automatically curried.

See also [pipe](#pipe).

```js
const classyGreeting = (firstName, lastName) => "The name's " + lastName + ", " + firstName + " " + lastName
const yellGreeting = R.compose(R.toUpper, classyGreeting);
yellGreeting('James', 'Bond'); //=> "THE NAME'S BOND, JAMES BOND"

R.compose(Math.abs, R.add(1), R.multiply(2))(-4) //=> 7
```

### construct

---------------------------------------------------------------------------------------------------------------------------

`(* → {*}) → (* → {*})`

Parameters

*   fnThe constructor function to wrap.

> Returns function A wrapped, curried constructor function.

Added in v0.1.0

Wraps a constructor function inside a curried function that can be called with the same arguments and returns the same type.

See also [invoker](#invoker).

```js
// Constructor function
function Animal(kind) {
  this.kind = kind;
};
Animal.prototype.sighting = function() {
  return "It's a " + this.kind + "!";
}

const AnimalConstructor = R.construct(Animal)

// Notice we no longer need the 'new' keyword:
AnimalConstructor('Pig'); //=> {"kind": "Pig", "sighting": function (){...}};

const animalTypes = ["Lion", "Tiger", "Bear"];
const animalSighting = R.invoker(0, 'sighting');
const sightNewAnimal = R.compose(animalSighting, AnimalConstructor);
R.map(sightNewAnimal, animalTypes); //=> ["It's a Lion!", "It's a Tiger!", "It's a Bear!"]
```

### curry

---------------------------------------------------------------------------------------------------------------

`(* → a) → (* → a)`

Parameters

*   fnThe function to curry.

> Returns function A new, curried function.

Added in v0.1.0

Returns a curried equivalent of the provided function. The curried function has two unusual capabilities. First, its arguments needn't be provided one at a time. If `f` is a ternary function and `g` is `R.curry(f)`, the following are equivalent:

*   `g(1)(2)(3)`
*   `g(1)(2, 3)`
*   `g(1, 2)(3)`
*   `g(1, 2, 3)`

Secondly, the special placeholder value [`R.__`](#__) may be used to specify "gaps", allowing partial application of any combination of arguments, regardless of their positions. If `g` is as above and `_` is [`R.__`](#__), the following are equivalent:

*   `g(1, 2, 3)`
*   `g(_, 2, 3)(1)`
*   `g(_, _, 3)(1)(2)`
*   `g(_, _, 3)(1, 2)`
*   `g(_, 2)(1)(3)`
*   `g(_, 2)(1, 3)`
*   `g(_, 2)(_, 3)(1)`

Please note that default parameters don't count towards a [function arity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length) and therefore `curry` won't work well with those.

See also [curryN](#curryN), [partial](#partial).

```js
const addFourNumbers = (a, b, c, d) => a + b + c + d;
const curriedAddFourNumbers = R.curry(addFourNumbers);
const f = curriedAddFourNumbers(1, 2);
const g = f(3);
g(4); //=> 10

// R.curry not working well with default parameters
const h = R.curry((a, b, c = 2) => a + b + c);
h(1)(2)(7); //=> Error! (`3` is not a function!)
```

### useWith

---------------------------------------------------------------------------------------------------------------------

`((x1, x2, …) → z) → [(a → x1), (b → x2), …] → (a → b → … → z)`

Parameters

*   fnThe function to wrap.
*   transformersA list of transformer functions

> Returns function The wrapped function.

Added in v0.1.0

Accepts a function `fn` and a list of transformer functions and returns a new curried function. When the new function is invoked, it calls the function `fn` with parameters consisting of the result of calling each supplied handler on successive arguments to the new function.

If more arguments are passed to the returned function than transformer functions, those arguments are passed directly to `fn` as additional parameters. If you expect additional arguments that don't need to be transformed, although you can ignore them, it's best to pass an identity function so that the new function reports the correct arity.

See also [converge](#converge).

```js
R.useWith(Math.pow, [R.identity, R.identity])(3, 4); //=> 81
R.useWith(Math.pow, [R.identity, R.identity])(3)(4); //=> 81
R.useWith(Math.pow, [R.dec, R.inc])(3, 4); //=> 32
R.useWith(Math.pow, [R.dec, R.inc])(3)(4); //=> 32
```

### flip

------------------------------------------------------------------------------------------------------------

`((a, b, c, …) → z) → (b → a → c → … → z)`

Parameters

*   fnThe function to invoke with its first two parameters reversed.

> Returns * The result of invoking `fn` with its first two parameters' order reversed.

Added in v0.1.0

Returns a new function much like the supplied one, except that the first two arguments' order is reversed.

```js
const mergeThree = (a, b, c) => [].concat(a, b, c);

mergeThree(1, 2, 3); //=> [1, 2, 3]

R.flip(mergeThree)(1, 2, 3); //=> [2, 1, 3]
```

### groupBy

-----------------------------------------------------------------------------------------------------------------

`Idx a => (b → a) → [b] → {a: [b]}`

`Idx = String | Int | Symbol`

Parameters

*   fnFunction :: a -> Idx
*   listThe array to group

> Returns Object An object with the output of `fn` for keys, mapped to arrays of elements that produced that key when passed to `fn`.

Added in v0.1.0

Splits a list into sub-lists stored in an object, based on the result of calling a key-returning function on each element, and grouping the results according to values returned.

Dispatches to the `groupBy` method of the second argument, if present.

Acts as a transducer if a transformer is given in list position.

See also [reduceBy](#reduceBy), [transduce](#transduce), [indexBy](#indexBy), [collectBy](#collectBy).

```js
const byGrade = R.groupBy(function(student) {
  const score = student.score;
  return score < 65 ? 'F' :
         score < 70 ? 'D' :
         score < 80 ? 'C' :
         score < 90 ? 'B' : 'A';
});
const students = [{name: 'Abby', score: 84},
                {name: 'Eddy', score: 58},
                // ...
                {name: 'Jack', score: 69}];
byGrade(students);
// {
//   'A': [{name: 'Dianne', score: 99}],
//   'B': [{name: 'Abby', score: 84}]
//   // ...,
//   'F': [{name: 'Eddy', score: 58}]
// }
```

### identity

------------------------------------------------------------------------------------------------------------------------

`a → a`

Parameters

*   xThe value to return.

> Returns * The input value, `x`.

Added in v0.1.0

A function that does nothing but return the parameter supplied to it. Good as a default or placeholder function.

```js
R.identity(1); //=> 1

const obj = {};
R.identity(obj) === obj; //=> true
```

### invoker

---------------------------------------------------------------------------------------------------------------------

`Number → String → (a → b → … → n → Object → *)`

Parameters

*   arityNumber of arguments the returned function should take before the target object.
*   methodName of any of the target object's methods to call.

> Returns function A new curried function.

Added in v0.1.0

Given an `arity` (Number) and a `name` (String) the `invoker` function returns a curried function that takes `arity` arguments and a `context` object. It will "invoke" the `name`'d function (a method) on the `context` object.

See also [construct](#construct).

```js
// A function with no arguments
const asJson = invoker(0, "json")
// Just like calling .then((response) => response.json())
fetch("http://example.com/index.json").then(asJson)

// A function with one argument
const sliceFrom = invoker(1, 'slice');
sliceFrom(6, 'abcdefghijklm'); //=> 'ghijklm'

// A function with two arguments
const sliceFrom6 = invoker(2, 'slice')(6);
sliceFrom6(8, 'abcdefghijklm'); //=> 'gh'

// NOTE: You can't simply pass some of the arguments to the initial invoker function.
const firstCreditCardSection = invoker(2, "slice", 0, 4)
firstCreditCardSection("4242 4242 4242 4242") // => Function<...>

// Since invoker returns a curried function, you may partially apply it to create the function you need.
const firstCreditCardSection = invoker(2, "slice")(0, 4)
firstCreditCardSection("4242 4242 4242 4242") // => "4242"
```

### nAry

------------------------------------------------------------------------------------------------------------

`Number → (* → a) → (* → a)`

Parameters

*   nThe desired arity of the new function.
*   fnThe function to wrap.

> Returns function A new function wrapping `fn`. The new function is guaranteed to be of arity `n`.

Added in v0.1.0

Wraps a function of any arity (including nullary) in a function that accepts exactly `n` parameters. Any extraneous parameters will not be passed to the supplied function.

See also [binary](#binary), [unary](#unary).

```js
const takesTwoArgs = (a, b) => [a, b];

takesTwoArgs.length; //=> 2
takesTwoArgs(1, 2); //=> [1, 2]

const takesOneArg = R.nAry(1, takesTwoArgs);
takesOneArg.length; //=> 1
// Only `n` arguments are passed to the wrapped function
takesOneArg(1, 2); //=> [1, undefined]
```

### once

------------------------------------------------------------------------------------------------------------

`(a… → b) → (a… → b)`

Parameters

*   fnThe function to wrap in a call-only-once wrapper.

> Returns function The wrapped function.

Added in v0.1.0

Accepts a function `fn` and returns a function that guards invocation of `fn` such that `fn` can only ever be called once, no matter how many times the returned function is invoked. The first value calculated is returned in subsequent invocations.

```js
const addOneOnce = R.once(x => x + 1);
addOneOnce(10); //=> 11
addOneOnce(addOneOnce(50)); //=> 11
```

### pipe

------------------------------------------------------------------------------------------------------------

`(((a, b, …, n) → o), (o → p), …, (x → y), (y → z)) → ((a, b, …, n) → z)`

Parameters

*   functions

> Returns function

Added in v0.1.0

Performs left-to-right function composition. The first argument may have any arity; the remaining arguments must be unary.

In some libraries this function is named `sequence`.

**Note:** The result of pipe is not automatically curried.

See also [compose](#compose).

```js
const f = R.pipe(Math.pow, R.negate, R.inc);

f(3, 4); // -(3^4) + 1
```

### tap

---

`(a → *) → a → a`

Parameters

*   fnThe function to call with `x`. The return value of `fn` will be thrown away.
*   x

> Returns * `x`.

Added in v0.1.0

Runs the given function with the supplied object, then returns the object.

Acts as a transducer if a transformer is given as second parameter.

```js
const sayX = x => console.log('x is ' + x);
R.tap(sayX, 100); //=> 100
// logs 'x is 100'
```

### binary

---

`(a → b → c → … → z) → ((a, b) → z)`

Parameters

*   fnThe function to wrap.

> Returns function A new function wrapping `fn`. The new function is guaranteed to be of arity 2.

Added in v0.2.0

Wraps a function of any arity (including nullary) in a function that accepts exactly 2 parameters. Any extraneous parameters will not be passed to the supplied function.

See also [nAry](#nAry), [unary](#unary).

```js
const takesThreeArgs = function(a, b, c) {
  return [a, b, c];
};
takesThreeArgs.length; //=> 3
takesThreeArgs(1, 2, 3); //=> [1, 2, 3]

const takesTwoArgs = R.binary(takesThreeArgs);
takesTwoArgs.length; //=> 2
// Only 2 arguments are passed to the wrapped function
takesTwoArgs(1, 2, 3); //=> [1, 2, undefined]
```

### unary

---

`(a → b → c → … → z) → (a → z)`

Parameters

*   fnThe function to wrap.

> Returns function A new function wrapping `fn`. The new function is guaranteed to be of arity 1.

Added in v0.2.0

Wraps a function of any arity (including nullary) in a function that accepts exactly 1 parameter. Any extraneous parameters will not be passed to the supplied function.

See also [binary](#binary), [nAry](#nAry).

```js
const takesTwoArgs = function(a, b) {
  return [a, b];
};
takesTwoArgs.length; //=> 2
takesTwoArgs(1, 2); //=> [1, 2]

const takesOneArg = R.unary(takesTwoArgs);
takesOneArg.length; //=> 1
// Only 1 argument is passed to the wrapped function
takesOneArg(1, 2); //=> [1, undefined]
```
