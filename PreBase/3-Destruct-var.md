# 变量的解构赋值

现在如果有一个对象, 你可以直接提取里面的属性值:

```js

// 有一个对象 names

let names = {
  p1: 'Flowke',
  p2: 'Sal'
}

// 想使用 p1, 或 p2 的值, 可以这样
// 用一个花括号包住要提取的属性名
// 这个时候作用域里面就会有两个变量
// 当然, 你不必全部属性都取完, 其中一部分就可以了
let {p1, p2} = names;

console.log(p1); // Flowke
console.log(p2); // Sal


```

可以看到, 你可以通过解构快速得到对象属性的一些值.

当然, 你也可以**使用新的变量名**:

```js
let names = {
  p1: 'Flowke',
  p2: 'Sal'
};

// p1 是要匹配的属性名, nP1 是要定义的变量名
let {p1: nP1, p2: nP2} = names;

console.log(nP1); // Flowke
console.log(nP2); // Sal
console.log(p1); // 报错, 没有定义的变量
console.log(p2); // 报错, 没有定义的变量

// 其实之前的写法是一直简写的形式
let {p1, p2} = names;
// ==== 相当于
let {p1:p1, p2:p2} = names;
// 就是把匹配到的 p1 属性赋给冒号后面的变量

```
> 现在你知道:
>
> let {p1, p2} = names;
>
> 本质上是 p1 去匹配对象属性, 然后赋给变量 p1. 那么 p2 也是同理

如果某一个解构出来的值是一个对象, 你可以继续解构下去:

```js
let {
  ps: {a:1,b:2}
} = names;

// 如果想得到 a, b 的值可以:
let { ps:{a,b} } = names;

console.log(a); // 1
console.log(b); // 2
console.log(ps); //报错, 变量未定义

```

可以看到, 对于嵌套解构的情况, 也是允许的. 语法也并不复杂.

你还可以在解构的时候给一个**默认值**:

```js
let names = {
  p1: 'Flowke',
  p2: 'Sal'
}

// 如果 z 在对象里没有, 默认值是 5
// 如果 p1 在对象里没有, 默认值是 Jack
let {z=5, p1='Jack'} = names;

console.log(z); // 5
console.log(p1); // 'Flowke'

```
最后, **数组也是可以解构**的:

```js
let arr = [1,2,3,4];

let [a,b,c] = arr;

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3

```

---

:point_right::point_right:[下一节, 我们看看 ES6 在函数方面的扩展](./4-Function-extend.md)

[回到大纲](../README.md#outline) :point_left::point_left:
