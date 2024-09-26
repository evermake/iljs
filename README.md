### subjective `null`

```js
{} instanceof null
// Uncaught TypeError: Right-hand side of 'instanceof' is not an object
```

```js
typeof null
// 'object'
```

**[Explanation](https://stackoverflow.com/a/7968470)**

`null` is not an object, but a primitive value. `typeof null` returning `'object'` is a bug, which is not fixed due to backward-compatability.

---

### '2' + '2' - '2' = 20

```js
'2' + '2' - '2'
// 20
```

**[Explanation](https://stackoverflow.com/a/48675918)**

- `+` is both concatenation and addition (`'2' + '2'` is `'22'`);
- `-` is only subtraction and arguments are coerced to numbers (`'22' - 2` is `20`).

---

### `typeof` undeclared

```js
console.log(abc)
// Uncaught ReferenceError: abc is not defined
```

```js
console.log(typeof abc)
// 'undefined'
```

**Explanation**

`typeof` operator can check whether the variable has been declared.

---

### [sparse arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#sparse_arrays)

```js
console.log(Array(5))
// [ <5 empty items> ]

const arr = [1,,,2,,,3]

console.log(arr.length)
// 7

arr.forEach((item, idx) => console.log(item, idx))
// 1 0
// 2 3
// 3 6

console.log(JSON.stringify(arr))
// '[1,null,null,2,null,null,3]'

const arr2 = [...arr]
arr2.forEach((item, idx) => console.log(item, idx))
// 1 0
// undefined 1
// undefined 2
// 2 3
// undefined 4
// undefined 5
// 3 6

arr[1000] = 1

console.log(arr.length)
// 1001

console.log(arr)
// [ 1, <2 empty items>, 2, <2 empty items>, 3, <993 empty items>, 1 ]
```

**Story**

Someday I was writing a Telegram bot and spent several hours debugging one issue.

Bot had logging functionality and logged something `JSON.stringif`ied, and after some changes I got an error:

```
FATAL ERROR: JS Allocation failed - process out of memory
```

In short, the problem was that I was setting some array's item by _Telegram user's ID_ (which was big like 987654321). So JS tried to stringify an array with nine hundred eighty-seven million six hundred fifty-four thousand three hundred twenty-one `null` and ran out of memory:

```js
arr[user.id] = 'hi'
JSON.stringify(arr)
// FATAL ERROR: JS Allocation failed - process out of memory
```

---

### `parseInt`

```js
parseInt(0.5)
// 0

parseInt(0.005)
// 0

parseInt(0.0000005)
// 5
```

**Explanation**

- The `parseInt` function _converts its first argument to a string_, parses that string, then returns an integer or `NaN`.
- If `parseInt` encounters a character that is not a numeral in the specified `radix`, it _ignores it and all succeeding characters_ and returns the integer value parsed up to that point.
- `(0.5).toString()` -> `'0.5'`
- `(0.0000005).toString()` -> `'5e-7'`
