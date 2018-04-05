# ReactDOM

`import ReactDOM from 'react-dom'`;

## 接口总览

- render()
- hydrate()
- unmountComponentAtNode()
- findDOMNode()
- createPortal()

## 接口参考

#### render()

```js
ReactDOM.render(element, container[, callback])
```

把 react element 渲染到容器内.

> 如果已经被渲染过, 再次调用会触发更新, 会进行 DOM 的  diff.

#### hydrate()

```js
ReactDOM.hydrate(element, container[, callback])
```

和 `render()` 一样, 但它是把 `ReactDOMServer` 渲染的HTML内容 插入到容器内.

React将尝试将事件监听器附保留到现有的标记.

React期望服务器和客户端之间渲染的内容是相同的。它可以修补文本内容的差异，但您应该将不匹配视为错误并修复它们。在开发模式中, 在 hydration 期间, React 会警告不匹配。在不匹配的情况下, 并不能保证修补属性之间的差异。这对于性能方面的原因很重要，因为在大多数应用程序中，不匹配是很少见的，因为验证所有标记是极其昂贵的.

如果单个元素的属性或文本内容在服务器和客户端之间不可避免地不同（例如，时间戳），则可以通过向元素添加 `suppressHydrationWarning = {true}` 来消除警告。它只能在一个层级有效，只是个后背方案, 不要过度使用它。除非是文本内容，否则React不会尝试修补它，在下一次更新之前,它可能会保持这种内容不一致。

如果您故意需要在服务器和客户端上渲染不同的东西，则可以执行两遍渲染。就是在 componentDidMount() 之后更新状态. 但注意性能问题.


#### unmountComponentAtNode()

```js
ReactDOM.unmountComponentAtNode(container)
```

从 DOM 元素中移除已挂载的React组件，清除它的事件处理器和 `state。`

如果容器内没有挂载任何组件，这个函数什么都不会干。

有组件被卸载的时候返回 `true` ，没有组件可供卸载时返回 `false`.

#### findDOMNode()

```js
ReactDOM.findDOMNode(component)
```
component: 已被挂载的类组件

#### createPortal()

```js
ReactDOM.createPortal(child, container)
```

创建一个 portal 。portal 可以让 children 渲染到指定的浏览器 DOM 节点里.
