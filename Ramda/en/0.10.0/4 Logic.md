[TOC]

### and

------------------------------------------------------------------------------------------------------

`a → b → a | b`

Added in v0.1.0

Returns the first argument if it is falsy, otherwise the second argument. Acts as the boolean `and` statement if both inputs are `Boolean`s.

See also [both](#both), [or](#or).

```js
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```

### isEmpty

------------------------------------------------------------------------------------------------------------------

`a → Boolean`

Added in v0.1.0

Returns `true` if the given value is its type's empty value; `false` otherwise.

See also [empty](#empty), [isNotEmpty](#isNotEmpty).

```js
R.isEmpty([1, 2, 3]);           //=> false
R.isEmpty([]);                  //=> true
R.isEmpty('');                  //=> true
R.isEmpty(null);                //=> false
R.isEmpty({});                  //=> true
R.isEmpty({length: 0});         //=> false
R.isEmpty(Uint8Array.from('')); //=> true
```

### not

------------------------------------------------------------------------------------------------------

`* → Boolean`

Parameters

*   aany value

> Returns Boolean the logical inverse of passed argument.

Added in v0.1.0

A function that returns the `!` of its argument. It will return `true` when passed false-y value, and `false` when passed a truth-y one.

See also [complement](#complement).

```js
R.not(true); //=> false
R.not(false); //=> true
R.not(0); //=> true
R.not(1); //=> false
```

### or

---------------------------------------------------------------------------------------------------

`a → b → a | b`

Added in v0.1.0

Returns the first argument if it is truthy, otherwise the second argument. Acts as the boolean `or` statement if both inputs are `Boolean`s.

See also [either](#either), [and](#and).

```js
R.or(true, true); //=> true
R.or(true, false); //=> true
R.or(false, true); //=> true
R.or(false, false); //=> false
```

### cond

---

`[[(*… → Boolean),(*… → *)]] → (*… → *)`

Parameters

*   pairsA list of [predicate, transformer]

> Returns function

Added in v0.6.0

Returns a function, `fn`, which encapsulates `if/else, if/else, ...` logic. `R.cond` takes a list of \[predicate, transformer\] pairs. All of the arguments to `fn` are applied to each of the predicates in turn until one returns a "truthy" value, at which point `fn` returns the result of applying its arguments to the corresponding transformer. If none of the predicates matches, `fn` returns undefined.

**Please note**: This is not a direct substitute for a `switch` statement. Remember that both elements of every pair passed to `cond` are _functions_, and `cond` returns a function.

See also [ifElse](#ifElse), [unless](#unless), [when](#when).

```js
const fn = R.cond([
  [R.equals(0),   R.always('water freezes at 0°C')],
  [R.equals(100), R.always('water boils at 100°C')],
  [R.T,           temp => 'nothing special happens at ' + temp + '°C']
]);
fn(0); //=> 'water freezes at 0°C'
fn(50); //=> 'nothing special happens at 50°C'
fn(100); //=> 'water boils at 100°C'
```

### ifElse

---

`(*… → Boolean) → (*… → *) → (*… → *) → (*… → *)`

Parameters

*   conditionA predicate function
*   onTrueA function to invoke when the `condition` evaluates to a truthy value.
*   onFalseA function to invoke when the `condition` evaluates to a falsy value.

> Returns function A new function that will process either the `onTrue` or the `onFalse` function depending upon the result of the \`condition\` predicate.

Added in v0.8.0

Creates a function that will process either the `onTrue` or the `onFalse` function depending upon the result of the `condition` predicate.

Note that `ifElse` takes its arity from the longest of the three functions passed to it.

See also [unless](#unless), [when](#when), [cond](#cond).

```js
const incCount = R.ifElse(
  R.has('count'),
  R.over(R.lensProp('count'), R.inc),
  R.assoc('count', 1)
);
incCount({ count: 1 }); //=> { count: 2 }
incCount({});           //=> { count: 1 }
```

### allPass

---

`[(*… → Boolean)] → (*… → Boolean)`

Parameters

*   predicatesAn array of predicates to check

> Returns function The combined predicate

Added in v0.9.0

Takes a list of predicates and returns a predicate that returns true for a given list of arguments if every one of the provided predicates is satisfied by those arguments.

The function returned is a curried function whose arity matches that of the highest-arity predicate.

See also [anyPass](#anyPass), [both](#both).

```js
const isQueen = R.propEq('Q', 'rank');
const isSpade = R.propEq('♠︎', 'suit');
const isQueenOfSpades = R.allPass([isQueen, isSpade]);

isQueenOfSpades({rank: 'Q', suit: '♣︎'}); //=> false
isQueenOfSpades({rank: 'Q', suit: '♠︎'}); //=> true
```

### anyPass

---

`[(*… → Boolean)] → (*… → Boolean)`

Parameters

*   predicatesAn array of predicates to check

> Returns function The combined predicate

Added in v0.9.0

Takes a list of predicates and returns a predicate that returns true for a given list of arguments if at least one of the provided predicates is satisfied by those arguments.

The function returned is a curried function whose arity matches that of the highest-arity predicate.

See also [allPass](#allPass), [either](#either).

```js
const isClub = R.propEq('♣', 'suit');
const isSpade = R.propEq('♠', 'suit');
const isBlackCard = R.anyPass([isClub, isSpade]);

isBlackCard({rank: '10', suit: '♣'}); //=> true
isBlackCard({rank: 'Q', suit: '♠'}); //=> true
isBlackCard({rank: 'Q', suit: '♦'}); //=> false
```

### defaultTo

---

`a → b → a | b`

Parameters

*   defaultThe default value.
*   val`val` will be returned instead of `default` unless `val` is `null`, `undefined` or `NaN`.

> Returns * The second value if it is not `null`, `undefined` or `NaN`, otherwise the default value

Added in v0.10.0

Returns the second argument if it is not `null`, `undefined` or `NaN`; otherwise the first argument is returned.

```js
const defaultTo42 = R.defaultTo(42);

defaultTo42(null);  //=> 42
defaultTo42(undefined);  //=> 42
defaultTo42(false);  //=> false
defaultTo42('Ramda');  //=> 'Ramda'
// parseInt('string') results in NaN
defaultTo42(parseInt('string')); //=> 42
```
