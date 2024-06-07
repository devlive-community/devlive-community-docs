[TOC]

### noConflict

`_.noConflict()` [source](https://underscorejs.org/docs/modules/noConflict.html)  

Give control of the global _ variable back to its previous owner. Returns a reference to the **Underscore** object.

```js
var underscore = _.noConflict();
```

The `_.noConflict` function is not present if you use the EcmaScript 6, AMD or CommonJS module system to import Underscore.

### identity

`_.identity(value)` [source](https://underscorejs.org/docs/modules/identity.html)  

Returns the same value that is used as the argument. In math: f(x) = x  
This function looks useless, but is used throughout Underscore as a default iteratee.

```js
var stooge = {name: 'moe'};
stooge === _.identity(stooge);
=> true
```

### constant

`_.constant(value)` [source](https://underscorejs.org/docs/modules/constant.html)  

Creates a function that returns the same value that is used as the argument of \_.constant.

```js
var stooge = {name: 'moe'};
stooge === _.constant(stooge)();
=> true
```

### noop

`_.noop()` [source](https://underscorejs.org/docs/modules/noop.html)  

Returns undefined irrespective of the arguments passed to it. Useful as the default for optional callback arguments.

```js
obj.initialize = _.noop;
```

### times

`_.times(n, iteratee, [context])` [source](https://underscorejs.org/docs/modules/times.html)  

Invokes the given iteratee function **n** times. Each invocation of [**iteratee**](#iteratee) is called with an index argument. Produces an array of the returned values.

```js
_.times(3, function(n){ genie.grantWishNumber(n); });
```

### random

`_.random(min, max)` [source](https://underscorejs.org/docs/modules/random.html)  

Returns a random integer between **min** and **max**, inclusive. If you only pass one argument, it will return a number between 0 and that number.

```js
_.random(0, 100);
=> 42
```

### mixin

`_.mixin(object)` [source](https://underscorejs.org/docs/modules/mixin.html)  

Allows you to extend Underscore with your own utility functions. Pass a hash of `{name: function}` definitions to have your functions added to the Underscore object, as well as the OOP wrapper. Returns the Underscore object to facilitate chaining.

```js
_.mixin({
  capitalize: function(string) {
    return string.charAt(0).toUpperCase() + string.substring(1).toLowerCase();
  }
});
_("fabio").capitalize();
=> "Fabio"
```

### iteratee

`_.iteratee(value, [context])` [source](https://underscorejs.org/docs/modules/iteratee.html)  

Generates a callback that can be applied to each element in a collection. _.iteratee supports a number of shorthand syntaxes for common callback use cases. Depending upon value's type, _.iteratee will return:

```js
// No value
_.iteratee();
=> _.identity()

// Function
_.iteratee(function(n) { return n * 2; });
=> function(n) { return n * 2; }

// Object
_.iteratee({firstName: 'Chelsea'});
=> _.matcher({firstName: 'Chelsea'});

// Anything else
_.iteratee('firstName');
=> _.property('firstName');
```

The following Underscore methods transform their predicates through `_.iteratee`: `countBy`, `every`, `filter`, `find`, `findIndex`, `findKey`, `findLastIndex`, `groupBy`, `indexBy`, `map`, `mapObject`, `max`, `min`, `partition`, `reject`, `some`, `sortBy`, `sortedIndex`, and `uniq`

You may overwrite `_.iteratee` with your own custom function, if you want additional or different shorthand syntaxes:

```js
// Support `RegExp` predicate shorthand.
var builtinIteratee = _.iteratee;
_.iteratee = function(value, context) {
  if (_.isRegExp(value)) return function(obj) { return value.test(obj) };
  return builtinIteratee(value, context);
};
```

### uniqueId

`_.uniqueId([prefix])` [source](https://underscorejs.org/docs/modules/uniqueId.html)  

Generate a globally-unique id for client-side models or DOM elements that need one. If **prefix** is passed, the id will be appended to it.

```js
_.uniqueId('contact_');
=> 'contact_104'
```

### escape

`_.escape(string)` [source](https://underscorejs.org/docs/modules/escape.html)  

Escapes a string for insertion into HTML, replacing `&`, `<`, `>`, `"`, \`, and `'` characters.

```js
_.escape('Curly, Larry & Moe');
=> "Curly, Larry &amp; Moe"
```

### unescape

`_.unescape(string)` [source](https://underscorejs.org/docs/modules/unescape.html)  

The opposite of [**escape**](#escape), replaces &amp;, &lt;, &gt;, &quot;, &#x60; and &#x27; with their unescaped counterparts.

```js
_.unescape('Curly, Larry &amp; Moe');
=> "Curly, Larry & Moe"
```

### result

`_.result(object, property, [defaultValue])` [source](https://underscorejs.org/docs/modules/result.html)  

If the value of the named **property** is a function then invoke it with the **object** as context; otherwise, return it. If a default value is provided and the property doesn't exist or is undefined then the default will be returned. If defaultValue is a function its result will be returned.

```js
var object = {cheese: 'crumpets', stuff: function(){ return 'nonsense'; }};
_.result(object, 'cheese');
=> "crumpets"
_.result(object, 'stuff');
=> "nonsense"
_.result(object, 'meat', 'ham');
=> "ham"
```

### now

`_.now()` [source](https://underscorejs.org/docs/modules/now.html)  

Returns an integer timestamp for the current time, using the fastest method available in the runtime. Useful for implementing timing/animation functions.

```js
_.now();
=> 1392066795351
```

### template

`_.template(templateString, [settings])` [source](https://underscorejs.org/docs/modules/template.html)  

Compiles JavaScript templates into functions that can be evaluated for rendering. Useful for rendering complicated bits of HTML from JSON data sources. Template functions can both interpolate values, using `<%= … %>`, as well as execute arbitrary JavaScript code, with `<% … %>`. If you wish to interpolate a value, and have it be HTML-escaped, use `<%- … %>`. When you evaluate a template function, pass in a **data** object that has properties corresponding to the template's free variables. The **settings** argument should be a hash containing any `_.templateSettings` that should be overridden.

```js
var compiled = _.template("hello: <%= name %>");
compiled({name: 'moe'});
=> "hello: moe"

var template = _.template("<b><%- value %></b>");
template({value: '<script>'});
=> "<b>&lt;script&gt;</b>"
```

You can also use `print` from within JavaScript code. This is sometimes more convenient than using `<%= ... %>`.

```js
var compiled = _.template("<% print('Hello ' + epithet); %>");
compiled({epithet: "stooge"});
=> "Hello stooge"
```

If ERB-style delimiters aren't your cup of tea, you can change Underscore's template settings to use different symbols to set off interpolated code. Define an **interpolate** regex to match expressions that should be interpolated verbatim, an **escape** regex to match expressions that should be inserted after being HTML-escaped, and an **evaluate** regex to match expressions that should be evaluated without insertion into the resulting string. Note that if part of your template matches more than one of these regexes, the first will be applied by the following order of priority: (1) **escape**, (2) **interpolate**, (3) **evaluate**. You may define or omit any combination of the three. For example, to perform [Mustache.js](https://github.com/janl/mustache.js#readme)\-style templating:

```js
_.templateSettings = {
  interpolate: /\{\{(.+?)\}\}/g
};

var template = _.template("Hello {{ name }}!");
template({name: "Mustache"});
=> "Hello Mustache!"
```

By default, **template** places the values from your data in the local scope via the with statement. However, you can specify a single variable name with the **variable** setting. This can significantly improve the speed at which a template is able to render.

```js
_.template("Using 'with': <%= data.answer %>", {variable: 'data'})({answer: 'no'});
=> "Using 'with': no"
```

Precompiling your templates can be a big help when debugging errors you can't reproduce. This is because precompiled templates can provide line numbers and a stack trace, something that is not possible when compiling templates on the client. The **source** property is available on the compiled template function for easy precompilation.

```js
<script>
  JST.project = <%= _.template(jstText).source %>;
</script>
```
