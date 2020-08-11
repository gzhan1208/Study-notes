在vue开发中，经常会遇到需要魔改第三方组件库的某些样式的需求，并且只限定在某个页面中。
由于vue组件编译后，会将templete中的每个元素加入[data-v-xxxx]属性来确保style scoped仅
本身组件的元素使用而不污染全局，这时就需要使用深度作用选择器（ >>> 和 /deep/ ）的方式去解决。

- CSS
```javascript
  <style lang="css" scoped>
    .a >>> .b {
      /* ... */
    }
  </style>
```
- SASS/LESS
```javascript
  <style lang="scss" scoped>
    .a {
      /deep/ .b {
        /* ... */
      }
    }
  </style>
```
或者
```javascript
  <style lang="scss" scoped>
    .a {
      ::v-deep/ .b {
        /* ... */
      }
    }
  </style>
```
