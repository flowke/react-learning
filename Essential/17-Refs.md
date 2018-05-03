# Refs

通过 ref 你可以拿到真实的 DOM 元素或组件实例.

以下情况你可能会用到:

- 焦点, 文本选择, 媒体播放控制
- 触发命令式动画
- 与第三方库集成

> 16.3 以后更新使用 React.createRef() API . 之前的版本推荐使用回调.


## 创建 Refs

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```

## 访问 refs

```js
const node = this.myRef.current;
```

ref的值根据节点的类型而有所不同：

- 用于 HTML element的时候, 得到真实的 DOM 元素.
- 自定义组件节点时, 得到组件实例
- 函数式组件上没有实例, 所以不应该使用. 会打印错误.(回调的方式得到 undefined, createRef API 的 current 会是 null)
