# 高阶组件
higher order component

具体而言，高阶组件是一个函数, 接收一个组件, 并返回一个组件。

```js
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```


## 约定

#### 1. 不传递无关的数据到 WrappedComponent

```js
render() {
  // Filter out extra props that are specific to this HOC and shouldn't be
  // passed through
  const { extraProp, ...passThroughProps } = this.props;

  // Inject props into the wrapped component. These are usually state values or
  // instance methods.
  const injectedProp = someStateOrInstanceMethod;

  // Pass props to wrapped component
  return (
    <WrappedComponent
      injectedProp={injectedProp}
      {...passThroughProps}
    />
  );
}
```
有助于确保HOC尽可能灵活且可重用。


#### 2. 最大化组合性

并非所有HOC看起来都一样。有时他们只接受一个参数，包装组件：

```js
const NavbarWithRouter = withRouter(Navbar);
```

```js
// React Redux's `connect`
const ConnectedComment = connect(commentSelector, commentActions)(CommentList);
```

#### 3. 将 display name 封装以便于调试

```js
function withSubscription(WrappedComponent) {
  class WithSubscription extends React.Component {/* ... */}
  WithSubscription.displayName = `WithSubscription(${getDisplayName(WrappedComponent)})`;
  return WithSubscription;
}

function getDisplayName(WrappedComponent) {
  return WrappedComponent.displayName || WrappedComponent.name || 'Component';
}
```

## 注意事项

#### 不在 render 里使用 HOCs

```js
render() {
  // A new version of EnhancedComponent is created on every render
  // EnhancedComponent1 !== EnhancedComponent2
  const EnhancedComponent = enhance(MyComponent);
  // That causes the entire subtree to unmount/remount each time!
  return <EnhancedComponent />;
}
```

这会影响 diff 算法性能, 也会丢失状态. 因为组件在 diff 后可能会被卸载.


#### 必须复制静态方法

```js
function enhance(WrappedComponent) {
  class Enhance extends React.Component {/*...*/}
  // Must know exactly which method(s) to copy :(
  Enhance.staticMethod = WrappedComponent.staticMethod;
  return Enhance;
}
```

使用 [hoist-non-react-statics](https://github.com/mridgway/hoist-non-react-statics)可以自动复制.

```js
import hoistNonReactStatic from 'hoist-non-react-statics';
function enhance(WrappedComponent) {
  class Enhance extends React.Component {/*...*/}
  hoistNonReactStatic(Enhance, WrappedComponent);
  return Enhance;
}
```

#### refs 不会传递

通常会把 props 都传递到 wrappedComp , 但是 ref 不是一个真正的 prop, key 也一样. 这些属性是 React 专门处理的.

解决这个问题的方法是使用 React.forwardRef API（在React 16.3中引入）。

---

:point_right::point_right:[下一节, Fragments](./17-Refs.md)

[回到大纲](../README.md#outline) :point_left::point_left:
