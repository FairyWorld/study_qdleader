# Array.of()

Array.of()
用于将一组值，转换为数组

```js
Array.of(); // []
Array.of(3); // [3]
Array.of(3, 11, 8); // [3,11,8]
```

## Array()

没有参数的时候，返回一个空数组

当参数只有一个的时候，实际上是指定数组的长度

参数个数不少于 2 个时，Array()才会返回由参数组成的新数组

```js
Array(); // []
Array(3); // [, , ,]
Array(3, 11, 8); // [3, 11, 8]
```

Array.of() 和 Array() 构造函数之间的区别在于对单个参数的处理：Array.of(7) 创建一个具有单个元素 7 的数组，而 Array(7) 创建一个 length 为 7 的空数组（这意味着一个由 7 个空槽组成的数组，而不是由 7 个 undefined 组成的数组）。
