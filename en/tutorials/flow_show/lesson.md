If you've used JSX in the past, you may have used native JavaScript like [`Array.prototype.map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) or ternaries to handle control flow in templates. But without a Virtual DOM, these techniques aren't always optimal. Instead, Solid ships with control flow helper components.

The most basic control flow is the conditional. Solid's compiler is smart enough to optimally handle ternaries (`a ? b : c`) and boolean expressions (`a && b`). However, it is often still more readable to use Solid's `<Show>` component.

In the example, we would like to show only the appropriate button that reflects the current state (whether or not the user is logged in). Update the JSX to:
```jsx
<Show
  when={loggedIn()}
  fallback={<button onClick={toggle}>Log in</button>}
>
  <button onClick={toggle}>Log out</button>
</Show>
```
The `fallback` prop acts as the `else` and will show when the condition passed to `when` is not truthy.

Now clicking the button will change back and forth like you would expect.
