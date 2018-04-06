# Generator

`generator` 会返回一个 迭代器对象.

声明它的时候, `function后` 加个\*: **function**

```js
function* fn() {
  yield 4;
  yield 8;
  return 3;
}

let it = fn();

console.log(it.next()); //{value: 4, done: false}
console.log(it.next()); //{value: 8, done: false}
console.log(it.next()); //{value: 3, done: true}
console.log(it.next()); //{value: undefined, done: true}

```

## yield 表达式

**point :clap:**

遇到 `yield`, 才开始对后面的表达式求值, 并停下来.

到了 `return` 语句, 遍历到的对象 `value` 是 `return` 的东西, `done` 是 `true`. 没有   return, `value` 是 `undefined`, 值是 `done`.

**point :clap:**

`yield` 表达式如果用在另一个表达式之中，必须放在圆括号里面。

```js

function* fn() {
  yield 4;
  yield 8;
  // 第三次next的使用 返回的是 {value: 998, done: false}
  // 第四次 next 才会 打印 helloundefined
  console.log('hello' + (yield 988));
  return 3;
}
```

> 注意上面的注释

**point :clap:**

yield表达式用作函数参数或放在赋值表达式的右边，可以不加括号。

```js
function* demo() {
  foo(yield 'a', yield 'b');
  let input = yield;
}
```

## next 方法参数

`next()` 的参数会当成**上一个**:exclamation::exclamation: `yield` 表达式的返回值, 否则是 `undefined`.

> 上一个意味着第一次调用 next() 传入参数是无效的.

## for...of 循环

```js
function* gen() {
  yield 1;
  yield 2;
  return 3;
}

for (let val of gen()) {
  console.log(val);
}
// 1 2
```
一旦next方法的返回对象的done属性为true，for...of循环就会中止，且不包含该返回对象.

## Generator.prototype.return()

终结遍历.

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen();

g.next()        // { value: 1, done: false }
g.return('foo') // { value: "foo", done: true }
g.next()        // { value: undefined, done: true }
```

如果 Generator 函数内部有try...finally代码块，那么return方法会推迟到finally代码块执行完再执行。

```js
function* numbers () {
  yield 1;
  try {
    yield 2;
    yield 3;
  } finally {
    yield 4;
    yield 5;
  }
  yield 6;
}
var g = numbers();
g.next() // { value: 1, done: false }
g.next() // { value: 2, done: false }
g.return(7) // { value: 4, done: false }
g.next() // { value: 5, done: false }
g.next() // { value: 7, done: true }
```

## yield* 表达式

`yield*`表达式，用来在一个 `Generator` 函数里面执行另一个 `Generator` 函数.

```js
function* bar() {
  yield 'x';
  yield* foo();
  yield 'y';
}

// 等同于
function* bar() {
  yield 'x';
  yield 'a';
  yield 'b';
  yield 'y';
}

// 等同于
function* bar() {
  yield 'x';
  for (let v of foo()) {
    yield v;
  }
  yield 'y';
}

for (let v of bar()){
  console.log(v);
}
// "x"
// "a"
// "b"
// "y"
```
yield*后面的 Generator 函数（没有return语句时），等同于在 Generator 函数内部，部署一个for...of循环。

```js
function* concat(iter1, iter2) {
  yield* iter1;
  yield* iter2;
}

// 等同于

function* concat(iter1, iter2) {
  for (var value of iter1) {
    yield value;
  }
  for (var value of iter2) {
    yield value;
  }
}

```
在有return语句时，则需要用`var value = yield* iterator`的形式获取return语句的值。

任何数据结构只要有 Iterator 接口，就可以被yield*遍历。

```js
function* gen(){
  yield* ["a", "b", "c"];
}

gen().next() // { value:"a", done:false }
```
