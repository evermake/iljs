### subjective `null`

```js
{} instanceof null
// Uncaught TypeError: Right-hand side of 'instanceof' is not an object
```

```js
typeof null
// 'object'
```

**[Explanation](https://stackoverflow.com/a/7968470)**<br/>
`null` is not an object, but a primitive value. `typeof null` returning `'object'` is bug, which is not fixed for the backward-compatability.
