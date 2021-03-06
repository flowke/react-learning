# React 可变气门升程教程 :sunny::sunny::sunny:

原谅我把标题写的这么拗口难读 :scream:. 但是本教程旨在帮助你从一个 react 初学者 变成一个合格的 react 开发者.

如果你是一个尚未接触 react 的前端人员, 并打算在 react 方向有所发展. 那么本教程将会对你有实质性的帮助.  :lollipop::lollipop::lollipop:

## 什么是 React ?

你可以在众多的书籍, 视频和博客教程中能够找到 关于 react 的各种介绍, 有什么样的优势等等这些信息.

但是我并不打算在一开始就长篇大论 React 是什么.

时间宝贵, 你只要知道 React 是**一个帮助你构建界面的库**就好了. 现在的你还不需要了解除此以外更多其他的信息.

这是它的官网: [English](https://reactjs.org/) | [中文](https://doc.react-china.org/) :fries::fries:

## 如何使用本教程 :exclamation::exclamation::exclamation:

如果你是一位初学者:

- 按照课程大纲的指示, 一步一步, 循序渐进.
- 章节中有需要敲代码的地方, 不能偷懒, 不能跳过.
- 你有 99.9% 的可能需要全程打开编辑器, 以便随时调试.
- 记着以上三条, 严格遵守, 做好心理准备.

如果你已经有 react 使用经验:

- 可以把本教程当文档查阅.
- 直接到相应章节弥补自己需要的知识.

我有近两年的 react 实际使用经验, 一个库的语法和 API 学起来是很容易的, 最宝贵的是那些使用上的经验.

一般来说我会在某些地方谈到这些经验以及你需要避免的坑.

大多数的经验很难表达, 并且不经历过很难体会到那种心境, 但我会说出一些处理问题的原则和方式, 这些原则是普适的.

**我有向 react 初学者群体 和 对react 有需求的前端从业人员面授 react 的经验. 带着他们从初学者到使用 redux 写项目.**

教授 react 的经验对我非常宝贵. :gift_heart::gift_heart::gift_heart:

所以我知道你在学习的过程中在哪些地方会遇到困难和疑惑, 在内容的编排与撰写上, 我根据学习者反应进行多次了调整与修订.

即便这样, 你依然可能在学习的过程中遇到某些问题, 你务必相信随着你使用和开发的经验越多, 这些问题都会迎刃而解. 不必在某个时间点纠结太久.

最后要跟你说的是, 本教程不会让你成为一个 react 的大牛. _能够让你成为大牛是你那些无可替代的使用经验 和 碰到各种业务问题时的各种解决方案._

## 调试代码

大多数时候你需要调试代码, 查看代码运行的效果. 这一点非常重要.

你可以使用 [`create-react-app`](create-react-app) 生成项目, 在本机调试.

或者, 使用 codesandbox 在线调试: :point_down::point_down:

 [![Edit new](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/new){:target:"_blank"}

## 学前要求

**以下几点必须具备**
1. 你必须具备 html, css, JavaScript 基础
2. 你必须 ES6 基础, 包括:
    - 声明: let, const
    - 函数扩展
    - 模板字符串
    - spread 与 rest
    - 变量的解构赋值
    - class 相关
    - ES6 模块化语法: import, export
3. CommonJS 模块化语法

ES6相关基础查看阮一峰的教程: [ECMAScript 6 入门](http://es6.ruanyifeng.com/#docs/let)

**以下几点拥有会更好**

1. webpack 与 babel
2. npm 或 yarn

可以到这里查看相应信息:

webpack: [English](https://webpack.js.org/configuration/) | [中文](https://doc.webpack-china.org/)

babel: [English](https://babeljs.io/) | [中文](https://babel.docschina.org/)

npm: [English](https://www.npmjs.com/)

yarn: [中文](https://yarnpkg.com/)

## 提问与建议

直接到本项目提交 [issue](https://github.com/flowke/react-learning/issues)

## 课程大纲 :dog::dog::dog: <a name="outline"/>

**最新动态**

**前置基础**

ES6基本语法相关

1. [变量声明:  let , const](./PreBase/1-var.md)
2. [模板字符串](./PreBase/2-Template-string.md)
3. [变量解构赋值](./PreBase/3-Destruct-var.md)
4. [函数扩展](./PreBase/4-Function-extend.md)
5. [spread 和 rest](./PreBase/5-Spread-rest.md)
6. [class 相关](./PreBase/6-Class.md)

常用数组方法

1. [map()](./PreBase/array-map.md)
2. [filter()](./PreBase/array-filter.md)
3. [every()](./PreBase/array-every.md)
4. [some()](./PreBase/array-some.md)
5. [reduce()](./PreBase/array-reduce.md)

模块化基础

1. [ES6 模块化语法](./PreBase/module-es6.md)
2. [CommonJS 模块化语法](./PreBase/module-commonJS.md)

**React 核心基础**

1. [开始第一次尝试](./Essential/0-HelloWorld.md)
2. [React 运行起来最基本的组成](./Essential/1-EntryPoint.md)
3. [初识 JSX](./Essential/2-JSX.md)
4. [理解 JSX](./Essential/3-JSX-in-deep.md)
5. [JSX 文档详情](./Essential/4-JSX-doc.md) (可选)
6. [组件](./Essential/5-Component.md)
7. [Props](./Essential/6-Props.md)
8. [State](./Essential/7-State.md)
9. [ State 的重要特性](./Essential/8-State-other-features.md)
10. [事件系统](./Essential/9-Event.md)
11. [生命周期](./Essential/10-LifeCycle.md) :exclamation::exclamation::exclamation:
12. [defaultProps](./Essential/11-defaultProps.md)
13. [类型检查](./Essential/12-propTypes.md)
14. [Fragments](./Essential/13-Fragments.md)
15. [Portals](./Essential/14-Portals.md)
16. [错误边界](./Essential/15-ErrorBoundaries.md)
17. [高阶组件](./Essential/16-HOC.md)
18. [Refs](./Essential/17-Refs.md)
19. [ForwardingRefs](./Essential/18-ForwardingRefs.md)


**React 测试**

1. [测试概述](./Testing/1-Test-intro.md)

**React 同构**
