[TOC]

### _.after(n, func)

The opposite of `_.before`; this method creates a function that invokes
`func` once it's called `n` or more times.

#### Arguments
1. `n` *(number)*: The number of calls before `func` is invoked.
2. `func` *(Function)*: The function to restrict.

#### Returns
*(Function)*:  Returns the new restricted function.

#### Example
```js
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('done saving!');
});

_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => logs 'done saving!' after the two async saves have completed
```

### _.ary(func, [n=func.length])

Creates a function that accepts up to `n` arguments ignoring any
additional arguments.

#### Arguments
1. `func` *(Function)*: The function to cap arguments for.
2. `[n=func.length]` *(number)*: The arity cap.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

### _.before(n, func)

Creates a function that invokes `func`, with the `this` binding and arguments
of the created function, while it's called less than `n` times. Subsequent
calls to the created function return the result of the last `func` invocation.

#### Arguments
1. `n` *(number)*: The number of calls at which `func` is no longer invoked.
2. `func` *(Function)*: The function to restrict.

#### Returns
*(Function)*:  Returns the new restricted function.

#### Example
```js
jQuery('#add').on('click', _.before(5, addContactToList));
// => allows adding up to 4 contacts to the list
```

### _.bind(func, thisArg, [partials])

Creates a function that invokes `func` with the `this` binding of `thisArg`
and prepends any additional `_.bind` arguments to those provided to the
bound function.
<br>
<br>
The `_.bind.placeholder` value, which defaults to `_` in monolithic builds,
may be used as a placeholder for partially applied arguments.
<br>
<br>
**Note:** Unlike native `Function#bind` this method does not set the "length"
property of bound functions.

