# defaultProps, props 的默认值

这节课开始我们说说轻松的啦.

在定义一个组件的时候, 我们可以规定一些情况: 如果某个 props 是未定义的, 那么你可以给它一个默认值.

我们看看如何给一个组件添加默认属性:

```js

class Greeting extends React.Component{
  render(){

    let {name} = this.props;

    return (
      <p>Hello {name}</p>
    )
  }
}

// 定义默认属性
Greeting.defaultProps = {
  name: 'Customer'
}

ReactDOM.render(
  <div>
    <Greeting name="Joe"/>
    <Greeting />
  </div>,
  document.getElementById('root')
)

```

我们看看渲染结构:

<img src="./img/11-1.png" />

可以看到, 我们只需要在组件名下面挂载一个 `defaultProps` 的属性, 我们使用一个对象, 对象里面的属性值就是对应 `props` 的默认属性值.

> 提示: 函数组件同理


---

:point_right::point_right:[下一节, 我们看看组件的默认 `prop`](./12-propTypes.md)

[回到大纲](../README.md#outline) :point_left::point_left:
