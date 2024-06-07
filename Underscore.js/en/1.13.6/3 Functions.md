[TOC]

### bind

`_.bind(function, object, *arguments)` [source](https://underscorejs.org/docs/modules/bind.html)  

Bind a **function** to an **object**, meaning that whenever the function is called, the value of _this_ will be the **object**. Optionally, pass **arguments** to the **function** to pre-fill them, also known as **partial application**. For partial application without context binding, use [partial](#partial).

```js
var func = function(greeting){ return greeting + ': ' + this.name };
func = _.bind(func, {name: 'moe'}, 'hi');
func();
=> 'hi: moe'
```

### bindAll

`_.bindAll(object, *methodNames)` [source](https://underscorejs.org/docs/modules/bindAll.html)  

Binds a number of methods on the **object**, specified by **methodNames**, to be run in the context of that object whenever they are invoked. Very handy for binding functions that are going to be used as event handlers, which would otherwise be invoked with a fairly useless _this_. **methodNames** are required.

```js
var buttonView = {
label  : 'underscore',
onClick: function(){ alert('clicked: ' + this.label); },
onHover: function(){ console.log('hovering: ' + this.label); }
};
_.bindAll(buttonView, 'onClick', 'onHover');
// When the button is clicked, this.label will have the correct value.
jQuery('#underscore_button').on('click', buttonView.onClick);
```

### partial

`_.partial(function, *arguments)` [source](https://underscorejs.org/docs/modules/partial.html)  

Partially apply a function by filling in any number of its **arguments**, _without_ changing its dynamic this value. A close cousin of [bind](#bind). You may pass \_ in your list of **arguments** to specify an argument that should not be pre-filled, but left open to supply at call-time. _Note: if you need \_ placeholders and a this binding at the same time, use both \_.partial and \_.bind_.

```js
var subtract = function(a, b) { return b - a; };
sub5 = _.partial(subtract, 5);
sub5(20);
=> 15

// Using a placeholder
subFrom20 = _.partial(subtract, _, 20);
subFrom20(5);
=> 15
```

### memoize

`_.memoize(function, [hashFunction])` [source](https://underscorejs.org/docs/modules/memoize.html)  

Memoizes a given **function** by caching the computed result. Useful for speeding up slow-running computations. If passed an optional **hashFunction**, it will be used to compute the hash key for storing the result, based on the arguments to the original function. The default **hashFunction** just uses the first argument to the memoized function as the key. The cache of memoized values is available as the cache property on the returned function.

```js
var fibonacci = _.memoize(function(n) {
return n < 2 ? n: fibonacci(n - 1) + fibonacci(n - 2);
});
```

### delay

`_.delay(function, wait, *arguments)` [source](https://underscorejs.org/docs/modules/delay.html)  

Much like **setTimeout**, invokes **function** after **wait** milliseconds. If you pass the optional **arguments**, they will be forwarded on to the **function** when it is invoked.

```js
var log = _.bind(console.log, console);
_.delay(log, 1000, 'logged later');
=> 'logged later' // Appears after one second.
```

### defer

`_.defer(function, *arguments)` [source](https://underscorejs.org/docs/modules/defer.html)  

Defers invoking the **function** until the current call stack has cleared, similar to using **setTimeout** with a delay of 0. Useful for performing expensive computations or HTML rendering in chunks without blocking the UI thread from updating. If you pass the optional **arguments**, they will be forwarded on to the **function** when it is invoked.

```js
_.defer(function(){ alert('deferred'); });
// Returns from the function before the alert runs.
```

### throttle

`_.throttle(function, wait, [options])` [source](https://underscorejs.org/docs/modules/throttle.html)  

Creates and returns a new, throttled version of the passed function, that, when invoked repeatedly, will only actually call the original function at most once per every **wait** milliseconds. Useful for rate-limiting events that occur faster than you can keep up with.

By default, **throttle** will execute the function as soon as you call it for the first time, and, if you call it again any number of times during the **wait** period, as soon as that period is over. If you'd like to disable the leading-edge call, pass {leading: false}, and if you'd like to disable the execution on the trailing-edge, pass  
`{trailing: false}`.

```js
var throttled = _.throttle(updatePosition, 100);
$(window).scroll(throttled);
```

If you need to cancel a scheduled throttle, you can call .cancel() on the throttled function.

### debounce

`_.debounce(function, wait, [immediate])` [source](https://underscorejs.org/docs/modules/debounce.html)  

Creates and returns a new debounced version of the passed function which will postpone its execution until after **wait** milliseconds have elapsed since the last time it was invoked. Useful for implementing behavior that should only happen _after_ the input has stopped arriving. For example: rendering a preview of a Markdown comment, recalculating a layout after the window has stopped being resized, and so on.

At the end of the **wait** interval, the function will be called with the arguments that were passed _most recently_ to the debounced function.

Pass true for the **immediate** argument to cause **debounce** to trigger the function on the leading instead of the trailing edge of the **wait** interval. Useful in circumstances like preventing accidental double-clicks on a "submit" button from firing a second time.

```js
var lazyLayout = _.debounce(calculateLayout, 300);
$(window).resize(lazyLayout);
```

If you need to cancel a scheduled debounce, you can call .cancel() on the debounced function.

### once

`_.once(function)` [source](https://underscorejs.org/docs/modules/once.html)  

Creates a version of the function that can only be called one time. Repeated calls to the modified function will have no effect, returning the value from the original call. Useful for initialization functions, instead of having to set a boolean flag and then check it later.

```js
var initialize = _.once(createApplication);
initialize();
initialize();
// Application is only created once.
```

### after

`_.after(count, function)` [source](https://underscorejs.org/docs/modules/after.html)  

Creates a wrapper of **function** that does nothing at first. From the **count**\-th call onwards, it starts actually calling **function**. Useful for grouping asynchronous responses, where you want to be sure that all the async calls have finished, before proceeding.

```js
var renderNotes = _.after(notes.length, render);
_.each(notes, function(note) {
note.asyncSave({success: renderNotes});
});
// renderNotes is run once, after all notes have saved.
```

### before

`_.before(count, function)` [source](https://underscorejs.org/docs/modules/before.html)  

Creates a wrapper of **function** that memoizes its return value. From the **count**\-th call onwards, the memoized result of the last invocation is returned immediately instead of invoking **function** again. So the wrapper will invoke **function** at most **count** - 1 times.

```js
var monthlyMeeting = _.before(3, askForRaise);
monthlyMeeting();
monthlyMeeting();
monthlyMeeting();
// the result of any subsequent calls is the same as the second call
```

### wrap

`_.wrap(function, wrapper)` [source](https://underscorejs.org/docs/modules/wrap.html)  

Wraps the first **function** inside of the **wrapper** function, passing it as the first argument. This allows the **wrapper** to execute code before and after the **function** runs, adjust the arguments, and execute it conditionally.

```js
var hello = function(name) { return "hello: " + name; };
hello = _.wrap(hello, function(func) {
return "before, " + func("moe") + ", after";
});
hello();
=> 'before, hello: moe, after'
```

### negate

`_.negate(predicate)` [source](https://underscorejs.org/docs/modules/negate.html)  

Returns a new negated version of the [**predicate**](#iteratee) function.

```js
var isFalsy = _.negate(Boolean);
_.find([-2, -1, 0, 1, 2], isFalsy);
=> 0
```

### compose

`_.compose(*functions)` [source](https://underscorejs.org/docs/modules/compose.html)  

Returns the composition of a list of **functions**, where each function consumes the return value of the function that follows. In math terms, composing the functions _f()_, _g()_, and _h()_ produces _f(g(h()))_.

```js
var greet    = function(name){ return "hi: " + name; };
var exclaim  = function(statement){ return statement.toUpperCase() + "!"; };
var welcome = _.compose(greet, exclaim);
welcome('moe');
=> 'hi: MOE!'
```

### restArguments

`_.restArguments(function, [startIndex])` [source](https://underscorejs.org/docs/modules/restArguments.html)  

Returns a version of the **function** that, when called, receives all arguments from and beyond **startIndex** collected into a single array. If you don’t pass an explicit **startIndex**, it will be determined by looking at the number of arguments to the **function** itself. Similar to ES6’s [rest parameters syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters).

```js
var raceResults = _.restArguments(function(gold, silver, bronze, everyoneElse) {
_.each(everyoneElse, sendConsolations);
});

raceResults("Dopey", "Grumpy", "Happy", "Sneezy", "Bashful", "Sleepy", "Doc");
```
