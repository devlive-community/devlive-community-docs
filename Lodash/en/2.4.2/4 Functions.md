[TOC]

### _.after(n, func)

Creates a function that executes `func`, with  the `this` binding and
arguments of the created function, only after being called `n` times.

#### Arguments
1. `n` *(number)*: The number of times the function must be called before `func` is executed.
2. `func` *(Function)*: The function to restrict.

#### Returns
*(Function)*:  Returns the new restricted function.

#### Example
```js
var saves = ['profile', 'settings'];

var done = _.after(saves.length, function() {
  console.log('Done saving!');
});

_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => logs 'Done saving!', after all saves have completed
```
* * *

### _.bind(func, [thisArg], [arg])

Creates a function that, when called, invokes `func` with the `this`
binding of `thisArg` and prepends any additional `bind` arguments to those
provided to the bound function.

#### Arguments
1. `func` *(Function)*: The function to bind.
2. `[thisArg]` *(&#42;)*: The `this` binding of `func`.
3. `[arg]` *(...&#42;)*: Arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new bound function.

#### Example
```js
var func = function(greeting) {
  return greeting + ' ' + this.name;
};

func = _.bind(func, { 'name': 'fred' }, 'hi');
func();
// => 'hi fred'
```
* * *

### _.bindAll(object, [methodName])

Binds methods of an object to the object itself, overwriting the existing
method. Method names may be specified as individual arguments or as arrays
of method names. If no method names are provided all the function properties
of `object` will be bound.

#### Arguments
1. `object` *(Object)*: The object to bind and assign the bound methods to.
2. `[methodName]` *(...string)*: The object method names to bind, specified as individual method names or arrays of method names.

#### Returns
*(Object)*:  Returns `object`.

#### Example
```js
var view = {
  'label': 'docs',
  'onClick': function() { console.log('clicked ' + this.label); }
};

_.bindAll(view);
jQuery('#docs').on('click', view.onClick);
// => logs 'clicked docs', when the button is clicked
```
* * *

### _.bindKey(object, key, [arg])

Creates a function that, when called, invokes the method at `object[key]`
and prepends any additional `bindKey` arguments to those provided to the bound
function. This method differs from `_.bind` by allowing bound functions to
reference methods that will be redefined or don't yet exist.
See http://michaux.ca/articles/lazy-function-definition-pattern.

#### Arguments
1. `object` *(Object)*: The object the method belongs to.
2. `key` *(string)*: The key of the method.
3. `[arg]` *(...&#42;)*: Arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new bound function.

#### Example
```js
var object = {
  'name': 'fred',
  'greet': function(greeting) {
    return greeting + ' ' + this.name;
  }
};

var func = _.bindKey(object, 'greet', 'hi');
func();
// => 'hi fred'

object.greet = function(greeting) {
  return greeting + 'ya ' + this.name + '!';
};

func();
// => 'hiya fred!'
```
* * *

### _.compose([func])

Creates a function that is the composition of the provided functions,
where each function consumes the return value of the function that follows.
For example, composing the functions `f()`, `g()`, and `h()` produces `f(g(h()))`.
Each function is executed with the `this` binding of the composed function.

#### Arguments
1. `[func]` *(...Function)*: Functions to compose.

#### Returns
*(Function)*:  Returns the new composed function.

#### Example
```js
var realNameMap = {
  'pebbles': 'penelope'
};

var format = function(name) {
  name = realNameMap[name.toLowerCase()] || name;
  return name.charAt(0).toUpperCase() + name.slice(1).toLowerCase();
};

var greet = function(formatted) {
  return 'Hiya ' + formatted + '!';
};

var welcome = _.compose(greet, format);
welcome('pebbles');
// => 'Hiya Penelope!'
```
* * *

### _.curry(func, [arity=func.length])

Creates a function which accepts one or more arguments of `func` that when
invoked either executes `func` returning its result, if all `func` arguments
have been provided, or returns a function that accepts one or more of the
remaining `func` arguments, and so on. The arity of `func` can be specified
if `func.length` is not sufficient.

#### Arguments
1. `func` *(Function)*: The function to curry.
2. `[arity=func.length]` *(number)*: The arity of `func`.

#### Returns
*(Function)*:  Returns the new curried function.

#### Example
```js
var curried = _.curry(function(a, b, c) {
  console.log(a + b + c);
});

curried(1)(2)(3);
// => 6

curried(1, 2)(3);
// => 6

curried(1, 2, 3);
// => 6
```
* * *

### _.debounce(func, wait, [options])

Creates a function that will delay the execution of `func` until after
`wait` milliseconds have elapsed since the last time it was invoked.
Provide an options object to indicate that `func` should be invoked on
the leading and/or trailing edge of the `wait` timeout. Subsequent calls
to the debounced function will return the result of the last `func` call.
<br>
<br>
Note: If `leading` and `trailing` options are `true` `func` will be called
on the trailing edge of the timeout only if the the debounced function is
invoked more than once during the `wait` timeout.

#### Arguments
1. `func` *(Function)*: The function to debounce.
2. `wait` *(number)*: The number of milliseconds to delay.
3. `[options]` *(Object)*: The options object.
4. `[options.leading=false]` *(boolean)*: Specify execution on the leading edge of the timeout.
5. `[options.maxWait]` *(number)*: The maximum time `func` is allowed to be delayed before it's called.
6. `[options.trailing=true]` *(boolean)*: Specify execution on the trailing edge of the timeout.

#### Returns
*(Function)*:  Returns the new debounced function.

#### Example
```js
// avoid costly calculations while the window size is in flux
var lazyLayout = _.debounce(calculateLayout, 150);
jQuery(window).on('resize', lazyLayout);

// execute `sendMail` when the click event is fired, debouncing subsequent calls
jQuery('#postbox').on('click', _.debounce(sendMail, 300, {
  'leading': true,
  'trailing': false
});

// ensure `batchLog` is executed once after 1 second of debounced calls
var source = new EventSource('/stream');
source.addEventListener('message', _.debounce(batchLog, 250, {
  'maxWait': 1000
}, false);
```
* * *

### _.defer(func, [arg])

Defers executing the `func` function until the current call stack has cleared.
Additional arguments will be provided to `func` when it is invoked.

#### Arguments
1. `func` *(Function)*: The function to defer.
2. `[arg]` *(...&#42;)*: Arguments to invoke the function with.

#### Returns
*(number)*:  Returns the timer id.

#### Example
```js
_.defer(function(text) { console.log(text); }, 'deferred');
// logs 'deferred' after one or more milliseconds
```
* * *

### _.delay(func, wait, [arg])

Executes the `func` function after `wait` milliseconds. Additional arguments
will be provided to `func` when it is invoked.

#### Arguments
1. `func` *(Function)*: The function to delay.
2. `wait` *(number)*: The number of milliseconds to delay execution.
3. `[arg]` *(...&#42;)*: Arguments to invoke the function with.

#### Returns
*(number)*:  Returns the timer id.

#### Example
```js
_.delay(function(text) { console.log(text); }, 1000, 'later');
// => logs 'later' after one second
```
* * *

### _.memoize(func, [resolver])

Creates a function that memoizes the result of `func`. If `resolver` is
provided it will be used to determine the cache key for storing the result
based on the arguments provided to the memoized function. By default, the
first argument provided to the memoized function is used as the cache key.
The `func` is executed with the `this` binding of the memoized function.
The result cache is exposed as the `cache` property on the memoized function.

#### Arguments
1. `func` *(Function)*: The function to have its output memoized.
2. `[resolver]` *(Function)*: A function used to resolve the cache key.

#### Returns
*(Function)*:  Returns the new memoizing function.

#### Example
```js
var fibonacci = _.memoize(function(n) {
  return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
});

fibonacci(9)
// => 34

var data = {
  'fred': { 'name': 'fred', 'age': 40 },
  'pebbles': { 'name': 'pebbles', 'age': 1 }
};

// modifying the result cache
var get = _.memoize(function(name) { return data[name]; }, _.identity);
get('pebbles');
// => { 'name': 'pebbles', 'age': 1 }

get.cache.pebbles.name = 'penelope';
get('pebbles');
// => { 'name': 'penelope', 'age': 1 }
```
* * *

### _.once(func)

Creates a function that is restricted to execute `func` once. Repeat calls to
the function will return the value of the first call. The `func` is executed
with the `this` binding of the created function.

#### Arguments
1. `func` *(Function)*: The function to restrict.

#### Returns
*(Function)*:  Returns the new restricted function.

#### Example
```js
var initialize = _.once(createApplication);
initialize();
initialize();
// `initialize` executes `createApplication` once
```
* * *

### _.partial(func, [arg])

Creates a function that, when called, invokes `func` with any additional
`partial` arguments prepended to those provided to the new function. This
method is similar to `_.bind` except it does **not** alter the `this` binding.

#### Arguments
1. `func` *(Function)*: The function to partially apply arguments to.
2. `[arg]` *(...&#42;)*: Arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new partially applied function.

#### Example
```js
var greet = function(greeting, name) { return greeting + ' ' + name; };
var hi = _.partial(greet, 'hi');
hi('fred');
// => 'hi fred'
```
* * *

### _.partialRight(func, [arg])

This method is like `_.partial` except that `partial` arguments are
appended to those provided to the new function.

#### Arguments
1. `func` *(Function)*: The function to partially apply arguments to.
2. `[arg]` *(...&#42;)*: Arguments to be partially applied.

#### Returns
*(Function)*:  Returns the new partially applied function.

#### Example
```js
var defaultsDeep = _.partialRight(_.merge, _.defaults);

var options = {
  'variable': 'data',
  'imports': { 'jq': $ }
};

defaultsDeep(options, _.templateSettings);

options.variable
// => 'data'

options.imports
// => { '_': _, 'jq': $ }
```
* * *

### _.throttle(func, wait, [options])

Creates a function that, when executed, will only call the `func` function
at most once per every `wait` milliseconds. Provide an options object to
indicate that `func` should be invoked on the leading and/or trailing edge
of the `wait` timeout. Subsequent calls to the throttled function will
return the result of the last `func` call.
<br>
<br>
Note: If `leading` and `trailing` options are `true` `func` will be called
on the trailing edge of the timeout only if the the throttled function is
invoked more than once during the `wait` timeout.

#### Arguments
1. `func` *(Function)*: The function to throttle.
2. `wait` *(number)*: The number of milliseconds to throttle executions to.
3. `[options]` *(Object)*: The options object.
4. `[options.leading=true]` *(boolean)*: Specify execution on the leading edge of the timeout.
5. `[options.trailing=true]` *(boolean)*: Specify execution on the trailing edge of the timeout.

#### Returns
*(Function)*:  Returns the new throttled function.

#### Example
```js
// avoid excessively updating the position while scrolling
var throttled = _.throttle(updatePosition, 100);
jQuery(window).on('scroll', throttled);

// execute `renewToken` when the click event is fired, but not more than once every 5 minutes
jQuery('.interactive').on('click', _.throttle(renewToken, 300000, {
  'trailing': false
}));
```
* * *

### _.wrap(value, wrapper)

Creates a function that provides `value` to the wrapper function as its
first argument. Additional arguments provided to the function are appended
to those provided to the wrapper function. The wrapper is executed with
the `this` binding of the created function.

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

p('Fred, Wilma, & Pebbles');
// => '<p>Fred, Wilma, &amp; Pebbles</p>'
```
* * *
