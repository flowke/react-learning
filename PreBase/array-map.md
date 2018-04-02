# map 方法

数组有个 `map()` 方法. 用于得到一个新数组, 新数组里面的元素依据 `map()` 的返回值而定.

假设下面代码:

```js
let arr = [1, 2, 3, 4];
```

现在我们用一下 `map` 方法.

```js
let arr = [1, 2, 3, 4];

// elt: 当前遍历到的元素
// i: 当前遍历到的元素的索引
let newArr = arr.map( (elt, i)=>{

  console.log(i);

  return elt + 10;
} );

console.log(newArr); // [11, 12, 13, 14]

```

可以看到, `map` 接受一个回调函数作为参数.

回调函数有两个参数,
    第一个参数是: 遍历到的元素
    第二个元素是: 元素索引

回调函数返回的值会作为新数组的元素.

---

:point_right::point_right:[下一节, 我们看看 `filter()` 方法](./array-filter.md)

[回到大纲](../README.md#outline) :point_left::point_left:
