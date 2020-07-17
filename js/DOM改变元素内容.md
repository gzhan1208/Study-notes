1. [innerHTML 改变元素的内容](#1)
2. [textContent 原样输出](#2)
3. [ele.style.cssAttr](#3)
4. [ele.style.cssText](#4)
5. [ele.className](#5)
6. [ele.classList 获取class集合](#6)
7. [ele.classList.add()](#7)
8. [ele.classList.remove()](#8)
9. [ele.classList.toggle() 在add和remove之前切换](#9)
10. [ele.classList.contains() 是否包含某个class，返回boolean值](#10)
11. [ele.setAttribute(attr, value) 设置样式](#11)
12. [隔行变色](#12)   


- <span id='1'>innerHTML 改变元素的内容</span>
  ```javascript
    test.onclick = function() {
      this.innerHTML = '<p>change</p>'
    }
  ```
- <span id='2'>textContent 原样输出</span>
  ```javascript
    test.onclick = function() {
      this.textContent = '<p>change</p>'
    }
  ```
- <span id='3'>ele.style.cssAttr</span>
  ```javascript
    test.onclick = function() {
      this.style.backgroundColor = '#0EA432'
    }
  ```
- <span id='4'>ele.style.cssText</span>
  ```javascript
    test.onclick = function() {
      this.style.cssText = "color:red;font-size:30px;background-color:yellow"
    }
  ```
- <span id='5'>ele.className</span>
  ```javascript
    test.onclick = function() {
      this.className = "test"
    }
  ```
- <span id='6'>ele.classList</span>
  ```javascript
    test.onclick = function() {
      console.log(this.classList)
    }
  ```
- <span id='7'>ele.classList.add()</span>
  ```javascript
    test.onclick = function() {
      this.classList.add("fs")
    }
  ```
- <span id='8'>ele.classList.remove()</span>
  ```javascript
    test.onclick = function() {
      this.classList.remove("fs")
    }
  ```
- <span id='9'>ele.classList.toggle() 在add和remove之前切换</span>
  ```javascript
    test.onclick = function() {
      this.classList.toggle("fs")
    }
  ```
- <span id='10'>ele.classList.contains() 是否包含某个class，返回boolean值</span>
  ```javascript
    test.onclick = function() {
      console.log(this.classList.contains("fs"))
    }
  ```
- <span id='11'>ele.setAttribute(attr, value) 设置样式</span>
  ```javascript
    var test = document.getElementById('test');
    test.setAttribute('style', 'color: red');
    test.setAttribute('class','current');
  ```
- <span id='12'>隔行变色</span>
    - css
      ```javascript
        :nth-child()  --> 从1开始
        even --> 偶数项
        odd --> 奇数项
        
        li:nth-child(odd) {
          color: red
        }
        li:nth-child(even) {
          color: green
        }
      ```
    - js
      ```javascript
        var lis = document.getElementsByTagName('li');
        for (var i = 0, len = lis.length; i < len; i++) {
          if (i % 2) {
            lis[i].style.color = 'red'
          } else {
            lis[i].style.color = 'green'
          }
        }
      ```
