proposal-array-select-reject
============================

A Stage 0 proposal to add `Array.prototype.select` and
`Array.prototype.reject`.

```js
const array = [1, 2, 3, 4, 5];

// Select is just an alias for Array.p.filter
array.select(i => (i < 3)); // => [1, 2];

// Reject does the opposite of select.
array.reject(i => (i < 3)); // => [3, 4, 5];
```

Motivation
----------

`Array.prototype.filter` is confusing. I constantly have to ask myself
"am I filtering in, or filtering out the current item?".

<dl>
  <dt>"Filtering in"</dt>
  <dd>

  Implies that returning `true` would keep the current item.

  </dd>

  <dt>"Filtering out"</dt>
  <dd>

  Implies that returning `true` would remove the current item.

  </dd>
</dl>

`Array.p.filter` acts as "filtering in". But when I think of the word
"filter", I think of "filtering out". So every time that I attempt to
write an array filter, I end up writing the opposite of what I intended.

`Array.p.select` fixes this confusion. You are _selecting_ the current
item. Similarly, `Array.p.reject` means you are _rejecting_ the current
item.


Semantics
---------

### `Array.prototype.select(callbackfn[, thisArg ])`

The initial value of the `select` property is the same function object
as the initial value of the `Array.prototype.filter` property.

### `Array.prototype.reject(callbackfn[, thisArg ])`

When the `reject` method is called with one or two arguments, the
following steps are taken:

1. Let `O` be `? ToObject(this value)`.
1. Let `len` be `? LengthOfArrayLike(O)`.
1. If `IsCallable(callbackfn)` is `false`, throw a `TypeError` exception.
1. If `thisArg` is present, let `T` be `thisArg`; else let `T` be `undefined`.
1. Let `A` be `? ArraySpeciesCreate(O, 0)`.
1. Let `k` be 0.
1. Let `to` be 0.
1. Repeat, while `k` &lt; `len`
   1. Let `Pk` be `! ToString(k)`.
   1. Let `kPresent` be `? HasProperty(O, Pk)`.
   1. If `kPresent` is `true`, then
      1. Let `kValue` be `? Get(O, Pk)`.
      1. Let `selected` be `! ToBoolean(? Call(callbackfn, T, « kValue, k, O »))`.
      1. If `selected` is `false`, then
      1. Perform `? CreateDataPropertyOrThrow(A, ! ToString(to), kValue)`.
   1. Set `to` to `to + 1`.
   1. Set `k` to `k + 1`.
1. Return `A`.

Related
-------

- Ruby
  - [`Array#select`](https://ruby-doc.org/core-2.4.1/Array.html#method-i-select)
  - [`Array#reject`](https://ruby-doc.org/core-2.4.1/Array.html#method-i-reject)
- Underscore
  - [`_.select`](https://underscorejs.org/#filter) (aliased to _.filter)
  - [`_.reject`](https://underscorejs.org/#reject)
- Lodash
  - [`_.reject`](https://lodash.com/docs/4.17.15#reject) ([700,000 downloads/week](https://www.npmjs.com/package/lodash.reject))
