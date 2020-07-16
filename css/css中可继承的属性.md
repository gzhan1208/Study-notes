# 常用CSS中可以被继承的属性

1. 字体系列属性   
    - font-family: 字体系列
    - font-weight: 字体粗细
    - font-size: 字体的大小
    - font-style: 字体的风格
   
2. 文体系列属性
    - text-indent：文本缩进
    - text-align：文本水平对齐
    - line-height：行高
    - word-spacing：单词之间的间距
    - letter-spacing：中文或者字母之间的间距
    - text-transform：控制文本大小写（就是uppercase、lowercase、capitalize这三个）
    - color：文本颜色
    
3. 可见性属性
    - visibility：控制元素显示隐藏
    
4. 列表布局属性
    - list-style：列表风格，包括 list-style-type、list-style-image 等
    
5. 光标属性
    - cursor: 光标显示为何种形态
    
# 继承中比较特殊的情况

1. a 标签的字体颜色不能被继承
2. h1-h6 标签字体的大小不能被继承   
> 因为他们都有一个默认值

# 实践

通过继承。最常见的就是在 body 中设置字体的颜色，大小等等

```
body {
  font-family: Helvetica Neue,Helvetica,PingFang SC,Hiragino Sans GB,Microsoft YaHei,SimSun,sans-serif;
  color: #e3e3e3;
  font-weight: 400;
  ...
}
```
