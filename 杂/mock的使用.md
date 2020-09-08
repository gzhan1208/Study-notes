### 使用缘由
前端做一段时间大概就会遇到需求有了，页面也设计好了，但是接口还在写，如果等待接口写好再去写页面往往是不可取的。
因此，学会使用mock就比较方便了，在需要调用接口时模拟一个就好。

### 安装

```javascript
  // 安装
  npm install mockjs
```

```javascript
  // 使用
  const Mock = require('mockjs');
  const data = Mock.mock({
    'list|1-10': [
      {
        'id|+1': 1
      }
    ]
  })
```
以上为简单使用。涉及复杂的数据结构可前往[mock wiki](https://github.com/nuysoft/Mock/wiki/Syntax-Specification)

### Mock.mock()
```Mock.mock(template)``` 根据数据模板生成模拟数据。   

使用较多的为：
```Mock.mock(rurl, function(options))```    
其中rurl表示拦截的URL，可以是URL字符串或正则。例如
```/\/domian\/list\.json/```、```'/domian/list.json'```    
function()则为生成响应数据的函数

### Mock.setup()
- Mock.setup(setting)
配置拦截Ajax请求时的行为。支持配置项有：```timeout```    
**setting** 必选项    
**timeout** 可选项   
```javascript
  // timeout String|Number。单位毫秒，String类型时中间需要横杠'-'表示毫秒之间。如下200到1000毫秒之间
  Mock.setup({
    timeout: '200-1000'
  })
```

> setup(setting)仅限于配置Ajax请求
