### 被遗忘的 `for in` 特性
***

`for in` 会遍历所有属性包括继承来的可枚举属性。

可以使用继承至 `Object` 上的 `hasOwnProperty` 函数去限制 `for in` ，使得只遍历本身对象的可枚举属性。
