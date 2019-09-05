## JavaScript基础

### 一 JS 支持哪些数据类型
Undefind

Null

String

Number

Boolean

Symbol

Object

```js
// Symbol类型的使用和应用场景
// 使用symbol类型是唯一的，其功能类似于唯一性的ID
// 使用
let s1 = Symbol()
// 或者
let s2 = Symbol("这里面的是属性描述符")

// 由于Symbol是一种基础数据类型，所以当我们使用typeof去检查它的类型的时候，它会返回一个属于自己的类型symbol，而不是什么string、object之类的：
typeof s1  // 'symbol'

// 另外，我们需要重点记住的一点是：每个Symbol实例都是唯一的。因此，当你比较两个Symbol实例的时候，将总会返回false：
s1 === s2 // false


// 使用symbol类型作为Object的属性名，是不能被Object.key(), for..in遍历出来的，symbol定义的属性对外界来说是隐藏的，如:
let NAME = Symbol()

let Obj = {
    [NAME]: 'ALex',
    age: '23',
    'sex': 1
}
Object.keys(Obj) // ["age", "sex"]

for(key in Obj) { // age sex
    console.log(key)
}

JSON.stringify(Obj) // "{"age":"23","sex":1}"

obj[NAME] // Alex

// 应用场景
// 使用Symbol来作为对象属性名(key),利用symbol不能被Object.key和for...in获取的特性，把一些不需要对外操作和访问的属性用symbol来定义

// 使用Symbol来替代常量

// 使用Symbol定义类的私有属性/方法

// 注册和获取全局Symbol:
// 如果应用涉及到多个windows共享一个symbol的话（比如说ifram），就不能使用symbol函数去定义一个全局唯一的symbol了，[因为在不同的windows环境中创建的Symbol实例总是唯一的],而我们需要在所有的这些window环境下保持一个共享的symbol，这种情况下，需要使用另一个API来创建和获取symbol，那个就是Symbol.for(),它可以注册和获取一个全局的Symbol实例：

let gs1 = Symbol.for('global_symbol_1')  //注册一个全局Symbol
let gs2 = Symbol.for('global_symbol_1')  //获取全局Symbol

gs1 === gs2  // true

// 这样一个Symbol不光在单个window中是唯一的，在多个相关window间也是唯一的了。
```

## JS的特性是什么

+ JS 是一种轻量级，解释性编程语言。

+ 为了创建以网络为中心的应用程序而设计

+ 补充和集成了 Java

+ 补充和集成了 HTML

+ 开放和跨平台

## JS创建对象的7种方式

1. 工厂模式
2. 构造函数模式
3. 原型模式
4. 构造函数与原型的组合模式
5. 动态原型模式
6. 寄生构造模式
7. 稳妥构造模式

> 工厂模式

```js
function Person () {
    let o = new Object()
    o.name = 'Alex'
    o.say = function () {
        console.log(this.name)
    }
    return o
}

var p1 = Person() // 这里不需要new， 因为函数已经返回
```
+ 优点: 返回了一个对象，完成了创建对象的要求
+ 缺点：

    1. 无法通过constructor识别对象，都是来自Object，无法得知是Person。【对象的构造函数指向它自己】
    2. 每次创建一个对象的时候， 所有的say方法都是一致的，但是存储了多次，造成资源浪费。

> 构造函数模式

```js
function Person () {
    this.name = 'Alex'
    this.say = function () {
        console.log(this.name)
    }
}

var p1 = new Person() //
```

+ 优点:

    1. 通过`constructor`或者`instanceof`可以识别对象实例的类别
    2. 可以通过`new` 关键字来创建对象实例，更像OO语言中创建对象实例

+ 缺点:

    1. 多个实例的say方法都是实现一样的效果，但是却存储了很多次（两个对象实例的say方法是不同的，因为存放的地址不同）

> 原型模式

```js
function Person () {}
Person.prototype.name = 'Alex'
Person.prototype.say = function () {
    console.log(this.name)
}
var p1 = new Person()
```

+ 优点：

    1. 所有的方法都是共享的，所有实例的方法都指向同一个
    2. 可以动态的添加原型对象的方法和属性，并直接反映在对象实例上。

+ 缺点：

    1. 当属性赋值给一个引用属性的情况下回出现共享的情况：
        ```js
            function Person () {}
            Person.prototype.name = 'LiHua'
            Person.prototype.arr = [1]
            Person.prototype.say = function () {
                console.log(this.name)
            }
            var p1 = new Person()
            var p2 = new Person()

            console.log(p1.arr) // [1]
            console.log(p2.arr) // [1]

            p2.push(0)
            console.log(p1.arr) // [1, 0]
        ```
        因为js对引用类型的赋值都是将地址存储在变量中，所以person1和person2的arr属性指向的是同一块存储区域。

    2. 第一次调用属性或函数的时候会搜索两次，第一次是在实例上去寻找这些方法和属性，没有的话就会去原型对象（`Person.prototype`）上去找，找到后会在实例上添加这些方法和属性

    3. 所有的方法都是共享的，没有办法创建实例自己的属性和方法，也没有办法像构造函数那样传递参数。

> 构造函数和原型组合模式

```js
function Person (name) {
    this.name = name
    this.arr = [0]
}
Person.prototype.say = function () {
    console.log(this.name)
}
var p1 = new Person('Alex')
```

+ 优点: 
    
    1. 解决了原型模式对于引用对象的缺点
    2. 解决了原型模式没有办法传递参数的缺点
    3. 解决了构造函数模式不能共享方法的缺点

+ 缺点:

    1. 存在一个问题就是直接通过对象字面量给`Person.prototype`进行赋值的时候会导致`constructor`改变，所以需要手动设置，其次就是通过对象字面量给`Person.prototype`进行赋值，会无法作用在之前创建的对象实例上

    ```js
        var person1 = new Person()
        Person.prototype = {
            name: 'hanmeimei2',
            setName: function(name){
            this.name = name
            }
        }
        person1.setName()   //Uncaught TypeError: person1.set is not a function(…)
    ```
    这是因为对象实例和对象原型直接是通过一个指针链接的，这个指针是一个内部属性`[[Prototype]]`，可以通过`__proto__`访问。我们通过对象字面量修改了`Person.prototype`指向的地址，然而对象实例的`__proto__`，并没有跟着一起更新，所以这就导致，实例还访问着原来的`Person.prototype`，所以建议不要通过这种方式去改变`Person.prototype`属性

> 动态原型模式

```js
function Person (name) {
    this.name = name
    if (typeof Person.prototype.say != 'function') {
        Person.prototype.say = function () {
            console.log(this.name)
        }
    }
}
```

+ 优点：

    1. 可以在初次调用构造函数的时候就完成原型对象的修改
    2. 修改能体现在所有的实例中

> 寄生构造函数模式

```js
function Person (name) {
    var o = new Object()
    o.name = name
    o.say = function () {
        console.log(this.name) // 这里的this很灵性
    }
    return o
}
var p1 = new Person('ALex') // 注意这里用了new操作符，和工厂模式不同
```

+ 优点

    1. 与工厂模式一样，多了个`new`

+ 缺点

    1. 与工厂模式一样，无法区分实例类别

> 稳妥构造模式

```js
function Person (name) {
    var o = new Object()
    o.name = name
    o.say = function () {
        console.log(name) // 注意这个地方
    }
}
var p1 = new Person('Alex')
p1.name // undefind
p1.say() // Alex
```