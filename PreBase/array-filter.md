# filter

数组有个 `filter()` 方法. 用于得到一个过滤原数组元素, 得到新数组, `filter()` 返回 `bool` 值, 根据 `true` 和 `false` 是否留下某个元素.

假设下面代码:

```js
let arr = [1, 2, 3, 4];
```

现在我们用一下 `map` 方法.

```js
let arr = [1, 2, 3, 4];

// elt: 当前遍历到的元素
// i: 当前遍历到的元素的索引
let newArr = arr.filter( (elt, i)=>{

  console.log(i);

  // 返回 true 就会留下, false 就会被移除
  // 这里会保留 值不等于 2 的元素
  return elt !== 2;
} );

console.log(newArr); // [1,3,4]

```

可以看到, `filter` 接受一个回调函数作为参数.

回调函数有两个参数,
    第一个参数是: 遍历到的元素
    第二个元素是: 元素索引

回调函数返回 `true` 就会保留元素, `false` 就好移除元素.

---

:point_right::point_right:[下一节, 我们看看 `every()` 方法](./array-every.md)

[回到大纲](../README.md#outline) :point_left::point_left:
