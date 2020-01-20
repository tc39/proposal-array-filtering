# proposal-array-filtering

A proposal to add `Array.prototype.filterOut`.

```js
const array = [1, 2, 3, 4, 5];

// filter keeps the items that return true.
array.filter(i => (i < 3)); // => [1, 2];

// filterOut removes the items that return true.
array.filterOut(i => (i < 3)); // => [3, 4, 5];
```

## Champions

- Justin Ridgewell ([@jridgewell](https://github.com/jridgewell/))

## Status

Current [Stage](https://tc39.es/process-document/): 1

## Motivation

`Array.p.filter` is confusing. I constantly have to ask myself "am I
keeping, or filtering out the current item?".

<dl>
  <dt>"Keeping"</dt>
  <dd>

  Implies that returning `true` would keep the current item.

  </dd>

  <dt>"Filtering out"</dt>
  <dd>

  Implies that returning `true` would remove the current item.

  </dd>
</dl>

`Array.p.filter` acts as "keeping". But when I think of the word
"filter", I think of "filtering out". So every time that I attempt to
write an array filter, I end up writing the opposite of what I intended.

`Array.p.filterOut` attempts to fix this confusion. By providing a
clearly named filtering function that matches my intuition, I'm able
what will happen when calling `filterOut`. And because it exists, I'm
able to assume that `filter` does something different, so it must be
"keep" version.

## Ongoing Discussions

- [Supporting Data from HTTP Archive and GitHub Archive](https://github.com/jridgewell/proposal-array-filtering/issues/4)
- [What should `filterOut` be called?](https://github.com/jridgewell/proposal-array-filtering/issues/6)
- [Should `partition` be included?](https://github.com/jridgewell/proposal-array-filtering/issues/2)

## Related

- Ruby
  - [`Array#select`](https://ruby-doc.org/core-2.4.1/Array.html#method-i-select)
  - [`Array#reject`](https://ruby-doc.org/core-2.4.1/Array.html#method-i-reject)
  - [`Array#partition`](https://ruby-doc.org/core-2.5.1/Enumerable.html#method-i-partition)
- Underscore
  - [`_.select`](https://underscorejs.org/#filter) (aliased to _.filter)
  - [`_.reject`](https://underscorejs.org/#reject)
  - [`_.partition`](https://underscorejs.org/#partition)
- Lodash
  - [`_.reject`](https://lodash.com/docs/4.17.15#reject) ([700k downloads/week](https://www.npmjs.com/package/lodash.reject))
  - [`_.partition`](https://lodash.com/docs/4.17.15#partition) ([18k downloads/week](https://www.npmjs.com/package/lodash.partition))