#### Arguments
1. `func` *(Function)*: The function to bind.
2. `thisArg` *(&#42;)*: The `this` binding of `func`.
3. `[partials]` *(...&#42;)*: The arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new bound function.

#### Example
```js
var greet = function(greeting, punctuation) {
  return greeting + ' ' + this.user + punctuation;
};

var object = { 'user': 'fred' };

var bound = _.bind(greet, object, 'hi');
bound('!');
// => 'hi fred!'

// using placeholders
var bound = _.bind(greet, object, _, '!');
bound('hi');
// => 'hi fred!'
```

### _.bindAll(object, [methodNames])

Binds methods of an object to the object itself, overwriting the existing
method. Method names may be specified as individual arguments or as arrays
of method names. If no method names are provided all enumerable function
properties, own and inherited, of `object` are bound.
<br>
<br>
**Note:** This method does not set the "length" property of bound functions.

#### Arguments
1. `object` *(Object)*: The object to bind and assign the bound methods to.
2. `[methodNames]` *(...(string|string&#91;&#93;)*: The object method names to bind, specified as individual method names or arrays of method names.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
var view = {
  'label': 'docs',
  'onClick': function() {
    console.log('clicked ' + this.label);
  }
};

_.bindAll(view);
jQuery('#docs').on('click', view.onClick);
// => logs 'clicked docs' when the element is clicked
```

### _.bindKey(object, key, [partials])

Creates a function that invokes the method at `object[key]` and prepends
any additional `_.bindKey` arguments to those provided to the bound function.
<br>
<br>
This method differs from `_.bind` by allowing bound functions to reference
methods that may be redefined or don't yet exist.
See [Peter Michaux's article](http://peter.michaux.ca/articles/lazy-function-definition-pattern)
for more details.
<br>
<br>
The `_.bindKey.placeholder` value, which defaults to `_` in monolithic
builds, may be used as a placeholder for partially applied arguments.

#### Arguments
1. `object` *(Object)*: The object the method belongs to.
2. `key` *(string)*: The key of the method.
3. `[partials]` *(...&#42;)*: The arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new bound function.

#### Example
```js
var object = {
  'user': 'fred',
  'greet': function(greeting, punctuation) {
    return greeting + ' ' + this.user + punctuation;
  }
};

var bound = _.bindKey(object, 'greet', 'hi');
bound('!');
// => 'hi fred!'

object.greet = function(greeting, punctuation) {
  return greeting + 'ya ' + this.user + punctuation;
};

bound('!');
// => 'hiya fred!'

// using placeholders
var bound = _.bindKey(object, 'greet', _, '!');
bound('hi');
// => 'hiya fred!'
```

### _.curry(func, [arity=func.length])

Creates a function that accepts one or more arguments of `func` that when
called either invokes `func` returning its result, if all `func` arguments
have been provided, or returns a function that accepts one or more of the
remaining `func` arguments, and so on. The arity of `func` may be specified
if `func.length` is not sufficient.
<br>
<br>
The `_.curry.placeholder` value, which defaults to `_` in monolithic builds,
may be used as a placeholder for provided arguments.
<br>
<br>
**Note:** This method does not set the "length" property of curried functions.

#### Arguments
1. `func` *(Function)*: The function to curry.
2. `[arity=func.length]` *(number)*: The arity of `func`.

#### Returns
*(Function)*:  Returns the new curried function.

#### Example
```js
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]

curried(1, 2)(3);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// using placeholders
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

### _.curryRight(func, [arity=func.length])

This method is like `_.curry` except that arguments are applied to `func`
in the manner of `_.partialRight` instead of `_.partial`.
<br>
<br>
The `_.curryRight.placeholder` value, which defaults to `_` in monolithic
builds, may be used as a placeholder for provided arguments.
<br>
<br>
**Note:** This method does not set the "length" property of curried functions.

#### Arguments
1. `func` *(Function)*: The function to curry.
2. `[arity=func.length]` *(number)*: The arity of `func`.

#### Returns
*(Function)*:  Returns the new curried function.

#### Example
```js
var abc = function(a, b, c) {
  return [a, b, c];
};

var curried = _.curryRight(abc);

curried(3)(2)(1);
// => [1, 2, 3]

curried(2, 3)(1);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// using placeholders
curried(3)(1, _)(2);
// => [1, 2, 3]
```

### _.debounce(func, [wait=0], [options])

Creates a debounced function that delays invoking `func` until after `wait`
milliseconds have elapsed since the last time the debounced function was
invoked. The debounced function comes with a `cancel` method to cancel
delayed invocations. Provide an options object to indicate that `func`
should be invoked on the leading and/or trailing edge of the `wait` timeout.
Subsequent calls to the debounced function return the result of the last
`func` invocation.
<br>
<br>
**Note:** If `leading` and `trailing` options are `true`, `func` is invoked
on the trailing edge of the timeout only if the the debounced function is
invoked more than once during the `wait` timeout.
<br>
<br>
See [David Corbacho's article](http://drupalmotion.com/article/debounce-and-throttle-visual-explanation)
for details over the differences between `_.debounce` and `_.throttle`.

#### Arguments
1. `func` *(Function)*: The function to debounce.
2. `[wait=0]` *(number)*: The number of milliseconds to delay.
3. `[options]` *(Object)*: The options object.
4. `[options.leading=false]` *(boolean)*: Specify invoking on the leading edge of the timeout.
5. `[options.maxWait]` *(number)*: The maximum time `func` is allowed to be delayed before it's invoked.
6. `[options.trailing=true]` *(boolean)*: Specify invoking on the trailing edge of the timeout.

#### Returns
*(Function)*:  Returns the new debounced function.

#### Example
```js
// avoid costly calculations while the window size is in flux
jQuery(window).on('resize', _.debounce(calculateLayout, 150));

// invoke `sendMail` when the click event is fired, debouncing subsequent calls
jQuery('#postbox').on('click', _.debounce(sendMail, 300, {
  'leading': true,
  'trailing': false
}));

// ensure `batchLog` is invoked once after 1 second of debounced calls
var source = new EventSource('/stream');
jQuery(source).on('message', _.debounce(batchLog, 250, {
  'maxWait': 1000
}));

// cancel a debounced call
var todoChanges = _.debounce(batchLog, 1000);
Object.observe(models.todo, todoChanges);

Object.observe(models, function(changes) {
  if (_.find(changes, { 'user': 'todo', 'type': 'delete'})) {
    todoChanges.cancel();
  }
}, ['delete']);

// ...at some point `models.todo` is changed
models.todo.completed = true;

// ...before 1 second has passed `models.todo` is deleted
// which cancels the debounced `todoChanges` call
delete models.todo;
```

### _.defer(func, [args])

Defers invoking the `func` until the current call stack has cleared. Any
additional arguments are provided to `func` when it's invoked.

#### Arguments
1. `func` *(Function)*: The function to defer.
2. `[args]` *(...&#42;)*: The arguments to invoke the function with.

#### Returns
*(number)*:  Returns the timer id.

#### Example
```js
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// logs 'deferred' after one or more milliseconds
```

### _.delay(func, wait, [args])

Invokes `func` after `wait` milliseconds. Any additional arguments are
provided to `func` when it's invoked.

#### Arguments
1. `func` *(Function)*: The function to delay.
2. `wait` *(number)*: The number of milliseconds to delay invocation.
3. `[args]` *(...&#42;)*: The arguments to invoke the function with.

#### Returns
*(number)*:  Returns the timer id.

#### Example
```js
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => logs 'later' after one second
```

### _.flow([funcs])

Creates a function that returns the result of invoking the provided
functions with the `this` binding of the created function, where each
successive invocation is supplied the return value of the previous.

#### Arguments
1. `[funcs]` *(...Function)*: Functions to invoke.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
function square(n) {
  return n * n;
}

var addSquare = _.flow(_.add, square);
addSquare(1, 2);
// => 9
```

### _.flowRight([funcs])

This method is like `_.flow` except that it creates a function that
invokes the provided functions from right to left.

#### Aliases
*_.backflow, _.compose*

#### Arguments
1. `[funcs]` *(...Function)*: Functions to invoke.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
function square(n) {
  return n * n;
}

var addSquare = _.flowRight(square, _.add);
addSquare(1, 2);
// => 9
```

### _.memoize(func, [resolver])

Creates a function that memoizes the result of `func`. If `resolver` is
provided it determines the cache key for storing the result based on the
arguments provided to the memoized function. By default, the first argument
provided to the memoized function is coerced to a string and used as the
cache key. The `func` is invoked with the `this` binding of the memoized
function.
<br>
<br>
**Note:** The cache is exposed as the `cache` property on the memoized
function. Its creation may be customized by replacing the `_.memoize.Cache`
constructor with one whose instances implement the [`Map`](http://ecma-international.org/ecma-262/6.0/#sec-properties-of-the-map-prototype-object)
method interface of `get`, `has`, and `set`.

#### Arguments
1. `func` *(Function)*: The function to have its output memoized.
2. `[resolver]` *(Function)*: The function to resolve the cache key.

#### Returns
*(Function)*:  Returns the new memoizing function.

#### Example
```js
var upperCase = _.memoize(function(string) {
  return string.toUpperCase();
});

upperCase('fred');
// => 'FRED'

// modifying the result cache
upperCase.cache.set('fred', 'BARNEY');
upperCase('fred');
// => 'BARNEY'

// replacing `_.memoize.Cache`
var object = { 'user': 'fred' };
var other = { 'user': 'barney' };
var identity = _.memoize(_.identity);

identity(object);
// => { 'user': 'fred' }
identity(other);
// => { 'user': 'fred' }

_.memoize.Cache = WeakMap;
var identity = _.memoize(_.identity);

identity(object);
// => { 'user': 'fred' }
identity(other);
// => { 'user': 'barney' }
```

### _.modArgs(func, [transforms])

Creates a function that runs each argument through a corresponding
transform function.

#### Arguments
1. `func` *(Function)*: The function to wrap.
2. `[transforms]` *(...(Function|Function&#91;&#93;)*: The functions to transform arguments, specified as individual functions or arrays of functions.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
function doubled(n) {
  return n * 2;
}

function square(n) {
  return n * n;
}

var modded = _.modArgs(function(x, y) {
  return [x, y];
}, square, doubled);

modded(1, 2);
// => [1, 4]

modded(5, 10);
// => [25, 20]
```

### _.negate(predicate)

Creates a function that negates the result of the predicate `func`. The
`func` predicate is invoked with the `this` binding and arguments of the
created function.

#### Arguments
1. `predicate` *(Function)*: The predicate to negate.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
function isEven(n) {
  return n % 2 == 0;
}

_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

### _.once(func)

Creates a function that is restricted to invoking `func` once. Repeat calls
to the function return the value of the first call. The `func` is invoked
with the `this` binding and arguments of the created function.

#### Arguments
1. `func` *(Function)*: The function to restrict.

#### Returns
*(Function)*:  Returns the new restricted function.

#### Example
```js
var initialize = _.once(createApplication);
initialize();
initialize();
// `initialize` invokes `createApplication` once
```

### _.partial(func, [partials])

Creates a function that invokes `func` with `partial` arguments prepended
to those provided to the new function. This method is like `_.bind` except
it does **not** alter the `this` binding.
<br>
<br>
The `_.partial.placeholder` value, which defaults to `_` in monolithic
builds, may be used as a placeholder for partially applied arguments.
<br>
<br>
**Note:** This method does not set the "length" property of partially
applied functions.

#### Arguments
1. `func` *(Function)*: The function to partially apply arguments to.
2. `[partials]` *(...&#42;)*: The arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new partially applied function.

#### Example
```js
var greet = function(greeting, name) {
  return greeting + ' ' + name;
};

var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'

// using placeholders
var greetFred = _.partial(greet, _, 'fred');
greetFred('hi');
// => 'hi fred'
```

### _.partialRight(func, [partials])

This method is like `_.partial` except that partially applied arguments
are appended to those provided to the new function.
<br>
<br>
The `_.partialRight.placeholder` value, which defaults to `_` in monolithic
builds, may be used as a placeholder for partially applied arguments.
<br>
<br>
**Note:** This method does not set the "length" property of partially
applied functions.

#### Arguments
1. `func` *(Function)*: The function to partially apply arguments to.
2. `[partials]` *(...&#42;)*: The arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new partially applied function.

#### Example
```js
var greet = function(greeting, name) {
  return greeting + ' ' + name;
};

var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'

// using placeholders
var sayHelloTo = _.partialRight(greet, 'hello', _);
sayHelloTo('fred');
// => 'hello fred'
```

### _.rearg(func, indexes)

Creates a function that invokes `func` with arguments arranged according
to the specified indexes where the argument value at the first index is
provided as the first argument, the argument value at the second index is
provided as the second argument, and so on.

#### Arguments
1. `func` *(Function)*: The function to rearrange arguments for.
2. `indexes` *(...(number|number&#91;&#93;)*: The arranged argument indexes, specified as individual indexes or arrays of indexes.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var rearged = _.rearg(function(a, b, c) {
  return [a, b, c];
}, 2, 0, 1);

rearged('b', 'c', 'a')
// => ['a', 'b', 'c']

var map = _.rearg(_.map, [1, 0]);
map(function(n) {
  return n * 3;
}, [1, 2, 3]);
// => [3, 6, 9]
```

### _.restParam(func, [start=func.length-1])

Creates a function that invokes `func` with the `this` binding of the
created function and arguments from `start` and beyond provided as an array.
<br>
<br>
**Note:** This method is based on the [rest parameter](https://developer.mozilla.org/Web/JavaScript/Reference/Functions/rest_parameters).

#### Arguments
1. `func` *(Function)*: The function to apply a rest parameter to.
2. `[start=func.length-1]` *(number)*: The start position of the rest parameter.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var say = _.restParam(function(what, names) {
  return what + ' ' + _.initial(names).join(', ') +
    (_.size(names) > 1 ? ', & ' : '') + _.last(names);
});

say('hello', 'fred', 'barney', 'pebbles');
// => 'hello fred, barney, & pebbles'
```

### _.spread(func)

Creates a function that invokes `func` with the `this` binding of the created
function and an array of arguments much like [`Function#apply`](https://es5.github.io/#x15.3.4.3).
<br>
<br>
**Note:** This method is based on the [spread operator](https://developer.mozilla.org/Web/JavaScript/Reference/Operators/Spread_operator).

#### Arguments
1. `func` *(Function)*: The function to spread arguments over.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var say = _.spread(function(who, what) {
  return who + ' says ' + what;
});

say(['fred', 'hello']);
// => 'fred says hello'

// with a Promise
var numbers = Promise.all([
  Promise.resolve(40),
  Promise.resolve(36)
]);

numbers.then(_.spread(function(x, y) {
  return x + y;
}));
// => a Promise of 76
```

### _.throttle(func, [wait=0], [options])

Creates a throttled function that only invokes `func` at most once per
every `wait` milliseconds. The throttled function comes with a `cancel`
method to cancel delayed invocations. Provide an options object to indicate
that `func` should be invoked on the leading and/or trailing edge of the
`wait` timeout. Subsequent calls to the throttled function return the
result of the last `func` call.
<br>
<br>
**Note:** If `leading` and `trailing` options are `true`, `func` is invoked
on the trailing edge of the timeout only if the the throttled function is
invoked more than once during the `wait` timeout.
<br>
<br>
See [David Corbacho's article](http://drupalmotion.com/article/debounce-and-throttle-visual-explanation)
for details over the differences between `_.throttle` and `_.debounce`.

#### Arguments
1. `func` *(Function)*: The function to throttle.
2. `[wait=0]` *(number)*: The number of milliseconds to throttle invocations to.
3. `[options]` *(Object)*: The options object.
4. `[options.leading=true]` *(boolean)*: Specify invoking on the leading edge of the timeout.
5. `[options.trailing=true]` *(boolean)*: Specify invoking on the trailing edge of the timeout.

#### Returns
*(Function)*:  Returns the new throttled function.

#### Example
```js
// avoid excessively updating the position while scrolling
jQuery(window).on('scroll', _.throttle(updatePosition, 100));

// invoke `renewToken` when the click event is fired, but not more than once every 5 minutes
jQuery('.interactive').on('click', _.throttle(renewToken, 300000, {
  'trailing': false
}));

// cancel a trailing throttled call
jQuery(window).on('popstate', throttled.cancel);
```

### _.wrap(value, wrapper)

Creates a function that provides `value` to the wrapper function as its
first argument. Any additional arguments provided to the function are
appended to those provided to the wrapper function. The wrapper is invoked
with the `this` binding of the created function.

#### Arguments
1. `value` *(&#42;)*: The value to wrap.
2. `wrapper` *(Function)*: The wrapper function.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var p = _.wrap(_.escape, function(func, text) {
  return '<p>' + func(text) + '</p>';
});

p('fred, barney, & pebbles');
// => '<p>fred, barney, &amp; pebbles</p>'
```

