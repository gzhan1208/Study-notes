> [借鉴: https://juejin.im/post/5d548b83f265da03ab42471d](https://juejin.im/post/5d548b83f265da03ab42471d)  
  
项目优化大致可分3个方面：代码层面、Webpack配置层面和Web层面  

## 1.Vue代码层面  
### 1.1. v-if和v-show分场景使用
### 1.2. watch和computed分场景使用
### 1.3. v-for必须加key，且避免同时使用v-if
### 1.4. 长列表性能优化
  [Vue](https://cn.vuejs.org/v2/guide/index.html)会通过[Object.defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
  对数据进行劫持，来实现视图响应数据的变化。但有时我们的组件纯粹的就是展示数据，所以我们不需要数据劫持。
  在大量数据展示时可以使用[Object.freeze()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
  方法来冻结一个对象，一旦被冻结的对象就再也不能被修改了。
  ```javascript
  export default {
    data: () => ({
      users: {}
    }),
    async created() {
      const users = await axios.get("/api/users");
      this.users = Object.freeze(users);
    }
  };
  ```
### 1.5. 事件销毁
  如果使用了监听器，在页面销毁前手动移除监听，避免内存泄漏
  ```javascript
  beforeDestory() {
    removeEventListener('click', this.click, false)
  }
  ```
### 1.6. 图片懒加载
  安装
  ```javascript
  npm install vue-lazyload --save-dev
  ```
  引入与使用
  ```javascript
  import VueLazyload from 'vue-lazyload';
  Vue.use(VueLazyload);
  ```
  自定义选项
  ```javascript
  Vue.use(VueLazyload, {
    preLoad: 1.3,
    error: 'dist/error.png',
    loading: 'dist/loading.gif',
    attempt: 1
  })
  ```
  图片懒加载
  ```javascript
  <img v-lazy="/static/img/1.png" alt="" />
  ```
### 1.7. 路由懒加载
  Vue  是单页面应用，可能会有很多的路由引入 ，这样使用 webpcak 打包后的文件很大，当进入首页时，加载的资源过多，
  页面会出现白屏的情况，不利于用户体验。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候
  才加载对应的组件，这样就更加高效了。这样会大大提高首屏显示的速度，但是可能其他的页面的速度就会降下来。
  ```javascript
  const Foo = () => import('./Foo.vue');
  const router = new VueRouter({
    routes: [
      { path: '/foo', component: Foo }
    ]
  })
  ```
### 1.8. 第三方插件按需引入
  我们在项目中经常会需要引入第三方插件，如果我们直接引入整个插件，会导致项目的体积太大，
  我们可以借助 babel-plugin-component ，然后可以只引入需要的组件，以达到减小项目体积的目的。
  以下为项目中引入 element-ui 组件库为例：
  ```javascript
  // 安装
  npm install babel-plugin-component -D  
  
  // 修改.babelrc文件
  {
    "presets": [["es2015", { "modules": false }]],
    "plugins": [
      [
        "component",
        {
          "libraryName": "element-ui",
          "styleLibraryName": "theme-chalk"
        }
      ]
    ]
  }  
  
  // 在main.js中引入部分组件
  import Vue from 'vue';
  import { Button, Select } from 'element-ui';
  Vue.use(Button)
  Vue.use(Select)
  ```
### 1.9. 优化无限列表性能
  如果存在很长或无线滚动的列表，那么需要采用窗口化的技术来优化性能，只需要渲染部分区域内容，减少重新渲染组件和创建 dom 节点时间。
  参考以下开源项目 [vue-virtual-scroll-list](https://github.com/tangbc/vue-virtual-scroll-list) 
  和 [vue-virtual-scroller](https://github.com/Akryum/vue-virtual-scroller) 来优化这种无限列表的场景的。
### 1.10. 服务端渲染SSR或者预渲染
  > 服务端渲染优点：  
      更好的 SEO ： SPA 页面内容是通过 Ajax 获取，搜索引擎爬取工具不会等待 Ajax 异步完成再抓取内容；而 SSR 直接由服务端返回渲染好的页面  
      更快的内容到达时间： SPA 会等待 Vue 编译后的 js 文件都下载完成后才会开始页面渲染； SSR 直接由服务端返回渲染好的页面，无需等待下载js文件  
  > 服务端渲染缺点：  
      更多的开发条件限制：只支持 beforCreate 和 created 两个钩子函数，这会导致一些外部扩展库需要特殊处理，才能在服务端渲染应用程序中运行；服务端渲染应用程序需要 Node.js server 运行环境  
      更多的服务器负载：因为在 Node.js 中渲染完成的应用程序，所以会占用部分 CPU 资源，如果在高流量环境下使用，需要准备相应的服务器负载，并民智的采用缓存策略  

## 2.Webpack层面  
### 2.1. 对图片进行压缩  
  使用 [image-webpack-loader](github.com/tcoopman/image-webpack-loader#readme) 来压缩图片
### 2.2. 减少 ES6 转为 ES5 的冗余代码
### 2.3. 提取公共代码
  使用 [CommonsChunkPlugin](https://webpack.js.org/plugins/commons-chunk-plugin/) 插件提取公共代码
### 2.4. 模板预编译  
  使用 [vue-template-loader](github.com/ktsn/vue-template-loader#readme) ，它也可以在构建过程中把模板文件转换成为 [JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript) 渲染函数。
### 2.5. 提取组件CSS
  [webpack](https://www.webpackjs.com/concepts/) + [vue-loader](https://vue-loader.vuejs.org/) ( [vue-cli](https://cli.vuejs.org/guide/) 的 [webpack](https://www.webpackjs.com/concepts/) 模板已经预先配置好)
### 2.6. 优化SourceMap
### 2.7. 构建结果输出分析

## 3.Web层面  
### 3.1. 开启 gzip 压缩
  使用 [compression](github.com/expressjs/compression#readme) 开启gzip压缩
### 3.2. 浏览器缓存
### 3.3. CDN的使用
### 3.4. Chrome Performance查找性能瓶颈

