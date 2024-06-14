[TOC]

### _.VERSION

(string): The semantic version number.

### _.support

(Object): An object environment feature flags.

### _.support.enumErrorProps

(boolean): Detect if `name` or `message` properties of `Error.prototype` are
enumerable by default (IE < 9, Safari < 5.1).

### _.support.enumPrototypes

(boolean): Detect if `prototype` properties are enumerable by default.
<br>
<br>
Firefox < 3.6, Opera > 9.50 - Opera < 11.60, and Safari < 5.1
(if the prototype or a property on the prototype has been set)
incorrectly set the `[[Enumerable]]` value of a function's `prototype`
property to `true`.

### _.support.nonEnumShadows

(boolean): Detect if properties shadowing those on `Object.prototype` are non-enumerable.
<br>
<br>
In IE < 9 an object's own properties, shadowing non-enumerable ones,
are made non-enumerable as well (a.k.a the JScript `[[DontEnum]]` bug).

### _.support.ownLast

(boolean): Detect if own properties are iterated after inherited properties (IE < 9).

### _.support.spliceObjects

(boolean): Detect if `Array#shift` and `Array#splice` augment array-like objects
correctly.
<br>
<br>
Firefox < 10, compatibility modes of IE 8, and IE < 9 have buggy Array
`shift()` and `splice()` functions that fail to remove the last element,
`value[0]`, of array-like objects even though the "length" property is
set to `0`. The `shift()` method is buggy in compatibility modes of IE 8,
while `splice()` is buggy regardless of mode in IE < 9.

### _.support.unindexedChars

(boolean): Detect lack of support for accessing string characters by index.
<br>
<br>
IE < 8 can't access characters by index. IE 8 can only access characters
by index on string literals, not string objects.

### _.templateSettings

(Object): By default, the template delimiters used by lodash are like those in
embedded Ruby (ERB). Change the following template settings to use
alternative delimiters.

### _.templateSettings.escape

(RegExp): Used to detect `data` property values to be HTML-escaped.

### _.templateSettings.evaluate

(RegExp): Used to detect code to be evaluated.

### _.templateSettings.imports

(Object): Used to import variables into the compiled template.

### _.templateSettings.interpolate

(RegExp): Used to detect `data` property values to inject.

### _.templateSettings.variable

(string): Used to reference the data object in the template text.
