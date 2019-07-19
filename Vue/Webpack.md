# Webpack相关知识点

> 什么是webpack

```
webpack是一个打包模块化javascript的工具，在webpack里一切文件皆模块，通过loader转换文件，通过plugin注入钩子，最后输出由多个模块组合成的文件，webpack专注构建模块化项目。
```

> 分别介绍bundle，chunk，module是什么

```
+ bundle：是由webpack打包出来的文件，
+ chunk：代码块，一个chunk由多个模块组合而成，用于代码的合并和分割。
+ module：是开发中的单个模块，在webpack的世界，一切皆模块，一个模块对应一个文件，webpack会从配置的entry中递归开始找出所有依赖的模块。
```

> 分别介绍什么是loader?什么是plugin?

```
+ loader：模块转换器，用于将模块的原内容按照需要转成你想要的内容 | 是使wenbpack拥有加载和解析非js文件的能力

+ plugin：在webpack构建流程中的特定时机注入扩展逻辑，来改变构建结果，是用来自定义webpack打包过程的方式，一个插件是含有apply方法的一个对象，通过这个方法可以参与到整个webpack打包的各个流程(生命周期) | 可以扩展webpack的功能，使得webpack更加灵活。可以在构建的过程中通过webpack的api改变输出的结果
```

> webpack构建流程

```
1. 初始化参数，从配置文件和shell语句中读到的参数合并，得到最后的参数
2. 开始编译：用合并得到的参数初始化complier对象，加载是所有配置的插件，执行run方法开始编译
3. 确定入口，通过entry找到入口文件
4. 编译模块，从入口文件出发，调用所有配置的loader对模块进行解析翻译，在找到该模块依赖的模块进行处理
5. 完成模块编译，得到每个模块被翻译之后的最终的内容和依赖关系
6. 输出资源，根据入口和模块之间的依赖关系，组装成一个个包含多个模块的chunk，在把每个chunk转换成一个单独的文件加载到输出列表
7. 输出完成，确定输出的路径和文件名，把内容写到文件系统中
```

> 如何利用webpack来优化前端性能

```
1. 压缩代码。uglifyJsPlugin 压缩js代码， mini-css-extract-plugin 压缩css代码
2. 利用CDN加速，将引用的静态资源修改为CDN上对应的路径，可以利用webpack对于output参数和loader的publicpath参数来修改资源路径
3. 删除死代码（tree shaking），css需要使用Purify-CSS
4. 提取公共代码。webpack4移除了CommonsChunkPlugin (提取公共代码)，用optimization.splitChunks和optimization.runtimeChunk来代替
```
