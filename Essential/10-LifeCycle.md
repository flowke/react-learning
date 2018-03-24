# 组件生命周期

[![Edit new](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/new)

在本地或线上调试生命周期函数, 看看他们在什么时候会执行.

---

现在我们应该知道一件事情, 有了 组件 和 props, 我们就可以把一个页面拆成一个个小组件.

有了 内部状态, 我们就可以让组件在某些时候做出一些变化.

我们的页面就是通过一个个小的组件, 组合成一个大的组件, 一份份小的 jsx, 组合成一份大的 jsx.

最后交给 `ReactDOM.render()`, 通过 DOM 操作, 把 Virtual DOM 渲染成浏览器真实的 DOM.

## 理解生命周期

**挂载阶段** :fire:

组件也是有生命的, 如果一个组件被渲染到了页面, 那么这个组件的生命便开始了.

也就是 Virtual DOM 变成真实 DOM的这个过程. 组件生命的开始也叫组件的挂载.

上代码:

```js
import React from 'react';
import ReactDOM from 'react-dom';

class A extends React.Component {

  render(){
    return (
      <div>
        <p> 数字: 999 </p>
        <button>click once</button>
      </div>
    )
  }
}

ReactDOM.render(
  <div>
    <A/>
  </div>
  , document.getElementById('root'));

```

`<A/>` 开始的时候还只是一份虚拟dom, 可一旦把它渲染到浏览器, 我们便说这个组件被挂载了.

**更新阶段** :fire:

一个被挂载的组件, 某些时候可能会变化, 也就是被更新:

```js
class A extends React.Component {

  constructor(props){
    super(props);

    this.state = {
      num: Math.random().toString().slice(2, 8)
    };
  }

  changeNum=()=>{
    this.setState({
      num: Math.random().toString().slice(2, 8)
    });
  }

  render(){

    let {num} = this.state;

    return (
      <div>
        <p> 数字: {num} </p>
        <button
          onClick={this.changeNum}
        >click once</button>
      </div>
    )
  }
}
```
我们改造下 `A` 组件. 每次点击按钮, 数字就会改变. 也就是这个组件会变化, 这个时候, 我们就说这个组件被更新了.

**卸载阶段** :fire:
当一个已经被挂载的组件从页面删除掉, 那么这个组件实例的生命就结束了. 我们就说这个组件被卸载了.

我们改一下上面的代码:

```js
class B extends React.Component{

  render(){
    return (
      <div>我是组件 B</div>
    )
  }
}

class A extends React.Component {

  constructor(props){
    super(props);

    this.state = {
      isShowB: true
    };
  }

  changeNum=()=>{
    this.setState({
      isShowB: !this.state.isShowB
    });
  }

  render(){

    let {isShowB} = this.state;

    return (
      <div>
        {
          isShowB ? (
            <B/>
          ) : (
            <p>我不是B</p>
          )
        }
        <button
          onClick={this.changeNum}
        >click once</button>
      </div>
    )
  }
}
```

在第一次点击按钮之前, 有一个 `B` 组件的实例被挂载到页面, 而点击按钮之后, 这个 `B` 组件实例就会被卸载掉.

重复的点击按钮, 就会不断有新的 `B` 组件实例被挂载, 然后被卸载.

## 生命周期函数

无论是组件挂载, 更新, 还是卸载. 都是一个瞬间的事情. 但是在这个瞬间执行之前和之后, React 会调用一些函数, 我们把这些函数叫做**生命周期函数**.

#### Mounting(挂载) 阶段

- `constructor( props )` :metal::metal:
  - 组件挂载时首先执行
  - 在这里可以:
    - 初始化 state
    - 给事件函数绑定 `this`
- componentWillMount() :metal::metal:
  - 组件将要挂载时执行
- render() :metal::metal:
  - 返回此刻组件的 JSX 结构
- componentDidMount() :metal::metal:
  - 组件挂载完成后执行
  - 在这里可以:
    - 开启定时器
    - 发起请求
    - 访问真实的 DOM 元素

这些函数是组件挂载阶段执行的函数.

因为一个组件实例只能被出生一次, 也就是一生只能被挂载一次, 所以这些函数在这个组件实例的生命周期中只会执行一次.

当然, `render()` 函数是个例外. 在挂载阶段它需要返回 `JSX` 结构, 在更新阶段, 它也需要返回新的 `JSX` 结构. 所以 `render()` 可能会执行多次.

#### Updateing(更新) 阶段

- componentWillReceiveProps( nextProps ) :metal::metal:
  - 父组件更新的时候执行
- shouldComponentUpdate( nextProps, nextState ) :metal::metal:
  - 返回 bool 值, 默认返回 `true`
  - 如果返回 false, 当前组件不会更新, 之后的生命周期函数不执行
  - 性能优化的主要手段之一
- componentWillUpdate( nextProps, nextState ) :metal::metal:
  - 组件将要更新时执行
- render() :metal::metal:
- componentDidUpdate( prevProps, prevState ) :metal::metal:
  - 组件更新之后执行

#### Unmounting(卸载) 阶段

- componentWillUnmount() :metal::metal:
  - 组件将要卸载的时候执行
    - 可以在这里:
      - 移除事件绑定
      - 清空定时器
      - 取消请求

## Error Handling :zap::zap:

很长一段时间, 组件的生命周期就是 挂载, 更新, 卸载三个阶段.

在更新到了 `16.0.0` 之后, 新增了一个 **错误处理的阶段**.

新增了一个函数:

- componentDidCatch( error, info )

当子组件的生命周期函数(包括 `render()`, `constructor()`和其他生命周期函数)里面抛出了错误, 那么这个函数就会执行.

> 注意, 在此组件之下的子组件发生错误的时候才会执行, 组件自身的生命周期函数发生错误不会捕获到.

## 关于生命周期函数

在上面我们初步了解了组件的生命周期函数, 并且我在每个生命周期函数的下面做了简单的说明.

现在我们只要知道生命周期函数会在什么之后执行就可以了.

有些生命周期会频繁使用, 而有些则会很少用到.

关于如何生命周期函数在什么时候用这种问题, 这需要随着时间, 随着你解决各种业务需求之后, 会慢慢越来越有体会.

现在, 你还不需要太关心这方面的问题.

---

<!-- :point_right::point_right:[下一节, 我们看看组件的生命周期](./10-LifeCycle.md) -->

[回到大纲](../README.md#outline) :point_left::point_left:
