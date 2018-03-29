# Spread 与 Rest

ES6 提供了 `spread` 和 `rest` 来出里数据的合并与读取问题, 这是一个很大的便利.

## Spread, 展开

展开的语法是: `...`, 没错, 就是英文的三个小点.

展开, 是为了把自己的数据, 展开给别人.

我们会经常用这个语法做一些数据展开操作:

**1. 把一个数组展开到另外一个数组里**

```js
let arr1 = [1, 2];
let arr2 = ['a', 'b'];

console.log( [...arr1, ...arr2, 9, 0] );
// 打印 [1,2,3,'a','b',9,0]

// 展开的位置就是顺序
console.log( [ 9, 0, ...arr2] );
// 打印 [9, 0, 'a', 'b']

```

**2. 把一个对象展开到另外一个对象里**

```js
let names = {
  p1: 'Sal',
  p2: 'Bob'
};

let out = {
  ...names,
  p3: 'Moli'
};

console.log(out); // {p1: 'Sal', p2: 'Bob', p3: 'Moli'}

// 后面的属性会把前面的属性覆盖

console.log({
  ...names,
  p1: 'Jack'
}); // 打印 {p1: 'Jack', p2: 'Bob'}

console.log({
  p1: 'Jack'
  ...names,
}); // 打印 {p1: 'Sal', p2: 'Bob'}

```

**3. 在函数参数列表里展开**

```js
// 假设有一个数组和一个函数

let arr = [1,2,3,4];

function logs(a, b) {
  console.log(a,b);
}

// 传参数的时候直接展开数组

logs(...arr); // 打印了 1 2
// ===== 相当于
logs(1,2,3,4);

```

## rest, 剩余

剩余, 就是代表剩余的数据. 让你拿到处理某些东西以外, 剩余的东西.

它的语法也是 `...`. :scream::scream::scream:

看看下面的情况:

**1. 解构数组时, 拿到剩余的元素**

```js
let arr = [1,2,3,4];

let [a,...rest] = arr;

console.log(a); // 1
console.log(rest); //数组: [2,3,4]

```

可以看到, 数组里面, `rest` 是剩余没取完的元素所组成的**数组**.

> 提示: rest 只是一个变量名, 所以它可以是毕节的名字, 比如:
>
> let [a,...restElt] = arr;

> 注意: rest 必须要写在数组末尾

**2. 解构对象时, 拿到剩余的属性**

```js
let obj = {
  a: 1,
  b: 2,
  c: 3
};

let { b, ...rest} = obj;

console.log(b); // 2
console.log(rest); // {a:1, c:3}

```

可以看到, 对象里面, `rest` 是剩余没取完的属性组成的一个**对象**.

> 注意: 虽然是解构一个对象, 但是 rest 应该在对象最后面写

**3. 拿到函数的剩余参数**


```js
// rest 代表剩余的参数组成的素组
function logs(a, b, ...rest) {
  console.log(a,b);
  console.log(rest);
}

logs(1);
// 第一个打印: 1, undefined
// 第二个打印: [] (空数组)

logs(1, 2);
// 第一个打印: 1, 2
// 第二个打印: [] (空数组)

logs(1, 2, 3);
// 第一个打印: 1, 2
// 第二个打印: [3]
//
logs(1, 2, 3, 4);
// 第一个打印: 1, 2
// 第二个打印: [3,4]
```

可以看到, 参数列表里面, `rest` 是剩余传过来的参数所组成的一个**数组**.

---

:point_right::point_right:[下一节, 我们看看 ES6 的 class](./6-Class.md)

[回到大纲](../README.md#outline) :point_left::point_left:
