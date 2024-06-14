[TOC]

### _.camelCase([string=''])

Converts `string` to [camel case](https://en.wikipedia.org/wiki/CamelCase).

#### Arguments
1. `[string='']` *(string)*: The string to convert.

#### Returns
*(string)*:  Returns the camel cased string.

#### Example
```js
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar');
// => 'fooBar'

_.camelCase('__foo_bar__');
// => 'fooBar'
```

### _.capitalize([string=''])

Capitalizes the first character of `string`.

#### Arguments
1. `[string='']` *(string)*: The string to capitalize.

#### Returns
*(string)*:  Returns the capitalized string.

#### Example
```js
_.capitalize('fred');
// => 'Fred'
```

### _.deburr([string=''])

Deburrs `string` by converting [latin-1 supplementary letters](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table)
to basic latin letters and removing [combining diacritical marks](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks).

#### Arguments
1. `[string='']` *(string)*: The string to deburr.

#### Returns
*(string)*:  Returns the deburred string.

#### Example
```js
_.deburr('déjà vu');
// => 'deja vu'
```

### _.endsWith([string=''], [target], [position=string.length])

Checks if `string` ends with the given target string.

#### Arguments
1. `[string='']` *(string)*: The string to search.
2. `[target]` *(string)*: The string to search for.
3. `[position=string.length]` *(number)*: The position to search from.

#### Returns
*(boolean)*:  Returns `true` if `string` ends with `target`, else `false`.

#### Example
```js
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

### _.escape([string=''])

Converts the characters "&", "<", ">", '"', "'", and "\`", in `string` to
their corresponding HTML entities.
<br>
<br>
**Note:** No other characters are escaped. To escape additional characters
use a third-party library like [_he_](https://mths.be/he).
<br>
<br>
Though the ">" character is escaped for symmetry, characters like
">" and "/" don't need escaping in HTML and have no special meaning
unless they're part of a tag or unquoted attribute value.
See [Mathias Bynens's article](https://mathiasbynens.be/notes/ambiguous-ampersands)
(under "semi-related fun fact") for more details.
<br>
<br>
Backticks are escaped because in Internet Explorer < 9, they can break out
of attribute values or HTML comments. See [#59](https://html5sec.org/#59),
[#102](https://html5sec.org/#102), [#108](https://html5sec.org/#108), and
[#133](https://html5sec.org/#133) of the [HTML5 Security Cheatsheet](https://html5sec.org/)
for more details.
<br>
<br>
When working with HTML you should always [quote attribute values](http://wonko.com/post/html-escaping)
to reduce XSS vectors.

#### Arguments
1. `[string='']` *(string)*: The string to escape.

#### Returns
*(string)*:  Returns the escaped string.

#### Example
```js
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

### _.escapeRegExp([string=''])

Escapes the `RegExp` special characters "\", "/", "^", "$", ".", "|", "?",
"*", "+", "(", ")", "[", "]", "{" and "}" in `string`.

#### Arguments
1. `[string='']` *(string)*: The string to escape.

#### Returns
*(string)*:  Returns the escaped string.

#### Example
```js
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https:\/\/lodash\.com\/\)'
```

### _.kebabCase([string=''])

Converts `string` to [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

#### Arguments
1. `[string='']` *(string)*: The string to convert.

#### Returns
*(string)*:  Returns the kebab cased string.

#### Example
```js
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__foo_bar__');
// => 'foo-bar'
```

### _.pad([string=''], [length=0], [chars=' '])

Pads `string` on the left and right sides if it's shorter than `length`.
Padding characters are truncated if they can't be evenly divided by `length`.

#### Arguments
1. `[string='']` *(string)*: The string to pad.
2. `[length=0]` *(number)*: The padding length.
3. `[chars=' ']` *(string)*: The string used as padding.

#### Returns
*(string)*:  Returns the padded string.

#### Example
```js
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

### _.padLeft([string=''], [length=0], [chars=' '])

Pads `string` on the left side if it's shorter than `length`. Padding
characters are truncated if they exceed `length`.

#### Arguments
1. `[string='']` *(string)*: The string to pad.
2. `[length=0]` *(number)*: The padding length.
3. `[chars=' ']` *(string)*: The string used as padding.

#### Returns
*(string)*:  Returns the padded string.

#### Example
```js
_.padLeft('abc', 6);
// => '   abc'

_.padLeft('abc', 6, '_-');
// => '_-_abc'

_.padLeft('abc', 3);
// => 'abc'
```

### _.padRight([string=''], [length=0], [chars=' '])

Pads `string` on the right side if it's shorter than `length`. Padding
characters are truncated if they exceed `length`.

#### Arguments
1. `[string='']` *(string)*: The string to pad.
2. `[length=0]` *(number)*: The padding length.
3. `[chars=' ']` *(string)*: The string used as padding.

#### Returns
*(string)*:  Returns the padded string.

#### Example
```js
_.padRight('abc', 6);
// => 'abc   '

_.padRight('abc', 6, '_-');
// => 'abc_-_'

_.padRight('abc', 3);
// => 'abc'
```

### _.parseInt(string, [radix])

Converts `string` to an integer of the specified radix. If `radix` is
`undefined` or `0`, a `radix` of `10` is used unless `value` is a hexadecimal,
in which case a `radix` of `16` is used.
<br>
<br>
**Note:** This method aligns with the [ES5 implementation](https://es5.github.io/#E)
of `parseInt`.

#### Arguments
1. `string` *(string)*: The string to convert.
2. `[radix]` *(number)*: The radix to interpret `value` by.

#### Returns
*(number)*:  Returns the converted integer.

#### Example
```js
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

### _.repeat([string=''], [n=0])

Repeats the given string `n` times.

#### Arguments
1. `[string='']` *(string)*: The string to repeat.
2. `[n=0]` *(number)*: The number of times to repeat the string.

#### Returns
*(string)*:  Returns the repeated string.

#### Example
```js
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

### _.snakeCase([string=''])

Converts `string` to [snake case](https://en.wikipedia.org/wiki/Snake_case).

#### Arguments
1. `[string='']` *(string)*: The string to convert.

#### Returns
*(string)*:  Returns the snake cased string.

#### Example
```js
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--foo-bar');
// => 'foo_bar'
```

### _.startCase([string=''])

Converts `string` to [start case](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage).

#### Arguments
1. `[string='']` *(string)*: The string to convert.

#### Returns
*(string)*:  Returns the start cased string.

#### Example
```js
_.startCase('--foo-bar');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__foo_bar__');
// => 'Foo Bar'
```

### _.startsWith([string=''], [target], [position=0])

Checks if `string` starts with the given target string.

#### Arguments
1. `[string='']` *(string)*: The string to search.
2. `[target]` *(string)*: The string to search for.
3. `[position=0]` *(number)*: The position to search from.

#### Returns
*(boolean)*:  Returns `true` if `string` starts with `target`, else `false`.

#### Example
```js
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

### _.template([string=''], [options])

Creates a compiled template function that can interpolate data properties
in "interpolate" delimiters, HTML-escape interpolated data properties in
"escape" delimiters, and execute JavaScript in "evaluate" delimiters. Data
properties may be accessed as free variables in the template. If a setting
object is provided it takes precedence over `_.templateSettings` values.
<br>
<br>
**Note:** In the development build `_.template` utilizes
[sourceURLs](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl)
for easier debugging.
<br>
<br>
For more information on precompiling templates see
[lodash's custom builds documentation](https://lodash.com/custom-builds).
<br>
<br>
For more information on Chrome extension sandboxes see
[Chrome's extensions documentation](https://developer.chrome.com/extensions/sandboxingEval).

#### Arguments
1. `[string='']` *(string)*: The template string.
2. `[options]` *(Object)*: The options object.
3. `[options.escape]` *(RegExp)*: The HTML "escape" delimiter.
4. `[options.evaluate]` *(RegExp)*: The "evaluate" delimiter.
5. `[options.imports]` *(Object)*: An object to import into the template as free variables.
6. `[options.interpolate]` *(RegExp)*: The "interpolate" delimiter.
7. `[options.sourceURL]` *(string)*: The sourceURL of the template's compiled source.
8. `[options.variable]` *(string)*: The data object variable name.

#### Returns
*(Function)*:  Returns the compiled template function.

#### Example
```js
// using the "interpolate" delimiter to create a compiled template
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// using the HTML "escape" delimiter to escape data property values
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// using the "evaluate" delimiter to execute JavaScript and generate HTML
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// using the internal `print` function in "evaluate" delimiters
var compiled = _.template('<% print("hello " + user); %>!');
compiled({ 'user': 'barney' });
// => 'hello barney!'

// using the ES delimiter as an alternative to the default "interpolate" delimiter
var compiled = _.template('hello ${ user }!');
compiled({ 'user': 'pebbles' });
// => 'hello pebbles!'

// using custom template delimiters
_.templateSettings.interpolate = /{{([\s\S]+?)}}/g;
var compiled = _.template('hello {{ user }}!');
compiled({ 'user': 'mustache' });
// => 'hello mustache!'

// using backslashes to treat delimiters as plain text
var compiled = _.template('<%= "\\<%- value %\\>" %>');
compiled({ 'value': 'ignored' });
// => '<%- value %>'

// using the `imports` option to import `jQuery` as `jq`
var text = '<% jq.each(users, function(user) { %><li><%- user %></li><% }); %>';
var compiled = _.template(text, { 'imports': { 'jq': jQuery } });
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'

// using the `sourceURL` option to specify a custom sourceURL for the template
var compiled = _.template('hello <%= user %>!', { 'sourceURL': '/basic/greeting.jst' });
compiled(data);
// => find the source of "greeting.jst" under the Sources tab or Resources panel of the web inspector

// using the `variable` option to ensure a with-statement isn't used in the compiled template
var compiled = _.template('hi <%= data.user %>!', { 'variable': 'data' });
compiled.source;
// => function(data) {
//   var __t, __p = '';
//   __p += 'hi ' + ((__t = ( data.user )) == null ? '' : __t) + '!';
//   return __p;
// }

// using the `source` property to inline compiled templates for meaningful
// line numbers in error messages and a stack trace
fs.writeFileSync(path.join(cwd, 'jst.js'), '\
  var JST = {\
    "main": ' + _.template(mainText).source + '\
  };\
');
```

### _.trim([string=''], [chars=whitespace])

Removes leading and trailing whitespace or specified characters from `string`.

#### Arguments
1. `[string='']` *(string)*: The string to trim.
2. `[chars=whitespace]` *(string)*: The characters to trim.

#### Returns
*(string)*:  Returns the trimmed string.

#### Example
```js
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

### _.trimLeft([string=''], [chars=whitespace])

Removes leading whitespace or specified characters from `string`.

#### Arguments
1. `[string='']` *(string)*: The string to trim.
2. `[chars=whitespace]` *(string)*: The characters to trim.

#### Returns
*(string)*:  Returns the trimmed string.

#### Example
```js
_.trimLeft('  abc  ');
// => 'abc  '

_.trimLeft('-_-abc-_-', '_-');
// => 'abc-_-'
```

### _.trimRight([string=''], [chars=whitespace])

Removes trailing whitespace or specified characters from `string`.

#### Arguments
1. `[string='']` *(string)*: The string to trim.
2. `[chars=whitespace]` *(string)*: The characters to trim.

#### Returns
*(string)*:  Returns the trimmed string.

#### Example
```js
_.trimRight('  abc  ');
// => '  abc'

_.trimRight('-_-abc-_-', '_-');
// => '-_-abc'
```

### _.trunc([string=''], [options], [options.length=30], [options.omission='...'], [options.separator])

Truncates `string` if it's longer than the given maximum string length.
The last characters of the truncated string are replaced with the omission
string which defaults to "...".

#### Arguments
1. `[string='']` *(string)*: The string to truncate.
2. `[options]` *(Object|number)*: The options object or maximum string length.
3. `[options.length=30]` *(number)*: The maximum string length.
4. `[options.omission='...']` *(string)*: The string to indicate text is omitted.
5. `[options.separator]` *(RegExp|string)*: The separator pattern to truncate to.

#### Returns
*(string)*:  Returns the truncated string.

#### Example
```js
_.trunc('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'

_.trunc('hi-diddly-ho there, neighborino', 24);
// => 'hi-diddly-ho there, n...'

_.trunc('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'

_.trunc('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': /,? +/
});
// => 'hi-diddly-ho there...'

_.trunc('hi-diddly-ho there, neighborino', {
  'omission': ' [...]'
});
// => 'hi-diddly-ho there, neig [...]'
```

### _.unescape([string=''])

The inverse of `_.escape`; this method converts the HTML entities
`&amp;`, `&lt;`, `&gt;`, `&quot;`, `&#39;`, and `&#96;` in `string` to their
corresponding characters.
<br>
<br>
**Note:** No other HTML entities are unescaped. To unescape additional HTML
entities use a third-party library like [_he_](https://mths.be/he).

#### Arguments
1. `[string='']` *(string)*: The string to unescape.

#### Returns
*(string)*:  Returns the unescaped string.

#### Example
```js
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

### _.words([string=''], [pattern])

Splits `string` into an array of its words.

#### Arguments
1. `[string='']` *(string)*: The string to inspect.
2. `[pattern]` *(RegExp|string)*: The pattern to match words.

#### Returns
*(Array)*:  Returns the words of `string`.

#### Example
```js
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```
