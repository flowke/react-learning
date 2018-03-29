# 函数相关扩展

ES6 在函数方面有了很多的改动, 比如添加了一种新的声明函数的语法: 箭头函数 ; 在传递参数方面也给了更多方便的东西.

我们来一起看看我们需要关注的一些地方, 这些是日常开发过程中比较常用的.

## 箭头函数

#### 基本语法

先来看看它的语法:

```js
(name)=>{
  console.log(`你好, ${name}`);
}
```

这样你就可到了一个箭头函数. ( ) 里面写参数, { } 里面写函数体.

**它是匿名的**:zap:, 所以如果不是在行内使用, 而是在别的地方也用到, 那你需要一个变量来接收它:

```js
let logs = (name)=>{
  console.log(`你好, ${name}`);
}

logs('Sal'); // 打印: 你好, Sal
```

当然, 某些情况它还有一些更简洁的写法, 注意下面代码的注释:

```js

// 如果只有一个参数, 可以不写括号
name=>{
  console.log(`你好, ${name}`);
}

// 可以直接返回值

// 函数返回 a, b 两个参数的和
let add = (a, b)=> a+b;

add(1,2) // 函数返回 3

// 如果想返回对象, 需要加括号, 否则对象会被当成方法体
let rtn = ()=>{a:1, b: 2} ;

rtn(); // 会报错, 语法不对,

let rtnFix = ()=>({a:1,b:2});

rtnFix(); // 函数返回 {a:1,b:2}

```

#### this 指向

  箭头函数的 this 永远会指向函数定义时的上下文环境:

```js
let o = {
  func: function () {

    // logEvg 是一个箭头函数, 它返回 this
    let logEvg = ()=>{
      return this;
    }

    // 当调用 o.func() 后
    console.log(this===logEvg()); // true
    console.log(logEvg()); // o 对象
    console.log(this); // o 对象

  }
}
// 当我们运行 o.func() 后
// 我们知道 o.func 这个函数的 this 执行 o
// 应为是 o 调用了 func
// 查看打印的就过我们会知道
// logEvo 里的 this 也是指向 o,
// 和它所处在的 func 函数的 this 执行一致
o.func();

// ============================

let b = {
  func: function () {

    // logEvg 是一个ES5函数, 它返回 this
    let logEvg = function(){
      return this;
    }

    // 当调用 b.func() 后
    console.log(this===logEvg()); // false
    console.log(logEvg()); // undefined
    console.log(this); // b 对象

  }
}

// logEvg() 本来应该返回 window 对象, 但是在
// 严格模式下, 它是 undefined
b.func();
```

除了 `this` 指向函数定义时所在的上下文环境, 你还要注意以下一些特性:

- 不可以 `new` 它, 它不能被当做构造函数
- 没有 `arguments` 对象

## 默认参数值

现在, 如果函数在运行的时候某个参数没有传递值, 你可以在定义函数的时候给一个默认值:

```js
// 如果给 a传递的值是 undefined, 那么 a 的值是5, b 同理
let fn = (a=5,b=3)=>a+b;

fn(9,9); // 9+9 = 18
fn(2); // 2+3 = 5
fn(); // 5+3 = 8

```

你可以看到, 给函数一个默认参数非常简单, 在 参数列表里写个等于就好了. 如果运行时某个参数没有传递值, 那么默认参数就好起作用.


---

:point_right::point_right:[下一节, 我们看看 ES6 的展开与剩余语法](./5-Spread-rest.md)

[回到大纲](../README.md#outline) :point_left::point_left:
