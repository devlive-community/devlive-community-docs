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

### ap

---

`[a → b] → [a] → [b]`

`Apply f => f (a → b) → f a → f b`

`(r → a → b) → (r → a) → (r → b)`

Added in v0.3.0

ap applies a list of functions to a list of values.

Dispatches to the `ap` method of the first argument, if present. Also treats curried functions as applicatives.

```js
R.ap([R.multiply(2), R.add(3)], [1,2,3]); //=> [2, 4, 6, 4, 5, 6]
R.ap([R.concat('tasty '), R.toUpper], ['pizza', 'salad']); //=> ["tasty pizza", "tasty salad", "PIZZA", "SALAD"]

// R.ap can also be used as S combinator
// when only two functions are passed
R.ap(R.concat, R.toUpper)('Ramda') //=> 'RamdaRAMDA'
```

### empty

---

`a → a`

Added in v0.3.0

Returns the empty value of its argument's type. Ramda defines the empty value of Array (`[]`), Object (`{}`), String (`''`), TypedArray (`Uint8Array []`, `Float32Array []`, etc), and Arguments. Other types are supported if they define `<Type>.empty`, `<Type>.prototype.empty` or implement the [FantasyLand Monoid spec](https://github.com/fantasyland/fantasy-land#monoid).

Dispatches to the `empty` method of the first argument, if present.

```js
R.empty(Just(42));               //=> Nothing()
R.empty([1, 2, 3]);              //=> []
R.empty('unicorns');             //=> ''
R.empty({x: 1, y: 2});           //=> {}
R.empty(Uint8Array.from('123')); //=> Uint8Array []
```

### of

---

`(* → {*}) → a → {a}`

Parameters

*   CtorA constructor
*   valany value

> Returns * An instance of the `Ctor` wrapping `val`.

Added in v0.3.0

```js
R.of(Array, 42);   //=> [42]
R.of(Array, [42]); //=> [[42]]
R.of(Maybe, 42);   //=> Maybe.Just(42)
```

### constructN

---

`Number → (* → {*}) → (* → {*})`

Parameters

*   nThe arity of the constructor function.
*   FnThe constructor function to wrap.

> Returns function A wrapped, curried constructor function.

Added in v0.4.0

Wraps a constructor function inside a curried function that can be called with the same arguments and returns the same type. The arity of the function returned is specified to allow using variadic constructor functions.

```js
// Variadic Constructor function
function Salad() {
  this.ingredients = arguments;
}

Salad.prototype.recipe = function() {
  const instructions = R.map(ingredient => 'Add a dollop of ' + ingredient, this.ingredients);
  return R.join('\n', instructions);
};

const ThreeLayerSalad = R.constructN(3, Salad);

// Notice we no longer need the 'new' keyword, and the constructor is curried for 3 arguments.
const salad = ThreeLayerSalad('Mayonnaise')('Potato Chips')('Ketchup');

console.log(salad.recipe());
// Add a dollop of Mayonnaise
// Add a dollop of Potato Chips
// Add a dollop of Ketchup
```

### converge

---

`((x1, x2, …) → z) → [((a, b, …) → x1), ((a, b, …) → x2), …] → (a → b → … → z)`

Parameters

*   afterA function. `after` will be invoked with the return values of `fn1` and `fn2` as its arguments.
*   functionsA list of functions.

> Returns function A new function.

Added in v0.4.2

Accepts a converging function and a list of branching functions and returns a new function. The arity of the new function is the same as the arity of the longest branching function. When invoked, this new function is applied to some arguments, and each branching function is applied to those same arguments. The results of each branching function are passed as arguments to the converging function to produce the return value.

See also [useWith](#useWith).

```js
const average = R.converge(R.divide, [R.sum, R.length])
average([1, 2, 3, 4, 5, 6, 7]) //=> 4

const strangeConcat = R.converge(R.concat, [R.toUpper, R.toLower])
strangeConcat("Yodel") //=> "YODELyodel"
```

### curryN

---

`Number → (* → a) → (* → a)`

Parameters

*   lengthThe arity for the returned function.
*   fnThe function to curry.

> Returns function A new, curried function.

Added in v0.5.0

Returns a curried equivalent of the provided function, with the specified arity. The curried function has two unusual capabilities. First, its arguments needn't be provided one at a time. If `g` is `R.curryN(3, f)`, the following are equivalent:

```js
*   `g(1)(2)(3)`
*   `g(1)(2, 3)`
*   `g(1, 2)(3)`
*   `g(1, 2, 3)`
```

Secondly, the special placeholder value [`R.__`](#__) may be used to specify "gaps", allowing partial application of any combination of arguments, regardless of their positions. If `g` is as above and `_` is [`R.__`](#__), the following are equivalent:

```js
*   `g(1, 2, 3)`
*   `g(_, 2, 3)(1)`
*   `g(_, _, 3)(1)(2)`
*   `g(_, _, 3)(1, 2)`
*   `g(_, 2)(1)(3)`
*   `g(_, 2)(1, 3)`
*   `g(_, 2)(_, 3)(1)`
```

See also [curry](#curry).

```js
const sumArgs = (...args) => R.sum(args);

const curriedAddFourNumbers = R.curryN(4, sumArgs);
const f = curriedAddFourNumbers(1, 2);
const g = f(3);
g(4); //=> 10
```

### __

---

Added in v0.6.0

A special placeholder value used to specify "gaps" within curried functions, allowing partial application of any combination of arguments, regardless of their positions.

If `g` is a curried ternary function and `_` is `R.__`, the following are equivalent:

*   `g(1, 2, 3)`
*   `g(_, 2, 3)(1)`
*   `g(_, _, 3)(1)(2)`
*   `g(_, _, 3)(1, 2)`
*   `g(_, 2, _)(1, 3)`
*   `g(_, 2)(1)(3)`
*   `g(_, 2)(1, 3)`
*   `g(_, 2)(_, 3)(1)`

```js
const greet = R.replace('{name}', R.__, 'Hello, {name}!');
greet('Alice'); //=> 'Hello, Alice!'
```

### bind

---

`(* → *) → {*} → (* → *)`

Parameters

*   fnThe function to bind to context
*   thisObjThe context to bind `fn` to

> Returns function A function that will execute in the context of `thisObj`.

Added in v0.6.0

Creates a function that is bound to a context. Note: `R.bind` does not provide the additional argument-binding capabilities of [Function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

See also [partial](#partial).

```js
const log = R.bind(console.log, console);
R.pipe(R.assoc('a', 2), R.tap(log), R.assoc('a', 3))({a: 1}); //=> {a: 3}
// logs {a: 2}
```

### apply

---

`(*… → a) → [*] → a`

Parameters

*   fnThe function which will be called with `args`
*   argsThe arguments to call `fn` with

> Returns * result The result, equivalent to `fn(...args)`

Added in v0.7.0

Applies function `fn` to the argument list `args`. This is useful for creating a fixed-arity function from a variadic function. `fn` should be a bound function if context is significant.

See also [call](#call), [unapply](#unapply).

```js
const nums = [1, 2, 3, -99, 42, 6, 7];
R.apply(Math.max, nums); //=> 42
```

### lift

---

`(*… → *) → ([*]… → [*])`

Parameters

*   fnThe function to lift into higher context

> Returns function The lifted function.

Added in v0.7.0

"lifts" a function of arity >= 1 so that it may "map over" a list, Function or other object that satisfies the [FantasyLand Apply spec](https://github.com/fantasyland/fantasy-land#apply).

See also [liftN](#liftN).

```js
const madd3 = R.lift((a, b, c) => a + b + c);

madd3([100, 200], [30, 40], [5, 6, 7]); //=> [135, 136, 137, 145, 146, 147, 235, 236, 237, 245, 246, 247]

const madd5 = R.lift((a, b, c, d, e) => a + b + c + d + e);

madd5([10, 20], [1], [2, 3], [4], [100, 200]); //=> [117, 217, 118, 218, 127, 227, 128, 228]
```

### liftN

---

`Number → (*… → *) → ([*]… → [*])`

Parameters

*   fnThe function to lift into higher context

> Returns function The lifted function.

Added in v0.7.0

"lifts" a function to be the specified arity, so that it may "map over" that many lists, Functions or other objects that satisfy the [FantasyLand Apply spec](https://github.com/fantasyland/fantasy-land#apply).

See also [lift](#lift), [ap](#ap).

```js
const madd3 = R.liftN(3, (...args) => R.sum(args));
madd3([1,2,3], [1,2,3], [1]); //=> [3, 4, 5, 4, 5, 6, 5, 6, 7]
```

### unapply

---

`([*…] → a) → (*… → a)`

Added in v0.8.0

Takes a function `fn`, which takes a single array argument, and returns a function which:

*   takes any number of positional arguments;
*   passes these arguments to `fn` as an array; and
*   returns the result.

In other words, `R.unapply` derives a variadic function from a function which takes an array. `R.unapply` is the inverse of [`R.apply`](#apply).

See also [apply](#apply).

```js
R.unapply(JSON.stringify)(1, 2, 3); //=> '[1,2,3]'
```

### call

---

`((*… → a), *…) → a`

Parameters

*   fnThe function to apply to the remaining arguments.
*   argsAny number of positional arguments.

> Returns *

Added in v0.9.0

Returns the result of calling its first argument with the remaining arguments. This is occasionally useful as a converging function for [`R.converge`](#converge): the first branch can produce a function while the remaining branches produce values to be passed to that function as its arguments.

See also [apply](#apply).

```js
R.call(R.add, 1, 2); //=> 3

const indentN = R.pipe(
  R.repeat(' '),
  R.join(''),
  R.replace(/^(?!$)/gm)
);

const format = R.converge(
  R.call,
  [
    R.pipe(R.prop('indent'), indentN),
    R.prop('value')
  ]
);

format({indent: 2, value: 'foo\nbar\nbaz\n'}); //=> '  foo\n  bar\n  baz\n'
```

### F

---

`* → Boolean`

Added in v0.9.0

A function that always returns `false`. Any passed in parameters are ignored.

See also [T](#T).

```js
R.F(); //=> false
```

### nthArg

---

`Number → *… → *`

Added in v0.9.0

Returns a function which returns its nth argument.

```js
R.nthArg(1)('a', 'b', 'c'); //=> 'b'
R.nthArg(-1)('a', 'b', 'c'); //=> 'c'
```

### T

---

`* → Boolean`

Added in v0.9.0

A function that always returns `true`. Any passed in parameters are ignored.

See also [F](#F).

```js
R.T(); //=> true
```

### partial

---

`((a, b, c, …, n) → x) → [a, b, c, …] → ((d, e, f, …, n) → x)`

Added in v0.10.0

Takes a function `f` and a list of arguments, and returns a function `g`. When applied, `g` returns the result of applying `f` to the arguments provided initially followed by the arguments provided to `g`.

See also [partialRight](#partialRight), [curry](#curry).

```js
const multiply2 = (a, b) => a * b;
const double = R.partial(multiply2, [2]);
double(3); //=> 6

const greet = (salutation, title, firstName, lastName) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const sayHello = R.partial(greet, ['Hello']);
const sayHelloToMs = R.partial(sayHello, ['Ms.']);
sayHelloToMs('Jane', 'Jones'); //=> 'Hello, Ms. Jane Jones!'
```

### partialRight

---

`((a, b, c, …, n) → x) → [d, e, f, …, n] → ((a, b, c, …) → x)`

Added in v0.10.0

Takes a function `f` and a list of arguments, and returns a function `g`. When applied, `g` returns the result of applying `f` to the arguments provided to `g` followed by the arguments provided initially.

See also [partial](#partial).

```js
const greet = (salutation, title, firstName, lastName) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

const greetMsJaneJones = R.partialRight(greet, ['Ms.', 'Jane', 'Jones']);

greetMsJaneJones('Hello'); //=> 'Hello, Ms. Jane Jones!'
```

### uncurryN

---

`Number → (a → b → c … → z) → ((a → b → c …) → z)`

Parameters

*   lengthThe arity for the returned function.
*   fnThe function to uncurry.

> Returns function A new function.

Added in v0.14.0

Returns a function of arity `n` from a (manually) curried function. Note that, the returned function is actually a ramda style curryied function, which can accept one or more arguments in each function calling.

See also [curry](#curry), [curryN](#curryN).

```js
const addFour = a => b => c => d => a + b + c + d;

const uncurriedAddFour = R.uncurryN(4, addFour);
uncurriedAddFour(1, 2, 3, 4); //=> 10
```

### addIndex

---

`(((a …) → b) … → [a] → *) → (((a …, Int, [a]) → b) … → [a] → *)`

Parameters

*   fnA list iteration function that does not pass index or list to its callback

> Returns function An altered list iteration function that passes (item, index, list) to its callback

Added in v0.15.0

Creates a new list iteration function from an existing one by adding two new parameters to its callback function: the current index, and the entire list.

This would turn, for instance, [`R.map`](#map) function into one that more closely resembles `Array.prototype.map`. Note that this will only work for functions in which the iteration callback function is the first parameter, and where the list is the last parameter. (This latter might be unimportant if the list parameter is not used.)

```js
const mapIndexed = R.addIndex(R.map);
mapIndexed((val, idx) => idx + '-' + val, ['f', 'o', 'o', 'b', 'a', 'r']);
//=> ['0-f', '1-o', '2-o', '3-b', '4-a', '5-r']
```

### juxt

---

`[(a, b, …, m) → n] → ((a, b, …, m) → [n])`

Parameters

*   fnsAn array of functions

> Returns function A function that returns a list of values after applying each of the original \`fns\` to its parameters.

Added in v0.19.0

juxt applies a list of functions to a list of values.

See also [applySpec](#applySpec).

```js
const getRange = R.juxt([Math.min, Math.max]);
getRange(3, 4, 9, -3); //=> [-3, 9]
```

### applySpec

---

`{k: ((a, b, …, m) → v)} → ((a, b, …, m) → {k: v})`

Parameters

*   specan object recursively mapping properties to functions for producing the values for these properties.

> Returns function A function that returns an object of the same structure as \`spec', with each property set to the value returned by calling its associated function with the supplied arguments.

Added in v0.20.0

Given a spec object recursively mapping properties to functions, creates a function producing an object of the same structure, by mapping each property to the result of calling its associated function with the supplied arguments.

See also [converge](#converge), [juxt](#juxt).

```js
const getMetrics = R.applySpec({
  sum: R.add,
  nested: { mul: R.multiply }
});
getMetrics(2, 4); // => { sum: 6, nested: { mul: 8 } }
```

### tryCatch

---

`(…x → a) → ((e, …x) → a) → (…x → a)`

Parameters

*   tryerThe function that may throw.
*   catcherThe function that will be evaluated if `tryer` throws.

> Returns function A new function that will catch exceptions and send them to the catcher.

Added in v0.20.0

`tryCatch` takes two functions, a `tryer` and a `catcher`. The returned function evaluates the `tryer`; if it does not throw, it simply returns the result. If the `tryer` _does_ throw, the returned function evaluates the `catcher` function and returns its result. Note that for effective composition with this function, both the `tryer` and `catcher` functions must return the same type of results.

```js
R.tryCatch(R.prop('x'), R.F)({x: true}); //=> true
R.tryCatch(() => { throw 'foo'}, R.always('caught'))('bar') // =>
'caught'
R.tryCatch(R.times(R.identity), R.always([]))('s') // => []
R.tryCatch(() => { throw 'this is not a valid value'}, (err, value)=>({error : err,  value }))('bar') // => {'error': 'this is not a valid value', 'value': 'bar'}
```



