# every

数组有个 `every()` 方法. 返回 `bool` 值.

假设下面代码:

```js
let arr = [1, 2, 3, 4];
```

现在我们用一下 `every` 方法.

```js
let arr = [1, 2, 3, 4];

// elt: 当前遍历到的元素
// i: 当前遍历到的元素的索引
let bool = arr.every( (elt, i)=>{

  console.log(i);
  console.log(elt);

  // 如果每一次遍历, 回调函数 都返回 true, 那么
  // 那么这一次 every() 返回 true
  // 只要有一次返回 false, 那么 every() 返回 false
  return elt === i+1;
} );

console.log(bool); // true

```

可以看到, `filter` 接受一个回调函数作为参数.

回调函数有两个参数,
    第一个参数是: 遍历到的元素
    第二个元素是: 元素索引

如果每一次遍历, 回调函数 都返回 `true`, 那么
那么这一次 `every()` 返回 `true`
只要有一次返回 `false`, 那么 `every()` 返回 `false`

---

:point_right::point_right:[下一节, 我们看看 `some()` 方法](./array-some.md)

[回到大纲](../README.md#outline) :point_left::point_left:
