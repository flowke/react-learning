# Class

class, 也就是类. 类是都某个实物的抽象, 比如 人, 就可以当成一个类. 而每一个具体的人, 就是人这个类的一个实例.

## 基本语法

在 ES6 之前, 如果我们响应使用 `new` 操作得到一个对象, 那么我们需要先 声明一个函数, 然后去 `new` 它, 我们也把这个函数叫做构造函数. 我们可能还会在原型链上挂载些其他的东西.

像这样:

```js
// 构造函数
function People(name) {
  this.name = name;
}

// 方法
People.prototype.sing = function () {
  console.log(`${this.name} 在唱歌`);
};

let mask = new People('Mask');

mask.sing(); // Mask 在唱歌

```

而现在, 你使用 `class` 来更简洁的声明类:

```js
// 使用 class 声明一个类
class People{
  // 构造函数
  constructor(name){
    this.name = name;
  }

  // 方法
  sing(){
    console.log(`${this.name} 在唱歌`);
  }

}

let Joe = new People('Joe');

Joe.sing(); // Joe 在唱歌

```

相对 ES5, 现在我们很明确的知道, `People` 是一个类, `constructor()` 是它的构造函数.

`sing()` 是这个类的方法.

所有的方法都写在类的花括号内, 清晰明了.

> 提示: `constructor()` 不是必须要写的.

## 继承

在 ES5 里面, 我们的继承需要通过对原型链进行操作. 在 ES6 里面, 类之间的继承只需要一个非常简洁的语法:  `extend`:

```js
class People{
  // 构造函数
  constructor(name){
    this.name = name;
  }

  // 方法
  sing(){
    console.log(`${this.name} 在唱歌`);
  }
}

// 继承 People
class StrongMan extends People{

  constructor(name, eyesNum){
    // 调用父类构造函数
    // 可以传递参数
    super(name);
    this.eyes = eyesNum;
  }

  fly(){
    console.log(`${this.name} 飞上了天`);
  }

}


let men = new StrongMan('Jack', 6);

console.log( men.name ); // Jack
console.log(men.eyes); // 6

men.sing(); // Jack 在唱歌
men.fly(); // Jack 飞上了天

```

可以看到, 通过 `extends` 关键字, 就可以继承另外一个类的属性和方法.

> 注意:
>
> 当继承了另外一个类之后, 如果你写了 `constructor()`, 那么你必须先 调用 super();

## 成员方法的 this

## 静态方法

---

[回到大纲](../README.md#outline) :point_left::point_left:
