# JSX 文档详情

_这一篇的内容可以在学完基础部分后随时查阅, 初学者可以暂时先跳过._ :rocket::rocket::rocket:

我们之前已经说过一些和 `JSX` 相关的特性:

- `jsx` 可以嵌入表达式
- `jsx` 本身可以当做表达式
- `jsx` 之间可以相互嵌套
- 每一份声明的 `jsx` 要有一个闭合标签包含
- 关键字属性需要换种形式: `class => className`
- 属性需要驼峰写法
- 声明 `jsx` 的地方, 需要 `React` 在作用域内

另外一些小特性你也需要注意:

- 所有的标签, 只要里面没有内容, 都可以自闭和. 如: `<div/>`
- 自闭和标签结尾处一定要 `/>`.

---

以下内容来自文档, 我进行了一些简化:
你可以原版查看: [JSX in deep](https://reactjs.org/docs/jsx-in-depth.html) | [深入 JSX](https://doc.react-china.org/docs/jsx-in-depth.html)

## React 元素类型

#### 内置组件首字母小写

比如: `<div/>`, `<span/>`. :speak_no_evil:

#### 自定义组件首字母大写

比如: `<Foo/>`. :speak_no_evil:

```jsx
<Foo/>
```

#### 点表示法

```jsx
  <Layout.Content>
  </Layout.Content>
```

#### 标签名不能是表达式
```jsx
// 你不能这样
<components[props.storyType] story={props.story} />

// 可以这样
const SpecificStory = components[props.storyType];

<SpecificStory story={props.story} />;
```
---
## 属性

#### 属性中使用表达式

```jsx
<MyComponent foo={1 + 2 + 3 + 4} />
```

#### 字符串字面量
以下是等价的:
```jsx
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

字符串常量不会被转义, 以下会相等:

```jsx
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

表达式的字符串会被转义, 以下**不**相等: :smiling_imp::smiling_imp:
```jsx
<MyComponent message='&lt;3' />

<MyComponent message={'&lt;3'} />
```

#### 默认值为 True :balloon::balloon:

```jsx
<MyTextBox autocomplete />
// === 这两种表示等价
<MyTextBox autocomplete={true} />
```

#### 属性的展开 :balloon::balloon:

以下会等价

```jsx
<Greeting firstName="Ben" lastName="Hector" />;
}
//===

const props = {firstName: 'Ben', lastName: 'Hector'};

<Greeting {...props} />;

```
---

## <a name="children"> Children

标签之间的内容 就是 `children`, 自定义标签通过 `props.children` 来访问 `children`.

:pill::pill::pill:
空行, 开始 和 结尾的空格. 会被移除.

标签临近的新行, 字符串内部换行被压缩成一个空格:

以下等价:

```jsx
<div>Hello World</div>

// 临近标签处的换行和空格被移除
<div>
  Hello World
</div>

// 字符串内换行变成一个空格
<div>
  Hello
  World
</div>

<div>

  Hello World
</div>
```

:pill::pill::pill: :exclamation::exclamation::exclamation:

**没有闭合标签包含的元素需要在数组里**,
```jsx
[
  // 不要忘记 key :)
  <li key="A">First item</li>,
  <li key="B">Second item</li>,
  <li key="C">Third item</li>,
];
```

#### 关于children需要注意的 :evergreen_tree::evergreen_tree::evergreen_tree::evergreen_tree::evergreen_tree:
自定义组件的 `children` 可以是任何数据类型, 你通过 `props.children` 都可以访问到.

啰嗦一句, 因为 `children` 只是一个普普通通的属性, 所以你可以传任何东西, 比如: 函数. 这个时候你可以在组件内运行这个函数, 做些别的事情.

所以, 你不一定非得是去渲染 `children`, 也不是所有的东西都是能渲染的. 往下看: :point_down::point_down:

## 能被渲染的东西

不是所有的东西都会被渲染, 仅有以下东西会被渲染:

- React element
- 字符串
- 数字
- 元素是 React node 的数组

**布尔值、Null 和 Undefined 被忽略** <a name="ess4-ignoreRender">

也就是说, 如果 `JSX` 里面, 标签之间的表达式返回了以上数据类型, 不会被渲染到页面.

如果要渲染, 先进行字符串转换, 如:

```jsx
<div> {String(true)} </div>
```

要注意一点是:

```jsx
// 此表达式返回 0, 0会被渲染
{0 && 'abc'}
```

---

[回到大纲](../README.md#outline) :point_left::point_left:
