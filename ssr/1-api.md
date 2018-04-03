# 接口文档

`import ReactDOMServer from 'react-dom/server'`;

## 接口概览

服务端和浏览器都能运行的方法:

- renderToString()
- renderToStaticMarkup()

只在服务器支持的方法:

- renderToNodeStream()
- renderToStaticNodeStream()

## 接口详情

#### renderToString()

```js
ReactDOMServer.renderToString(element)
```

将 React 元素渲染为其初始 HTML. 会返回 HTML 字符串. 可以使用它来在服务端生成 HTML 并在首次请求的时候返回标签以对 SEO 友好.

 已经在这个服务端渲染的标签的 node 服务器里调用 [ReactDOM.hydrate()](https://reactjs.org/docs/react-dom.html#hydrate), React 会保留它并且只保留事件回调函数, 允许你有一个很棒的首次加载体验.


#### renderToStaticMarkup()

```js
ReactDOMServer.renderToStaticMarkup(element)
```

和 `renderToString` 很像, 但它不会创建额外 React 自己使用的 DOM 属性, 比如 data-reactroot. 如果你只把 React 当成一个简单的静态页面生成器就会很有用, 移除额外的属性还能节省一些字节大小.

如果你想在客户端使用 React 与标签做一些交互, 就不要用这个方法. 相反, 你应该在 服务端使用 `renderToString`, 在客户端用 `ReactDOM.hydrate()`.
