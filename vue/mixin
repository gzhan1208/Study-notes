# 基础使用
mixin是一种以更加灵活的方式分发vue组件中可复用的功能。  
官方推荐作为插件发布，不建议全局注册。  

// myMixin
`const myMixin = {
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
`

由上可发现混入的同名属性会被组件内的属性覆盖。  

# 使用场景
