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

## 暴露 DOM 元素给父组件的最佳实践

如果您使用React 16.3或更高版本，推荐使用ref forwarding。Ref转发允许组件选择将任何子组件的ref作为自己的。

如果您使用React 16.2或更低版本，或者如果您需要比ref forwarding提供的更多灵活性，则可以使用[这种替代方法](https://gist.github.com/gaearon/1a018a023347fe1c2476073330cc5509)，并明确传递ref作为不同名称的prop。

## Callback Refs

callback refs 这种可以在设置和移除ref时有更多细粒度的控制.

```js
<input ref={el=>this.inputRef=el} />
```
ref 接受一个回调函数, 回调函数会把 input 元素当参数.

ref 回调会在组件挂载时调用, 并传入DOM. 卸载时候会调用并传入 null. 会在 didMount 和 didUpdate 之前调用.

```js
function CustomTextInput(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}

class Parent extends React.Component {
  render() {
    return (
      <CustomTextInput
        inputRef={el => this.inputElement = el}
      />
    );
  }
}
```

**注意事项**
如何 ref 回调是一个行内函数, 在更新时期会调用两次, 第一次是 null, 接着才是 DOM. 因为新的函数实例, 在每次渲染的时候, React 需要先清除旧的 ref, 然后设置一个新的. 大多数时候不用担心, 想修正的话可以传一个固定的函数.



## Legacy API: String Refs

已经不被推荐. 会出现些[问题](https://github.com/facebook/react/pull/8333#issuecomment-271648615):

- 它要求React跟踪当前的渲染组件（因为它不能猜到 this）。这使得React有点慢。
- 它并不像大多数人所期望的那样使用 `“render回调”`模式（例如`<DataGrid renderRow = {this.renderRow} />`），因为ref会因为上述原因而被放置在DataGrid上。
- 它不是可组合的，即如果一个library对被传递下来的child 放置了ref，用户就不能再放置另一个ref（例如[＃8734](https://github.com/facebook/react/issues/8734)）。回调方式是完美的可组合。

---

:point_right::point_right:[下一节, Fragments](./18-ForwardingRefs.md)

[回到大纲](../README.md#outline) :point_left::point_left:
