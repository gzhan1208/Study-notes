常见于 v-for 遍历数据   
```javascript
  <ul>
    <li v-for='item in items' :key='item.id'>...</li>
  </ul>
```
也可以用于强制替换元素/组件而不是重复使用它。如下两种场景： 
- 完成地触发组件的声明周期钩子
- 触发过度

例如：   
```javascript
  <transition>
    <span :key='text'>{{ text }}</span>
  </transition>
```
当text发生改变时，<span> 总是会被替换而不是修改，因此会触发过度。   

以前在写 vue 代码总觉得奇怪，为什么 v-for 就一定要加 key，不加 vue 就会报错。查看官网并了解虚拟 DOM 算法后才明白原由。   
总所周知，Vue 使用虚拟 DOM 算法，这个算法会在更新 DOM 结构时对比新旧两个 DOM。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能
的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。   

就地修改意味着从发生变化的节点后所有的 DOM 元素都将更新。而使用 key 时只基于key的变化重新排列元素顺序，不需要更新其他未修改的 DOM 元素，因此
加上 key 会使得 Vue 的以更高的效率更新虚拟DOM。   

通过查询关于key的知识时发现了一个有趣的问题，这个问题似乎没有在官网上看到，可能被我遗漏了。
用代码展示：
```javascript
  <div id="app">
    <div>
      <input type='text' v-model='name'>
      <button @click='add'>添加</button>
    </div>
    <ul>
      <li v-for='item in list'>
        <input type='checkbox'> {{ item.name }}
      </li>
    </ul>
  </div>
  // javascript
  const app = new Vue({
    el: '#app',
    data: {
      name: '',
      newId: 3,
      list: [
        {
          id: 1,
          name: 'TOM'
        },
        {
          id: 2,
          name: 'JERRY'
        }
      ]
    },
    methods: {
      add() {
        this.list.unshift({ id: ++this.newId, name: this.name });
        this.name = ''
      }
    }
  });
```
**当不加key时**，我先勾选 TOM，然后添加一条数据'new data'后，会发现'new data'项会被勾选，而'TOM'选项未被勾选。  
**当加上key时**，勾选TOM后无论怎么添加数据，最终都是TOM项被勾选。   
这也验证了加上key的元素具有唯一性，所以同一个组件中的key必须不同，否则就会渲染错误。这唯一的key则会和checkbox挂钩起来，最终达到我们需要的。
