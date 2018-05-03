# Forwarding Refs

Ref forwarding 是一种自动传递一个 ref 给子组件的技术. 对大多数应用来说是不必要的. 然而, 在某些情况, 特别是可重用组件库特别有用.

## 转发 refs 到 DOM 组件

```js
function FancyButton(props) {
  return (
    <button className="FancyButton">
      {props.children}
    </button>
  );
}
```

React组件隐藏其实现细节，包括它们的渲染输出。使用FancyButton的其他组件通常不需要获取对内部按钮DOM元素的引用。这很好，因为它可以防止组件过分依赖彼此的DOM结构。

虽然这样的封装对于像FeedStory或Comment这样的应用程序级组件来说是可取的，但对于像FancyButton或MyTextInput这样的高度可重用的“叶子”组件来说，这可能不方便。这些组件倾向于以类似于常规DOM按钮和输入的方式在整个应用程序中使用，并且访问它们的DOM节点可能不可避免地用于管理焦点，选择或动画。
