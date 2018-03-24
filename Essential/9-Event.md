# 事件系统

 [![Edit new](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/new)

---

现在我们依然使用之前计数器的代码:

```js
import React from 'react';
import ReactDOM from 'react-dom';

class Counter extends React.Component{

  constructor(props){
    super(props);
    this.state= {
      count: 0,
    };
  }

  render(){
    let { count } = this.state;

    return (
      <div>
        <p>目前计数: {count}</p>
        <button
          onClick={()=>{
            this.setState({
              count: count +1
            })
          }}
        >计数 +1</button>
      </div>
    )
  }
}

ReactDOM.render(
  <div>
    <Counter/>
  </div>

  , document.getElementById('root')
);
```

添加事件非常简单, 比如在 `button` 这里:

```jsx
<button
  onClick={()=>{
    this.setState({
      count: count +1
    })
  }}
>计数 +1</button>
```

我们添加了一个点击事件.

**我们已经知道了其中两个特性:**

- 事件名要驼峰写法, 不是小写
- 事件接收一个回调函数

## 合成事件对象

在事件的回调函数里, `react` 提供了一个事件对象作为参数:

```jsx
<button
  onClick={(event)=>{
    this.setState({
      count: count +1
    })
  }}
>计数 +1</button>
```

`event` 参数是 `react` 提供的一个事件对象, 我们可以从里面得到一些事件相关的信息和操作:


```js
boolean bubbles
boolean cancelable
DOMEventTarget currentTarget
boolean defaultPrevented
number eventPhase
boolean isTrusted
DOMEvent nativeEvent // 原生的浏览器事件对象
void preventDefault() // 阻止默认行为
boolean isDefaultPrevented()
void stopPropagation() // 阻止事件传播(冒泡)
boolean isPropagationStopped()
DOMEventTarget target // 发生事件的真实 dom 原生
number timeStamp
string type
```
虽然不同的事件, (比如鼠标事件和键盘事件), 从事件对象里得到的信息有所不同, 但是以上信息是所有事件对象共有的.

上面我写了注释的几个属性可能经常用到.

比如, 如果你想阻止冒泡和默认行为, 可以这样:

```js
<button
  onClick={(e)=>{
    e.stopPropagation();
    e.preventDefault();
    this.setState({
      count: count +1
    })
  }}
>计数 +1</button>
```

## React 支持的事件

React 对事件进行了标准化, 意思是你不需要处理兼容的问题.

对于这一部分的内容, 文档其实已经写得非常清晰和明了.

你可以到文档去查看一下相应的内容, 看看 react 支持什么样的事件, 以及不同的事件提供了什么特别的事件对象属性:

**React 支持的事件:**
[English](https://reactjs.org/docs/events.html#supported-events) |
[中文](https://doc.react-china.org/docs/events.html#%E6%94%AF%E6%8C%81%E7%9A%84%E4%BA%8B%E4%BB%B6)  :point_left::point_left::point_left:

## 事件中 this 指向 :exclamation::exclamation::exclamation::boom::boom:

在上述代码中:

```js
<button
  onClick={(e)=>{
    e.stopPropagation();
    e.preventDefault();

    this.setState({
      count: count +1
    })
  }}
  onMouseDown={this.a}
>计数 +1</button>
```

事件中的 `this` 指向组件的实例, 所以拥有 `setState` 方法.

原因是, 我们给了事件一个行内的箭头函数, 这个时候, 箭头函数内的 `this` 指向了 `render()` 方法的 `this`, 而 `render()` 方法是组件实例调用的, 于是, 箭头函数的 `this` 是组件实例.

但大多时候, 我们是这样组织事件回调函数代码的:

```js
class Counter extends React.Component{

  constructor(props){
    super(props);
    this.state= {
      count: 0,
    };
  }

  buttonHandler(){
    console.log(this); // undefined

    // this 是 undefined, 所以会报错
    let {count} = this.state;

    this.setState({
      count: count +1
    });
  }

  render(){
    let { count } = this.state;

    return (
      <div>
        <p>目前计数: {count}</p>
        <button
          onClick={this.buttonHandler}
        >计数 +1</button>
      </div>
    )
  }
}
```

我们给类添加了一个 `buttonHandler()` 方法, 并且把这个方法当做按钮点击事件的回调函数.

但是一点击就会报错, 原因是 事件处理函数的 `this` 变成了 `undefined`, 没有 `state` 属性, 更没有 `setState()` 接口.

**你有 3 种办法来修正这个问题** :cherry_blossom::cherry_blossom::cherry_blossom:

* 在构造函数初始绑定 this: :star:

```js
constructor(props){
  super(props);
  this.state= {
    count: 0,
  };
  this.buttonHandler = this.buttonHandler.bind(this);
}
```

* 属性初始化器语法: :star:

```js
buttonHandler=(ev)=>{
  console.log(this); // undefined

  // this 是 undefined, 所以会报错
  let {count} = this.state;

  this.setState({
    count: count +1
  });
}
```

也就是在给类添加方法的时候, 这样去添加.

但是要注意一点, 这是一个未被标准化的语法, 如果你是自己搭建运行环境, 你需要使用 babel 的插件 [babel-plugin-transform-class-properties](https://babel.docschina.org/docs/plugins/transform-class-properties/) 来进行转化.

* 行内绑定 this :star:

```js
<button
  onClick={this.buttonHandler.bind(this)}
>计数 +1</button>
```

行内绑定需要留意性能问题, 因为使用 bind 总会生成一个新函数. Virtual DOM 在进行比较的时候, 会认为两个函数不一样, 从而进行了不必要的 DOM 更新.

性能部分我们会在高级部分讲到, 这里先不担心.

---

:point_right::point_right:[下一节, 我们看看组件的生命周期](./10-LifeCycle.md)

[回到大纲](../README.md#outline) :point_left::point_left:
