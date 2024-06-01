[TOC]

### _.constant(value)

Creates a function that returns `value`.

#### Arguments
1. `value` *(&#42;)*: The value to return from the new function.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var object = { 'name': 'fred' };
var getter = _.constant(object);
getter() === object;
// => true
```
* * *

### _.createCallback([func=identity], [thisArg], [argCount])

Produces a callback bound to an optional `thisArg`. If `func` is a property
name the created callback will return the property value for a given element.
If `func` is an object the created callback will return `true` for elements
that contain the equivalent object properties, otherwise it will return `false`.

#### Arguments
1. `[func=identity]` *(&#42;)*: The value to convert to a callback.
2. `[thisArg]` *(&#42;)*: The `this` binding of the created callback.
3. `[argCount]` *(number)*: The number of arguments the callback accepts.

#### Returns
*(Function)*:  Returns a callback function.

#### Example
```js
var characters = [
  { 'name': 'barney', 'age': 36 },
  { 'name': 'fred',   'age': 40 }
];

// wrap to create custom callback shorthands
_.createCallback = _.wrap(_.createCallback, function(func, callback, thisArg) {
  var match = /^(.+?)__([gl]t)(.+)$/.exec(callback);
  return !match ? func(callback, thisArg) : function(object) {
    return match[2] == 'gt' ? object[match[1]] > match[3] : object[match[1]] < match[3];
  };
});

_.filter(characters, 'age__gt38');
// => [{ 'name': 'fred', 'age': 40 }]
```
* * *

### _.escape(string)

Converts the characters `&`, `<`, `>`, `"`, and `'` in `string` to their
corresponding HTML entities.

#### Arguments
1. `string` *(string)*: The string to escape.

#### Returns
*(string)*:  Returns the escaped string.

#### Example
```js
_.escape('Fred, Wilma, & Pebbles');
// => 'Fred, Wilma, &amp; Pebbles'
```
* * *

### _.identity(value)

This method returns the first argument provided to it.

#### Arguments
1. `value` *(&#42;)*: Any value.

#### Returns
*(&#42;)*:  Returns `value`.

#### Example
```js
var object = { 'name': 'fred' };
_.identity(object) === object;
// => true
```
* * *

### _.mixin([object=lodash], source, [options])

Adds function properties of a source object to the destination object.
If `object` is a function methods will be added to its prototype as well.

#### Arguments
1. `[object=lodash]` *(Function|Object)*: object The destination object.
2. `source` *(Object)*: The object of functions to add.
3. `[options]` *(Object)*: The options object.
4. `[options.chain=true]` *(boolean)*: Specify whether the functions added are chainable.

#### Example
```js
function capitalize(string) {
  return string.charAt(0).toUpperCase() + string.slice(1).toLowerCase();
}

_.mixin({ 'capitalize': capitalize });
_.capitalize('fred');
// => 'Fred'

_('fred').capitalize().value();
// => 'Fred'

_.mixin({ 'capitalize': capitalize }, { 'chain': false });
_('fred').capitalize();
// => 'Fred'
```
* * *

### _.noConflict()

Reverts the '_' variable to its previous value and returns a reference to
the `lodash` function.

#### Returns
*(Function)*:  Returns the `lodash` function.

#### Example
```js
var lodash = _.noConflict();
```
* * *

### _.noop()

A no-operation function.

#### Example
```js
var object = { 'name': 'fred' };
_.noop(object) === undefined;
// => true
```
* * *

### _.now

Gets the number of milliseconds that have elapsed since the Unix epoch
(1 January 1970 00:00:00 UTC).

#### Example
```js
var stamp = _.now();
_.defer(function() { console.log(_.now() - stamp); });
// => logs the number of milliseconds it took for the deferred function to be called
```
* * *

### _.parseInt(value, [radix])

Converts the given value into an integer of the specified radix.
If `radix` is `undefined` or `0` a `radix` of `10` is used unless the
`value` is a hexadecimal, in which case a `radix` of `16` is used.
<br>
<br>
Note: This method avoids differences in native ES3 and ES5 `parseInt`
implementations. See http://es5.github.io/#E.

#### Arguments
1. `value` *(string)*: The value to parse.
2. `[radix]` *(number)*: The radix used to interpret the value to parse.

#### Returns
*(number)*:  Returns the new integer value.

#### Example
```js
_.parseInt('08');
// => 8
```
* * *

### _.property(key)

Creates a "_.pluck" style function, which returns the `key` value of a
given object.

#### Arguments
1. `key` *(string)*: The name of the property to retrieve.

#### Returns
*(Function)*:  Returns the new function.

#### Example
```js
var characters = [
  { 'name': 'fred',   'age': 40 },
  { 'name': 'barney', 'age': 36 }
];

var getName = _.property('name');

_.map(characters, getName);
// => ['barney', 'fred']

_.sortBy(characters, getName);
// => [{ 'name': 'barney', 'age': 36 }, { 'name': 'fred',   'age': 40 }]
```
* * *

### _.random([min=0], [max=1], [floating=false])

Produces a random number between `min` and `max` (inclusive). If only one
argument is provided a number between `0` and the given number will be
returned. If `floating` is truey or either `min` or `max` are floats a
floating-point number will be returned instead of an integer.

#### Arguments
1. `[min=0]` *(number)*: The minimum possible value.
2. `[max=1]` *(number)*: The maximum possible value.
3. `[floating=false]` *(boolean)*: Specify returning a floating-point number.

#### Returns
*(number)*:  Returns a random number.

#### Example
```js
_.random(0, 5);
// => an integer between 0 and 5

_.random(5);
// => also an integer between 0 and 5

_.random(5, true);
// => a floating-point number between 0 and 5

_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```
* * *

### _.result(object, key)

Resolves the value of property `key` on `object`. If `key` is a function
it will be invoked with the `this` binding of `object` and its result returned,
else the property value is returned. If `object` is falsey then `undefined`
is returned.

#### Arguments
1. `object` *(Object)*: The object to inspect.
2. `key` *(string)*: The name of the property to resolve.

#### Returns
*(&#42;)*:  Returns the resolved value.

#### Example
```js
var object = {
  'cheese': 'crumpets',
  'stuff': function() {
    return 'nonsense';
  }
};

_.result(object, 'cheese');
// => 'crumpets'

_.result(object, 'stuff');
// => 'nonsense'
```
* * *

### _.runInContext([context=root])

Create a new `lodash` function using the given context object.

#### Arguments
1. `[context=root]` *(Object)*: The context object.

#### Returns
*(Function)*:  Returns the `lodash` function.

* * *

### _.template(text, data, [options], [sourceURL], [variable])

A micro-templating method that handles arbitrary delimiters, preserves
whitespace, and correctly escapes quotes within interpolated code.
<br>
<br>
Note: In the development build, `_.template` utilizes sourceURLs for easier
debugging. See http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl
<br>
<br>
For more information on precompiling templates see:<br>
https://lodash.com/custom-builds
<br>
<br>
For more information on Chrome extension sandboxes see:<br>
http://developer.chrome.com/stable/extensions/sandboxingEval.html

#### Arguments
1. `text` *(string)*: The template text.
2. `data` *(Object)*: The data object used to populate the text.
3. `[options]` *(Object)*: The options object.
4. `[options.escape]` *(RegExp)*: The "escape" delimiter.
5. `[options.evaluate]` *(RegExp)*: The "evaluate" delimiter.
6. `[options.imports]` *(Object)*: An object to import into the template as local variables.
7. `[options.interpolate]` *(RegExp)*: The "interpolate" delimiter.
8. `[sourceURL]` *(string)*: The sourceURL of the template's compiled source.
9. `[variable]` *(string)*: The data object variable name.

#### Returns
*(Function|string)*:  Returns a compiled function when no `data` object
is given, else it returns the interpolated text.

#### Example
```js
// using the "interpolate" delimiter to create a compiled template
var compiled = _.template('hello <%= name %>');
compiled({ 'name': 'fred' });
// => 'hello fred'

// using the "escape" delimiter to escape HTML in data property values
_.template('<b><%- value %></b>', { 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// using the "evaluate" delimiter to generate HTML
var list = '<% _.forEach(people, function(name) { %><li><%- name %></li><% }); %>';
_.template(list, { 'people': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// using the ES6 delimiter as an alternative to the default "interpolate" delimiter
_.template('hello ${ name }', { 'name': 'pebbles' });
// => 'hello pebbles'

// using the internal `print` function in "evaluate" delimiters
_.template('<% print("hello " + name); %>!', { 'name': 'barney' });
// => 'hello barney!'

// using a custom template delimiters
_.templateSettings = {
  'interpolate': /{{([\s\S]+?)}}/g
};

_.template('hello {{ name }}!', { 'name': 'mustache' });
// => 'hello mustache!'

// using the `imports` option to import jQuery
var list = '<% jq.each(people, function(name) { %><li><%- name %></li><% }); %>';
_.template(list, { 'people': ['fred', 'barney'] }, { 'imports': { 'jq': jQuery } });
// => '<li>fred</li><li>barney</li>'

// using the `sourceURL` option to specify a custom sourceURL for the template
var compiled = _.template('hello <%= name %>', null, { 'sourceURL': '/basic/greeting.jst' });
compiled(data);
// => find the source of "greeting.jst" under the Sources tab or Resources panel of the web inspector

// using the `variable` option to ensure a with-statement isn't used in the compiled template
var compiled = _.template('hi <%= data.name %>!', null, { 'variable': 'data' });
compiled.source;
// => function(data) {
  var __t, __p = '', __e = _.escape;
  __p += 'hi ' + ((__t = ( data.name )) == null ? '' : __t) + '!';
  return __p;
}

// using the `source` property to inline compiled templates for meaningful
// line numbers in error messages and a stack trace
fs.writeFileSync(path.join(cwd, 'jst.js'), '\
  var JST = {\
    "main": ' + _.template(mainText).source + '\
  };\
');
```
* * *

### _.times(n, callback, [thisArg])

Executes the callback `n` times, returning an array of the results
of each callback execution. The callback is bound to `thisArg` and invoked
with one argument; (index).

#### Arguments
1. `n` *(number)*: The number of times to execute the callback.
2. `callback` *(Function)*: The function called per iteration.
3. `[thisArg]` *(&#42;)*: The `this` binding of `callback`.

#### Returns
*(Array)*:  Returns an array of the results of each `callback` execution.

#### Example
```js
var diceRolls = _.times(3, _.partial(_.random, 1, 6));
// => [3, 6, 4]

_.times(3, function(n) { mage.castSpell(n); });
// => calls `mage.castSpell(n)` three times, passing `n` of `0`, `1`, and `2` respectively

_.times(3, function(n) { this.cast(n); }, mage);
// => also calls `mage.castSpell(n)` three times
```
* * *

### _.unescape(string)

The inverse of `_.escape` this method converts the HTML entities
`&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&#39;` in `string` to their
corresponding characters.

#### Arguments
1. `string` *(string)*: The string to unescape.

#### Returns
*(string)*:  Returns the unescaped string.

#### Example
```js
_.unescape('Fred, Barney &amp; Pebbles');
// => 'Fred, Barney & Pebbles'
```
* * *

### _.uniqueId([prefix])

Generates a unique ID. If `prefix` is provided the ID will be appended to it.

#### Arguments
1. `[prefix]` *(string)*: The value to prefix the ID with.

#### Returns
*(string)*:  Returns the unique ID.

#### Example
```js
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```
* * *
