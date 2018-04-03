# 变量声明

ES6 新增了新的变量声明命令: `let` 和 `const`.

## let

声明变量的语法我们很熟悉:

```js
var a = 5;

=> // 你也可以使用 let 声明

let b = 6;
```

不过使用 let 声明变量后, 有了一些新的特性, 你要特别注意以下两点:

**1. 不能重复声明**

比如:

```js
let a;
let a;

// 会报错, 重复声明了 a 变量
```

**2. 有块级作用域**

可以把一个 `{}` 当成一个块, 比如, `{}`, 函数, `if`, `for` 的 {}...

```js
for(let i=0; i<10; i++){
  setTimeout(function() {
    console.log(i); //依次打印 0-9
  })
}

// 注意, 如果此时打印 i
console.log(i) // i 是 undefined

// ==================

for(var j=0; j<10; j++){
  setTimeout(function() {
    console.log(j); //每次打印 10
  })
}

// 注意, 如果此时打印 j
console.log(j) // j 是 10

```

## const

const 用来声明一个常量, 它期望对它是只读的:

```js
const NAME = "Bob"; // 你必须对它初始化

NAME = "Sal"; // 修改变量的值会报错
```

它也符合 `let` 声明时的一些特性, 比如不能 重复声明, 有块级作用域等等...

但是声明对象时需要注意:

```js
const list = {a: 1, b: 2} ;

// 这样操作对象的内部是可以成功的,
list.a = 5;

console.log(list) // list变成{a: 5, b: 2}

```

## 总结

当然变量声明有更多其他的特性, 但记住这几点, 并且在写代码的过程中尽量遵照代码规范来实践. 那么便可以符合大多数场景.

---

:point_right::point_right:[下一节, 我们看看模板字符串](./2-Template-string.md)

[回到大纲](../README.md#outline) :point_left::point_left:
