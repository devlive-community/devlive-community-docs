[TOC]

### _.escape(string)

Converts the characters `&`, `<`, `>`, `"`, and `'` in `string` to their corresponding HTML entities.

#### Arguments

1. `string` *(String)*: The string to escape.

#### Returns

*(String)*: Returns the escaped string.

#### Example

```js
_.escape('Moe, Larry & Curly');
// => 'Moe, Larry &amp; Curly'
```

* * *

### _.identity(value)

This method returns the first argument passed to it.

#### Arguments

1. `value` *(Mixed)*: Any value.

#### Returns

*(Mixed)*: Returns `value`.

#### Example

```js
var moe = { 'name': 'moe' };
moe === _.identity(moe);
// => true
```

* * *

### _.mixin(object)

Adds functions properties of `object` to the `lodash` function and chainable wrapper.

#### Arguments

1. `object` *(Object)*: The object of function properties to add to `lodash`.

#### Example

```js
_.mixin({
  'capitalize': function(string) {
    return string.charAt(0).toUpperCase() + string.slice(1).toLowerCase();
  }
});

_.capitalize('moe');
// => 'Moe'

_('moe').capitalize();
// => 'Moe'
```

* * *

### _.noConflict()

Reverts the '_' variable to its previous value and returns a reference to the `lodash` function.

#### Returns

*(Function)*: Returns the `lodash` function.

#### Example

```js
var lodash = _.noConflict();
```

* * *

### _.parseInt(value [, radix])

Converts the given `value` into an integer of the specified `radix`. If `radix` is `undefined` or `0`, a `radix` of `10` is used unless the `value` is a hexadecimal, in which case a `radix` of `16` is used.

Note: This method avoids differences in native ES3 and ES5 `parseInt` implementations. See http://es5.github.com/#E.

#### Arguments

1. `value` *(String)*: The value to parse.
2. `[radix]` *(Number)*: The radix used to interpret the value to parse.

#### Returns

*(Number)*: Returns the new integer value.

#### Example

```js
_.parseInt('08');
// => 8
```

* * *

### _.random([min=0, max=1])

Produces a random number between `min` and `max` *(inclusive)*. If only one argument is passed, a number between `0` and the given number will be returned.

#### Arguments

1. `[min=0]` *(Number)*: The minimum possible value.
2. `[max=1]` *(Number)*: The maximum possible value.

#### Returns

*(Number)*: Returns a random number.

#### Example

```js
_.random(0, 5);
// => a number between 0 and 5

_.random(5);
// => also a number between 0 and 5
```

* * *

### _.result(object, property)

Resolves the value of `property` on `object`. If `property` is a function, it will be invoked with the `this` binding of `object` and its result returned, else the property value is returned. If `object` is falsey, then `undefined` is returned.

#### Arguments

1. `object` *(Object)*: The object to inspect.
2. `property` *(String)*: The property to get the value of.

#### Returns

*(Mixed)*: Returns the resolved value.

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

### _.runInContext([context=window])

Create a new `lodash` function using the given `context` object.

#### Arguments

1. `[context=window]` *(Object)*: The context object.

#### Returns

*(Function)*: Returns the `lodash` function.

* * *

### _.template(text, data, options)

A micro-templating method that handles arbitrary delimiters, preserves whitespace, and correctly escapes quotes within interpolated code.

Note: In the development build, `_.template` utilizes sourceURLs for easier debugging. See http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl

For more information on precompiling templates see:<br>
http://lodash.com/#custom-builds

For more information on Chrome extension sandboxes see:<br>
http://developer.chrome.com/stable/extensions/sandboxingEval.html

#### Arguments

1. `text` *(String)*: The template text.
2. `data` *(Object)*: The data object used to populate the text.
3. `options` *(Object)*: The options object. escape - The "escape" delimiter regexp. evaluate - The "evaluate" delimiter regexp. interpolate - The "interpolate" delimiter regexp. sourceURL - The sourceURL of the template's compiled source. variable - The data object variable name.

#### Returns

*(Function, String)*: Returns a compiled function when no `data` object  is given, else it returns the interpolated text.

#### Example

```js
// using a compiled template
var compiled = _.template('hello <%= name %>');
compiled({ 'name': 'moe' });
// => 'hello moe'

var list = '<% _.forEach(people, function(name) { %><li><%= name %></li><% }); %>';
_.template(list, { 'people': ['moe', 'larry'] });
// => '<li>moe</li><li>larry</li>'

// using the "escape" delimiter to escape HTML in data property values
_.template('<b><%- value %></b>', { 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// using the ES6 delimiter as an alternative to the default "interpolate" delimiter
_.template('hello ${ name }', { 'name': 'curly' });
// => 'hello curly'

// using the internal `print` function in "evaluate" delimiters
_.template('<% print("hello " + epithet); %>!', { 'epithet': 'stooge' });
// => 'hello stooge!'

// using custom template delimiters
_.templateSettings = {
  'interpolate': /{{([\s\S]+?)}}/g
};

_.template('hello {{ name }}!', { 'name': 'mustache' });
// => 'hello mustache!'

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

### _.times(n, callback [, thisArg])

Executes the `callback` function `n` times, returning an array of the results of each `callback` execution. The `callback` is bound to `thisArg` and invoked with one argument; *(index)*.

#### Arguments

1. `n` *(Number)*: The number of times to execute the callback.
2. `callback` *(Function)*: The function called per iteration.
3. `[thisArg]` *(Mixed)*: The `this` binding of `callback`.

#### Returns

*(Array)*: Returns a new array of the results of each `callback` execution.

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

The inverse of `_.escape`, this method converts the HTML entities `&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&#39;` in `string` to their corresponding characters.

#### Arguments

1. `string` *(String)*: The string to unescape.

#### Returns

*(String)*: Returns the unescaped string.

#### Example

```js
_.unescape('Moe, Larry &amp; Curly');
// => 'Moe, Larry & Curly'
```

* * *

### _.uniqueId([prefix])

Generates a unique ID. If `prefix` is passed, the ID will be appended to it.

#### Arguments

1. `[prefix]` *(String)*: The value to prefix the ID with.

#### Returns

*(String)*: Returns the unique ID.

#### Example

```js
_.uniqueId('contact_');
// => 'contact_104'

_.uniqueId();
// => '105'
```

* * *
