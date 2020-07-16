# 从父原则  

> 当设置 position 值为 fixed 后会触发元素创建一个新的层叠上下文，我理解为子级。设置了 fixed 的元素，只能和同级以及子级元素比较层级关系  

> 如果需要和父级外的其他元素做层叠比较的话，需要给设置了 position：fixed 的父级添加 position 值，并设置 z-index，并最终以父级的 z-index 和其他元素做层级比较


##### 例如
```javascript
<div class="a">
  <div class="b"></div>
</div>
<div class="c"></div>

此时给 class.b 设置 position: fixed。    
那么 b 和 c 需要做层级比较的时候，则需要给 a 也设置 position 并根据 a 的 z-index 去和 c 的 z-index 比较
```
