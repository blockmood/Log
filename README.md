# 每日遇到的问题记录

## React 原生滚动条事件绑定

```
addEventListener('scroll',fn,true) true很关键
```

## React 解决 >= IE9的办法。

> browserslist  根据提供的目标浏览器的环境来，智能添加css前缀,js的polyfill垫片,来兼容旧版本浏览器。
```
@babel/polyfill
```
``` 
"browserslist": [
    "> 1%",
    "ie >= 9",
    "not op_mini all"
]
```
