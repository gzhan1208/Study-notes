# 基础使用
mixin是一种以更加灵活的方式分发vue组件中可复用的功能。  
官方推荐作为插件发布，不建议全局注册。  

// myMixin  

```javascript
const myMixin = {
  data() {
    return {
      name: 'Tom'
    }
  },
  created() {
    console.log('This is a mixin.')
  }
};

new Vue({
  mixins: [myMixin],
  data() {
    return {
      name: 'Jerry'
    }
  },
  created() {
    console.log(this.name);
    console.log('Self')
  }
});

//  => This is a mixin.
//  => Jerry
//  => Self
```

由上可发现混入的同名属性会被组件内的属性覆盖。  

# 使用场景
## 分页列表场景
```javascript
//  mixinList.vue
const list = {
  data() {
    return {
      list: [],
      page: 1,
      lineSize: 10,
      total: 0,
      loading: true
    }
  },
  created() {
    //  可控初始化
    const option = this.$option.isInit;
    if (option) {
      this.initData()
    }
  },
  methods: {
    initList() {
      this.list = [];
      this.page = 1;
      this.loading = true;
      this.loadData()
    },
    handleCurrentChange(val) {
      this.loading = true;
      this.page = val;
      this.loadData()
    },
    handleSizeChange(val) {
      this.loading = true;
      this.lineSize = val;
      this.page = 1;
      this.loadData()
    }
  }
};
export default list;
```
```javascript
//  other.vue
import List from '@/mixins/list';
export default {
    mixins: [List],
    data() {
        return {
            // 组件内其他属性
        }
    },
    method: {
        loadData() {
            // 调用接口请求数据
        }
    },
    isInit: true,
}
```
通过isInit控制时候在created时初始化。在使用keep-alive时，可以将isInit设置成false。
