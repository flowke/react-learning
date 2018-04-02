# 需要掌握的 commonJS 模块化语法

commonJS 的模块化语法相比 ES6, 语法更加简单. nodeJS 就是使用的这一套模块化规范.


## module.exports (导出)

一个文件的导出, 只要把要导出的值赋给 module.exports 就行了.

一个文件只需要一个 module.exports.

```js
// a.js

let a = 6;

module.exports = a ;

```
导出就是这么简单. 就是把一个变量, 或一个值赋给 `module.exports` 就行.

## require (引入)

直接看引入语法:

```js
// b.js

const num = require('./a.js');

console.log(num); //6

```

`require('./a.js')` 在 `require` 函数里面传一个参数: 模块路径, 它会返回一个值, 这个值就是另一个模块 `module.exports` 的值.

---

[回到大纲](../README.md#outline) :point_left::point_left:
