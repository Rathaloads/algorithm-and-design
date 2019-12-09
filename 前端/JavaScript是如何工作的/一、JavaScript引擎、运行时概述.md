## 一、JavaScript引擎、运行时概述



### JavaScript引擎

JavaScript引擎，目前最流行的的一个示例是谷歌的V8引擎，其示例可以简化为下面图像：

![JavaScript引擎概述预览图](C:\code\algorithm-and-design\前端\JavaScript是如何工作的\images\JavaScript引擎概述预览图.png)

图片解释了V8引擎主要由两部分组成：

1. Memory Heap（内存堆）： V8 JavaScript Engine的一部分，用于存储变量以及函数的声明。V8引擎读取代码的时候，如果遇到变量以及函数的声明，会存在内存堆中以便使用。
2. Call Stack（调用堆栈）： V8 JavaScript Engine的一部分，用于存储和调用函数的地方。当Js引擎遇到函数调用之类的可操作项的时候，它会将其添加到堆栈中。将函数添加到堆栈后，JS引擎将立即跳入并开始解析其代码，将变量添加到Heap，将新函数调用添加到堆栈的顶部，或将自身发送到Web API调用所在的第三个容器。当一个函数返回一个值或发送到Web API容器时，它会从堆栈中弹出并移至堆栈中的下一个函数。 如果JS引擎到达函数的末尾并且没有显式编写任何返回值，则JS引擎将返回未定义并从堆栈中弹出该函数。



### The JavaScript Runtime Environment (JavaScript运行环境，也叫JavaScript运行时)



通过一张图片，简要概述一下 **Javascript Runtime Environment**



![](C:\code\algorithm-and-design\前端\JavaScript是如何工作的\images\JavaScript运行环境.png)

由上图可以知道，JavaScript Runtime Environment 主要由三个部分组成

1. **JavaScript Engine** -- 左侧的用于解析代码的JavaScript引擎，每个浏览器都有自己的JavaScript Engine，如谷歌的v8等。
2. **Web APIs** - 右上角的Web APIs，我们平常用到的setTimeout、setInterval、DOM、Window等等方法或者对象(API)，这些并不是JavaScript Engine所提供的，它们都是由浏览器提供的可以在JavaScript Engine中可用的API对象以及方法
3. **Event Loop** - 事件循环机制，Event Loop可以看做是JavaScript Runtime Environment中的一种机制，它的主要工作就是不断地检查堆栈（Call Stack?）和队列(Callback Queue?)中的内容，如果发现堆栈是空的，它就会通知队列将下一个回调函数发送给堆栈。队列和堆栈在一段时间内可能会是空的，但是Event Loop却永远不会停止它的工作，以确保Web APIs触发操作后，随时地将回调函数添加到队列中。
4. **Callback Queue** - 回调队列，Callback Queue也可以看做是JavaScript Runti Environment中的一种机制，它的主要工作就是按照添加顺序存储所有的回调函数，存储的回调函数会在Event Loop的检查下添加到JavaScript Engine的Call Stack中执行。