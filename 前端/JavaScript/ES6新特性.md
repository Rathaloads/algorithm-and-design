# ES6新特性
> const 与 let 变量

  使用var会出现变量提升的问题，使用let和const则不会出现这样的问题

> 模板字面量

  之前使用字符串拼接是使用+号或concat()方法，模板字面量使用``，模板里面可以嵌入表达式或变量

> 解构

  在ES6中,可以使用解构从数组和对象提取值并赋值给独特的变量

> 对象字面量简写法

  使用和所分配的变量名称相同的名称初始化对象时如果属性名称和所分配的变量名称一样，那么就可以从对象属性中删掉这些重复的变量名称。

> for...of循环

  ....

> 展开运算符(...)

  展开运算符（用三个连续的点 (...) 表示）是 ES6 中的新概念，使你能够将字面量对象展开为多个元素

> ES6箭头函数

  ()=>{}, 箭头函数内的this与外面的this是一样的

> 默认参数函数

  ....

> Javascript类

  ES6类只是一个语法糖,原型继续实际上在底层隐藏起来, 与传统类机制语言有些区别

```js
class Plane {
  //constructor方法虽然在类中,但不是原型上的方法,只是用来生成实例的.
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }
  //原型上的方法, 由所有实例对象共享.
  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}

console.log(typeof Plane); //function
```

> super 和 extends

  使用新的super和extends关键字扩展类:

```js
class Tree {
  constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
    this.size = size;
    this.leaves = leaves;
    this.leafColor = null;
  }

  changeSeason(season) {
    this.leafColor = this.leaves[season];
    if (season === 'spring') {
      this.size += 1;
    }
  }
}

class Maple extends Tree {
  constructor(syrupQty = 15, size, leaves) {
    super(size, leaves); //super用作函数
    this.syrupQty = syrupQty;
  }

  changeSeason(season) {
    super.changeSeason(season);//super用作对象
    if (season === 'spring') {
      this.syrupQty += 1;
    }
  }

  gatherSyrup() {
    this.syrupQty -= 3;
  }
}
// super 必须在 this 之前被调用
```

  在子类构造函数中，在使用 this 之前，必须先调用超级类。

```js
class Apple {}
class GrannySmith extends Apple {
  constructor(tartnessLevel, energy) {
    this.tartnessLevel = tartnessLevel; // 在 'super' 之前会抛出一个错误！
    super(energy); 
  }
}
```