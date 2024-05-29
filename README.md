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

### '2' + '2' - '2' = 20

```js
'2' + '2' - '2'
// 20
```

**[Explanation](https://stackoverflow.com/a/48675918)**<br/>
- `+` is both concatenation and addition (`'2' + '2'` is `'22'`);
- `-` is only subtraction and arguments are coerced to numbers (`'22' - 2` is `20`).
