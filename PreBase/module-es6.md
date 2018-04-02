# 需要掌握的 ES6 模块化语法

模块化, 也就是文件直接的相互依赖. 一个模块就是一个 js 文件.

一个模块会暴露一些东西, 一个模块也可能会从别的模块引入一些东西.

## export 和 如何引入(import)

一个模块可以通过 `export` 语法来导出一些东西.

一个模块可以有多个 `export` 命令.

比如有一个 `a.js` 文件.

```js
// a.js

let name1 = "Joe",
    name2 = "Mike";

let fileName = 'app.js';

// 直接在变量声明前使用 export
 export let a = 6;

// export 之后接一个花括号, 里面写变量名
export {
  name1,
  name2
}

// 可以在导出的时候, 导出的变量名换成另一个名字, 使用 as
export {
  fileName as appJS,
}

```

现在同一文件夹下有个` b.js` 的文件, 它从 `a.js` 里面引入东西:

```js
// b.js

// from 后面的字符串是 `b.js` 的路径
// import 后面使用一个花括号来取得另一个模块的 export 语法的导出
import {a, name1, name2, appJS } from './b.js'

console.log(a); // 6
console.log(name1); // "Joe"
console.log(name2); // "Mike"
console.log(appJS); // "app.js"

```

可以看到, 在接收另一个模块使用 `export` 语法导出的东西的时候, 引入时, 在 `import` 命令后面写一个花括号 `{}`, 然后在花括号里面写 `export` 时的变量名就可以了.

## export default 和 如何引入(import)

除了使用 `export` 导出东西, 还可以使用 `export default` 导出东西.

`export default` 一个模块只能出现一次.

我们继续以上面的代码举例:

在 `a.js` 里使用 `export default` 导出:
```js
// a.js

let name1 = "Joe",
    name2 = "Mike";

let fileName = 'app.js';

export let a = 6;

export {
  name1,
  name2
}

export {
  fileName as appJS,
}

// 使用 export default
// 后面直接写要导出的值
export default function() {
  console.log('Hello');
}

```

接着, 我们在 `b.js` 里面引入:

```js
// b.js

// 接收 export default 的导出的时候, 不需要写在 花括号内,
// 并且可以写任意指定的名字
import logHello, {a, name1, name2, appJS } from './b.js'

console.log(a); // 6
console.log(name1); // "Joe"
console.log(name2); // "Mike"
console.log(appJS); // "app.js"

logHello(); // Hello

```

引入 `export default` 的导出的时候, 不需要写在 花括号内, 并且变量名自己定.

注意, 以下这些 使用 `export default` 的语法是错的:

```js
------------ 情况一 ---------------
// 错
export default let a = 5;

// 对
export default 5;

---------- 情况二 --------------
let a = 6, b=8;

// 这个时候, 花括号是对象,
// 和 export 后的花括号 {} 不是一回事
// 对
export default {
  a,
  b
};

如果此时在别的模块引入:

import obj from './b.js';

console.log(obj); // {a: 6, b:8}

```

---

:point_right::point_right:[下一节, 我们看看 commonJS 的模块化](./module-commonJS.md)

[回到大纲](../README.md#outline) :point_left::point_left:
