1. 最佳方法：直接和null做比较
```javascript
var tmp = null;
if(tmp === null) {
  alert("null");
} else {
  alert("不是null");
}
// 必须使用 === 防止强转
```

2. 也凑合
```javascript
var tmp = null;
if(!tmp && typeof(tmp) != "undefined" && tmp != 0) {
  alert("null");
} else {
  alert("不是null");
}
```
