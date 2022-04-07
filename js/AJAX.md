```
参考: https://wangdoc.com/javascript/bom/xmlhttprequest.html
```
### AJAX 包括以下几个步骤

  > 1. 创建 XMLHttpRequest 实例
  > 2. 发出 HTTP 请求
  > 3. 接收服务器传回的数据
  > 4. 更新网页数据

  `AJAX 只能向同源网址（协议、域名、端口都相同）发出 HTTP 请求，如果发出跨域请求，就会报错`
  
### 下面是XMLHttpRequest对象简单用法的完整例子
```
  var xhr = new XMLHttpRequest();

  xhr.onreadystatechange = function(){
    // 通信成功时，状态值为4
    if (xhr.readyState === 4){
      if (xhr.status === 200){
        console.log(xhr.responseText);
      } else {
        console.error(xhr.statusText);
      }
    }
  };

  xhr.onerror = function (e) {
    console.error(xhr.statusText);
  };

  xhr.open('GET', '/endpoint', true);
  xhr.send(null);
```
