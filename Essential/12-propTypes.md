# 数据验证: propTypes

在传递 `prop` 的时候, 你可以验证传递下来的数据类型.

要使用数据验证, 需要先安装一个 `prop-types` 的库.

下面是一个典型例子:

```js
// 先引入 prop-types 这个库
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    let {name} = this.props;
    return (
      <h1>Hello, {name}</h1>
    );
  }
}

// 声明数据验证规则
Greeting.propTypes = {
  name: PropTypes.string
};
```

你可以通过 `PropTypes.string` 来规定, name 这个 prop 只能接受 字符串类型.

如果出现了别的数据类型, 就会出现警告.

> 注意: 即便数据验证不通过, 也不意味着程序不能运行. 仅仅只是警告.

> 注意: 只在开发阶段使用 PropTypes 验证. 否则会有性能问题. 在生产时最后移除验证相关代码, 可以借助 [Babel React Optimize](https://github.com/jamiebuilds/babel-react-optimize) 这类工具来自动化移除代码.

---

## 更多的验证规则

除了可以验证字符串, PropTypes 还可以验证更多的数据类型和更多的验证规则.

我们来看看下面列出的相关规则:

```js
PropTypes.array // 数组
PropTypes.bool // true or false
PropTypes.func // 函数
PropTypes.number // 数字
PropTypes.object // 对象
PropTypes.string // 字符串
PropTypes.symbol // symbol

// 可被渲染的东西: 数字, 字符串, React element(可理解成JSX), 数组(元素可被渲染), null, undefined, bool
PropTypes.node

// React element
PropTypes.element

// 某个类的实例
PropTypes.instanceOf(Message)

// 某些值中的一个
PropTypes.oneOf(['News', 'Photos'])

// 某些类型之一
PropTypes.oneOfType([
  PropTypes.string,
  PropTypes.number,
  PropTypes.instanceOf(Message)
])

// 一个数组, 元素为指定的类型
PropTypes.arrayOf(PropTypes.number)

// 一个对象, 属性值为指定类型
PropTypes.objectOf(PropTypes.number)

// 具有某些属性的对象, 属性值指定了类型
PropTypes.shape({
  color: PropTypes.string,
  fontSize: PropTypes.number
})

// 在后面加上 isRequired 后表示必须传递值
PropTypes.func.isRequired
```

## 限制 children 有一个最外层标签包含

```js
import PropTypes from 'prop-types';

function Met({children}) {
  return (
    <div>
      {children}
    </div>
  )
}

Met.propTypes = {
  children: PropTypes.element.isRequired
}

// ----------------------------------
// 使用时

// 不可以
<Met>
  <p>a</p>
  <p>a</p>
</Met>

// 可以
<Met>
  <div>
    <p>a</p>
    <p>a</p>
  </div>
</Met>

```

---

> 注意: 在 defaultProps 定义的默认属性也会参与数据验证.
