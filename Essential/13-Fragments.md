# Fragment

在之前, 每一个 `JSX` 片段都需要在最外层有一个元素包含, 或者放在一个数组里.

如:

```js
// 想声明类似这样的 JSX 片段:
<p>1</p>
<p>2</p>
<p>3</p>

// 你需要通过以下方式

<div>
  <p>1</p>
  <p>2</p>
  <p>3</p>
</div>

// 或
// 在数组里还得声明 key
[
  <p key="1">1</p>,
  <p key="2">2</p>,
  <p key="3">3</p>,
]

```

## 使用 Fragment

现在, 要解决上面, 可以使用 React.Fragment, 来包含并列的元素, 它不会被渲染成真实的 DOM 元素:

```js
<React.Fragment>
  <p>1</p>
  <p>2</p>
  <p>3</p>
</React.Fragment>
```

**列表渲染**

列表渲染的时候, 可以给 `React.Fragment` 添加 key 属性, 并且这是目前唯一可以添加的属性, 以后可能会逐步添加其他的属性, 比如事件等等.

## 简洁语法

你可以使用一个更简洁的语法: `<></>` 来做这件事:

```js
<>
  <p>1</p>
  <p>2</p>
  <p>3</p>
</>
```

使用这个语法时,要注意一些问题:

- 不支持属性
- 需要使用 [Babel v7.0.0-beta.31](https://github.com/babel/babel/releases/tag/v7.0.0-beta.31)及以上版本来编译转换.

---

:point_right::point_right:[下一节, Fragments](./14-Portals.md)

[回到大纲](../README.md#outline) :point_left::point_left:
