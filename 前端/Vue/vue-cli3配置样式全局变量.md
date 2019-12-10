## vue-cli3配置样式全局变量.md

安装 style-resources-loader

```bash
npm i style-resources-loader -D
```

配置vue.config.js

```js
const merge = require('webpack-merge')
const tsImportPluginFactory = require('ts-import-plugin')
const autoprefixer = require('autoprefixer')
const pxtorem = require('postcss-pxtorem')
const path = require('path')

module.exports = {
  css: {
    // 配置postcss，自动将px转化成rem
    loaderOptions: {
      postcss: {
        plugins: [
          autoprefixer(),
          pxtorem({
            rootValue: 37.5,
            propList: ['*']
          })
        ]
      }
    }
  },
  chainWebpack: config => {
    // 配置项目的样式变量全局引入
    config.module
      .rule('less')
      .oneOf('vue')
      .use('style-resource')
      .loader('style-resources-loader')
      .options({
        patterns: [
          path.resolve(__dirname, './src/styles/variable.less'),
        ]
      })
  }
}

```

