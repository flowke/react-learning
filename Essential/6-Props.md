# Props

组件之间可以传递一些数据, 这些传递的数据叫做 `Props`.

看看如下代码:

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

function Ment(props) {
  return (
      <div>
        <h2>Hello {props.name}</h2>
        {props.num} people here!
      </div>
  )

}

class Aoi extends React.Component{
  render(){
    return (
      <div>
        <h2>Hello {this.props.name}</h2>
        {this.props.num} people here!
      </div>
    )
  }
}

ReactDOM.render(
  <div>
    <Ment num={9} name="Moli"/>
    <Aoi num={22} name="Joe"/>
  </div>

  , document.getElementById('root')
);
```

现在我们分析一下这段代码.

函数组件 `<Ment/>`, 类式组件 `<Aoi/>`.

在标签上你可以写上一些属性(prop), 接下来, 在组件内部, 你就可以访问这些传递过来的 `props`.

下面我们看看 `props` 在两种组件上的访问方式:

**在函数组件上:** :smiling_imp::smiling_imp::smiling_imp:

```jsx
function Ment(props) {
  return (
      <div>
        <h2>Hello {props.name}</h2>
        {props.num} people here!
      </div>
  )
}
```

我们通过函数的第一个参数可以得到一个 `props` 的对象.

接下来, 我们就可以通过 `props` 对象访问到 标签传递过来的 `prop` 了.

而如何使用这些 `props` , 就由你决定了.

**在类式组件上:** :smiling_imp::smiling_imp::smiling_imp:

```jsx
class Aoi extends React.Component{
  render(){
    return (
      <div>
        <h2>Hello {this.props.name}</h2>
        {this.props.num} people here!
      </div>
    )
  }
}
```

在 render() 方法里, 你需要通过组件的实例: `this` 来访问 props 对象.

访问到 `props`, 使用上就和函数组件一样了.

## props.children

查看如下代码:

```jsx
ReactDOM.render(
  <div>
    <Ment num={9} name="Moli">
      <p>网速太卡了!!</p>
    </Ment>

  </div>

  , document.getElementById('root')
);
```

我们在使用 `Ment` 组件的时候, 我们在标签之间插入了一个  `p` 标签, 但是你会发现 `p` 标签的内容并没有渲染到页面上. :anger::anger:

**事实上, 以下两种写法是等价的:** :star2::star2:

```jsx
<Ment num={9} name="Moli">
  <p>网速太卡了!!</p>
</Ment>

// === 这两种写法等价

<Ment
  num={9}
  name="Moli"
  children={<p>网速太卡了!!</p>}
/>
```

发现了么, 写在组件标签之间的内容本质上只是给组件传递了一个 `children` 属性.

所以, 要想 `p` 标签显示出来, 就得用上它.

比如: 在组件实现上, 你可以这样:

```jsx
function Ment(props) {
  return (
      <div>
        <h2>Hello {props.name}</h2>
        {props.num} people here!
        {props.children}
      </div>
  )
}
```

这样就 OK 啦!

在 :point_right::point_right:[JSX 文档详情](./4-JSX-doc.md#children), 我也提到过 `children`. 可以去看看.


---

## 什么数据可以当成 prop

`props` 接受任何的数据类型:

- 数字
- 字符串
- 函数
- 组件变量
- JSX
- bool
- ......

## 需要注意的事

`props` 是 [immutable](https://zh.wikipedia.org/wiki/%E4%B8%8D%E5%8F%AF%E8%AE%8A%E7%89%A9%E4%BB%B6) 的. 你要保证你对 `props` 只能是**只读不写**.

如果你做如下操作:

```jsx
// 在类组件上
function Ment(props) {

  // 修改props.name 😱😱😱:scream:
  props.name = 'Sal';

  return (
      <div>
        <h2>Hello {props.name}</h2>
        {props.num} people here!
      </div>
  )
}

// 在函数组件上
class Aoi extends React.Component{
  render(){

    // 修改this.props.name 😱😱😱:scream:
    this.props.name = 'Sal';

    return (
      <div>
        <h2>Hello {this.props.name}</h2>
        {this.props.num} people here!
      </div>
    )
  }
}

```

这样的操作是不允许的. 如果运行了这样的代码, 就会给你抛出错误.

原因往下看 :point_down::point_down: :

## props 的实质

在一个 `react` 应用里, 组件之间会相互组合, 相互嵌套. 父子组件之间需要传递数据.

这种传递数据的能力就是 `props` 赋予的.

props 从组件的顶层流向底层, 保证了清晰的数据流. 并且这种数据流总是单向的, 它总是从顶层流向底层.

这种清晰的数据流保证了项目的可维护性.

所以, 如果你的组件嵌套的层级很深, 在不使用 redux 这样的状态管理库之前, 传递多少层都不过分. 虽然会有麻烦, 但却是最佳实践. (当然, 如果嵌套过深, 本身可能你在组件的设计上就出了问题.)

## 小思考

如果现在 `ReactDOM.render()` 代码是这样的:

```jsx
ReactDOM.render(
  <div>
    <Ment num={9} name="Moli"/>
    <Aoi num={22} name="Joe"/>

    <Ment num={9}/>
  </div>

  , document.getElementById('root')
);
```

有一个 `<Ment num={9}/>`, 只传递了 num 属性, 没有 `name` 属性. 那么在页面上的表现是怎样的?

结果是:

**其中一个** `Ment` 组件在渲染的时候, 名字不会显示. 因为 `props.name` 的值是 `undefined`.

这个知识点在: [JSX 文档详情](./4-JSX-doc.md#ess4-ignoreRender) 有提到过, 可以去看看.


---

[回到大纲](../README.md#outline) :point_left::point_left:
