[TOC]

### _.after(n, func)

If `n` is greater than `0`, a function is created that is restricted to executing `func`, with the `this` binding and arguments of the created function, only after it is called `n` times. If `n` is less than `1`, `func` is executed immediately, without a `this` binding or additional arguments, and its result is returned.

#### Arguments

1. `n` *(Number)*: The number of times the function must be called before it is executed.
2. `func` *(Function)*: The function to restrict.

#### Returns

*(Function)*: Returns the new restricted function.

#### Example

```js
var renderNotes = _.after(notes.length, render);
_.forEach(notes, function(note) {
  note.asyncSave({ 'success': renderNotes });
});
// `renderNotes` is run once, after all notes have saved
```

* * *

### _.bind(func [, thisArg, arg1, arg2, ...])

Creates a function that, when called, invokes `func` with the `this` binding of `thisArg` and prepends any additional `bind` arguments to those passed to the bound function.

#### Arguments

1. `func` *(Function)*: The function to bind.
2. `[thisArg]` *(Mixed)*: The `this` binding of `func`.
3. `[arg1, arg2, ...]` *(Mixed)*: Arguments to be partially applied.

#### Returns

*(Function)*: Returns the new bound function.

#### Example

```js
var func = function(greeting) {
  return greeting + ' ' + this.name;
};

func = _.bind(func, { 'name': 'moe' }, 'hi');
func();
// => 'hi moe'
```

* * *

### _.bindAll(object [, methodName1, methodName2, ...])

Binds methods on `object` to `object`, overwriting the existing method. Method names may be specified as individual arguments or as arrays of method names. If no method names are provided, all the function properties of `object` will be bound.

#### Arguments

1. `object` *(Object)*: The object to bind and assign the bound methods to.
2. `[methodName1, methodName2, ...]` *(String)*: Method names on the object to bind.

#### Returns

*(Object)*: Returns `object`.

#### Example

```js
var view = {
 'label': 'docs',
 'onClick': function() { alert('clicked ' + this.label); }
};

_.bindAll(view);
jQuery('#docs').on('click', view.onClick);
// => alerts 'clicked docs', when the button is clicked
```

* * *

### _.bindKey(object, key [, arg1, arg2, ...])

Creates a function that, when called, invokes the method at `object[key]` and prepends any additional `bindKey` arguments to those passed to the bound function. This method differs from `_.bind` by allowing bound functions to reference methods that will be redefined or don't yet exist. See http://michaux.ca/articles/lazy-function-definition-pattern.

#### Arguments

1. `object` *(Object)*: The object the method belongs to.
2. `key` *(String)*: The key of the method.
3. `[arg1, arg2, ...]` *(Mixed)*: Arguments to be partially applied.

#### Returns

*(Function)*: Returns the new bound function.

#### Example

```js
var object = {
  'name': 'moe',
  'greet': function(greeting) {
    return greeting + ' ' + this.name;
  }
};

var func = _.bindKey(object, 'greet', 'hi');
func();
// => 'hi moe'

object.greet = function(greeting) {
  return greeting + ', ' + this.name + '!';
};

func();
// => 'hi, moe!'
```

* * *

### _.compose([func1, func2, ...])

Creates a function that is the composition of the passed functions, where each function consumes the return value of the function that follows. For example, composing the functions `f()`, `g()`, and `h()` produces `f(g(h()))`. Each function is executed with the `this` binding of the composed function.

#### Arguments

1. `[func1, func2, ...]` *(Function)*: Functions to compose.

#### Returns

*(Function)*: Returns the new composed function.

#### Example

```js
var greet = function(name) { return 'hi ' + name; };
var exclaim = function(statement) { return statement + '!'; };
var welcome = _.compose(exclaim, greet);
welcome('moe');
// => 'hi moe!'
```

* * *

### _.createCallback([func=identity, thisArg, argCount=3])

Produces a callback bound to an optional `thisArg`. If `func` is a property name, the created callback will return the property value for a given element. If `func` is an object, the created callback will return `true` for elements that contain the equivalent object properties, otherwise it will return `false`.

Note: All Lo-Dash methods, that accept a `callback` argument, use `_.createCallback`.

#### Arguments

1. `[func=identity]` *(Mixed)*: The value to convert to a callback.
2. `[thisArg]` *(Mixed)*: The `this` binding of the created callback.
3. `[argCount=3]` *(Number)*: The number of arguments the callback accepts.

#### Returns

*(Function)*: Returns a callback function.

#### Example

```js
var stooges = [
  { 'name': 'moe', 'age': 40 },
  { 'name': 'larry', 'age': 50 }
];

// wrap to create custom callback shorthands
_.createCallback = _.wrap(_.createCallback, function(func, callback, thisArg) {
  var match = /^(.+?)__([gl]t)(.+)$/.exec(callback);
  return !match ? func(callback, thisArg) : function(object) {
    return match[2] == 'gt' ? object[match[1]] > match[3] : object[match[1]] < match[3];
  };
});

_.filter(stooges, 'age__gt45');
// => [{ 'name': 'larry', 'age': 50 }]

// create mixins with support for "_.pluck" and "_.where" callback shorthands
_.mixin({
  'toLookup': function(collection, callback, thisArg) {
    callback = _.createCallback(callback, thisArg);
    return _.reduce(collection, function(result, value, index, collection) {
      return (result[callback(value, index, collection)] = value, result);
    }, {});
  }
});

_.toLookup(stooges, 'name');
// => { 'moe': { 'name': 'moe', 'age': 40 }, 'larry': { 'name': 'larry', 'age': 50 } }
```

* * *

### _.debounce(func, wait, options)

Creates a function that will delay the execution of `func` until after `wait` milliseconds have elapsed since the last time it was invoked. Pass an `options` object to indicate that `func` should be invoked on the leading and/or trailing edge of the `wait` timeout. Subsequent calls to the debounced function will return the result of the last `func` call.

Note: If `leading` and `trailing` options are `true`, `func` will be called on the trailing edge of the timeout only if the the debounced function is invoked more than once during the `wait` timeout.

#### Arguments

1. `func` *(Function)*: The function to debounce.
2. `wait` *(Number)*: The number of milliseconds to delay.
3. `options` *(Object)*: The options object. [leading=false] A boolean to specify execution on the leading edge of the timeout. [maxWait] The maximum time `func` is allowed to be delayed before it's called. [trailing=true] A boolean to specify execution on the trailing edge of the timeout.

#### Returns

*(Function)*: Returns the new debounced function.

#### Example

```js
var lazyLayout = _.debounce(calculateLayout, 300);
jQuery(window).on('resize', lazyLayout);

jQuery('#postbox').on('click', _.debounce(sendMail, 200, {
  'leading': true,
  'trailing': false
});
```

* * *

### _.defer(func [, arg1, arg2, ...])

Defers executing the `func` function until the current call stack has cleared. Additional arguments will be passed to `func` when it is invoked.

#### Arguments

1. `func` *(Function)*: The function to defer.
2. `[arg1, arg2, ...]` *(Mixed)*: Arguments to invoke the function with.

#### Returns

*(Number)*: Returns the timer id.

#### Example

```js
_.defer(function() { alert('deferred'); });
// returns from the function before `alert` is called
```

* * *

### _.delay(func, wait [, arg1, arg2, ...])

Executes the `func` function after `wait` milliseconds. Additional arguments will be passed to `func` when it is invoked.

#### Arguments

1. `func` *(Function)*: The function to delay.
2. `wait` *(Number)*: The number of milliseconds to delay execution.
3. `[arg1, arg2, ...]` *(Mixed)*: Arguments to invoke the function with.

#### Returns

*(Number)*: Returns the timer id.

#### Example

```js
var log = _.bind(console.log, console);
_.delay(log, 1000, 'logged later');
// => 'logged later' (Appears after one second.)
```

* * *

### _.memoize(func [, resolver])

Creates a function that memoizes the result of `func`. If `resolver` is passed, it will be used to determine the cache key for storing the result based on the arguments passed to the memoized function. By default, the first argument passed to the memoized function is used as the cache key. The `func` is executed with the `this` binding of the memoized function. The result cache is exposed as the `cache` property on the memoized function.

#### Arguments

1. `func` *(Function)*: The function to have its output memoized.
2. `[resolver]` *(Function)*: A function used to resolve the cache key.

#### Returns

*(Function)*: Returns the new memoizing function.

#### Example

```js
var fibonacci = _.memoize(function(n) {
  return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
});
```

* * *

### _.once(func)

Creates a function that is restricted to execute `func` once. Repeat calls to the function will return the value of the first call. The `func` is executed with the `this` binding of the created function.

#### Arguments

1. `func` *(Function)*: The function to restrict.

#### Returns

*(Function)*: Returns the new restricted function.

#### Example

```js
var initialize = _.once(createApplication);
initialize();
initialize();
// `initialize` executes `createApplication` once
```

* * *

### _.partial(func [, arg1, arg2, ...])

Creates a function that, when called, invokes `func` with any additional `partial` arguments prepended to those passed to the new function. This method is similar to `_.bind`, except it does **not** alter the `this` binding.

#### Arguments

1. `func` *(Function)*: The function to partially apply arguments to.
2. `[arg1, arg2, ...]` *(Mixed)*: Arguments to be partially applied.

#### Returns

*(Function)*: Returns the new partially applied function.

#### Example

```js
var greet = function(greeting, name) { return greeting + ' ' + name; };
var hi = _.partial(greet, 'hi');
hi('moe');
// => 'hi moe'
```

* * *

### _.partialRight(func [, arg1, arg2, ...])

This method is similar to `_.partial`, except that `partial` arguments are appended to those passed to the new function.

#### Arguments

1. `func` *(Function)*: The function to partially apply arguments to.
2. `[arg1, arg2, ...]` *(Mixed)*: Arguments to be partially applied.

#### Returns

*(Function)*: Returns the new partially applied function.

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

### _.throttle(func, wait, options)

Creates a function that, when executed, will only call the `func` function at most once per every `wait` milliseconds. Pass an `options` object to indicate that `func` should be invoked on the leading and/or trailing edge of the `wait` timeout. Subsequent calls to the throttled function will return the result of the last `func` call.

Note: If `leading` and `trailing` options are `true`, `func` will be called on the trailing edge of the timeout only if the the throttled function is invoked more than once during the `wait` timeout.

#### Arguments

1. `func` *(Function)*: The function to throttle.
2. `wait` *(Number)*: The number of milliseconds to throttle executions to.
3. `options` *(Object)*: The options object. [leading=true] A boolean to specify execution on the leading edge of the timeout. [trailing=true] A boolean to specify execution on the trailing edge of the timeout.

#### Returns

*(Function)*: Returns the new throttled function.

#### Example

```js
var throttled = _.throttle(updatePosition, 100);
jQuery(window).on('scroll', throttled);

jQuery('.interactive').on('click', _.throttle(renewToken, 300000, {
  'trailing': false
}));
```

* * *

### _.wrap(value, wrapper)

Creates a function that passes `value` to the `wrapper` function as its first argument. Additional arguments passed to the function are appended to those passed to the `wrapper` function. The `wrapper` is executed with the `this` binding of the created function.

#### Arguments

1. `value` *(Mixed)*: The value to wrap.
2. `wrapper` *(Function)*: The wrapper function.

#### Returns

*(Function)*: Returns the new function.

#### Example

```js
var hello = function(name) { return 'hello ' + name; };
hello = _.wrap(hello, function(func) {
  return 'before, ' + func('moe') + ', after';
});
hello();
// => 'before, hello moe, after'
```
