# 每日遇到的问题记录

## 正则匹配文字 数字 字母 下划线
```
[\u4e00-\u9fa5_a-zA-Z0-9]
```

## swiper loop:true 属性  无法复制react合成事件，导致事件失效
解决: 第一和最后 单独绑定click

## swiper 4.0  滑动导致activeIndex 错乱问题
原因：滑动的时候setInterval还在执行，导致activeIndex混乱，只需在事件中停止即可。

## es7 装饰器babel支持

```
@babel/plugin-proposal-decorators
```

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
