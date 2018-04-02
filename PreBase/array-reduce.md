# reduce

`reduce()` 依然接收一个回调函数, 返回 最后一次回调函数执行的结果.

## 语法

`arr.reduce( reducer, initial_value)`

```
关于两个参数:
  reducer 是一个回调函数, 接受 4 个参数:

    accumulator: 代表上一次回调函数的返回值
    currentValue: 当前遍历的值
    index: 索引 (可选)
    array: 调用 reduce 的数组 (可选)

  initial_value 是 accumulator 的初始值 (可选)
```

我们看下面使用示例:

```js
let arr = [1, 2, 3, 4];

let value = arr.reduce((accu, elt)=>{
  // accu 是上一次回调函数的返回值, 如果第一次调用, 初始值是 0
  // elt 是当前遍历到的元素的值
  return accu + elt;

  // 0是第一次调用回调函数时, accu 的初始值
}, 0)

console.log(value); // 10 = 0+1+2+3+4

```

可以看到实例, accu 是上一次函数调用的返回值, `reduce()` 最终的返回值是 最后一次回调函数返回的值.

> 注意::exclamation::exclamation::exclamation:
> 如果没有提供 initial_value, 那么 `reduce()` 会从索引 1 的地方开始遍历, 这时, accu 的值会是 第 0 个元素.
>

---

[回到大纲](../README.md#outline) :point_left::point_left:
