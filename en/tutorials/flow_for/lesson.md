To iterate over a list in template, use the `<For>` helper component. Let's see how this works by iterating over our array of cats:

```jsx
<For each={cats()}>{(cat, i) =>
  <li>
    <a target="_blank" href={`https://www.youtube.com/watch?v=${cat.id}`}>
      {i() + 1}: {cat.name}
    </a>
  </li>
}</For>
```

`<For>` takes an `each` prop, which is the array to iterate over. The child of the `<For>` component is a bit different than what we've seen so far: it's a _function_,
similar to the callback in JavaScript's [`forEach`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach), that maps the current element and its index to a view node.

It is automatically keyed by reference, so as data updates it is optimized to update or move rows rather than recreate them. The callback is non-tracking and passes the item and an index Signal.

The `index` is a Signal so that it can update independently when the row is moved. The item is not a Signal as changing would mean a new reference and cause a new row to be created. The way to do nested updates is to make nested Signals or use Solid's Store proxy.

You can also use `<For>` to iterate over other iterable objects that are not arrays by using methods like `Object.keys` or simple spreading into an array like `[...iterable]`.