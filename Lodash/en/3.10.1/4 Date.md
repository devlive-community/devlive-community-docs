[TOC]

### _.now

Gets the number of milliseconds that have elapsed since the Unix epoch
(1 January 1970 00:00:00 UTC).

#### Example
```js
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => logs the number of milliseconds it took for the deferred function to be invoked
```
