# State 的重要特性

本节的内容说的比较抽象. 你需要使用代码调试来理解.

 [![Edit new](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/new)

## State 会合并更新

比如你的状态是这样的:

```js
this.state= {
  c1: 0,
  c2: 0
};
```

你可以这样去只更新其中的一部分:

```js

this.setState({
  c1: 5,
});

this.setState({
  c2: 8,
});
```

## state 通常是异步更新

如果现在 `c1` 的值是 0, 然后你更新:

```js
// 现在 c1 = 0

this.setState({
  c1: 2
});

console.log(this.state.c1) // 打印 0

```
这个时候打印的结果是 `0`. 原因是调用 `this.setState()` 后, `c1` 的值**不会立即发生更新**.

## 在异步执行的函数里面, state 会同步更新

查看如下代码:

```js
// 现在 c1 = 0

setTimeout(()=>{
  this.setState({
    c1: 2
  });

  console.log(this.state.c1) // 打印 2
})
```
这个时候结果打印 `2`, 如果 `this.setState()` 在一个异步函数里面调用, 那么 `state` 会立即更新.

以下的函数同样是这种情况:

- Promise 的回调函数
- ajax 响应后的回调函数

**只要是异步执行的函数, 就适用这种情况.**


## this.setState() API

setState() 第一个参数可以传入一个对象, 这种使用方式我们已经知道.

第一个参数还可以传入一个函数:

```js
this.setState((preState, props)=>{
  return {
    c1: preState.c1 + 1
  }
});
```

`preState` 是之前的 `state`

`props` 是组件的 `props`

函数返回的就是要更新的组件状态.

再看看如下代码:


```js
// c1 此时是 0

this.setState((preState, props)=>{
  console.log(preState.c1); // 打印 0
  return {
    c1: 2
  }
});

console.log(this.state.c1); // 打印 0

this.setState((preState, props)=>{
  console.log(preState.c1); // 打印 2
  return {
    c1: 5
  }
});

console.log(this.state.c1); // 打印 0

```

仔细查看这几次打印, state 异步更新的情况没有变.

但 `preState` 的值是前一次 `setState()` 调用之后, 得到的 `State`;

**第二个参数**

setState() 第二个参数是一个可选的毁掉函数, 当组件更新完成之后, 会调用.

## state 的更新只是浅层合并

如果这是现在 `state` 的情况:

```js
this.state = {
  c1: 0,
  c2: {a:1, b: 2}
}
```

现在你这样更新:

```js
this.setState({
  c2: {a: 40}
})
```

这个时候, 最终的 `state` 会变成这样:

```js
this.state = {
  c1: 0,
  c2: {a:40}
}
```

`c2` 的 `b` 属性不见了. 因为整个对象都会换掉了.

`setState()` 之后进行 1 个层级的浅层合并.

---

:point_right::point_right:[下一节, 我们看看在 React 中使用事件](./9-Event.md)

[回到大纲](../README.md#outline) :point_left::point_left:
