# 每日遇到的问题记录

## micro task queue 队列的顺序 
> 后进先出

## chrome 跨域浏览器
```
--disable-web-security --user-data-dir=C:\MyChromeDevUserData  (C:\MyChromeDevUserData 你自己的目录)
```

## node中 new RegExp()  反斜杠 \ 必须为 双反斜杠 不然无法解析

```
例子  /school/(\\d+)/ 
```

## webpack 通过plugins设置不同的环境变量
```
new webpack.DefinePlugin({
   "process.env.REACT_ENV": JSON.stringify("h5 / app")  // 指定不同的编译环境
})

react中通过 process.env.REACT_ENV 编译不同的环境代码

```

## 正则匹配文字 数字 字母 下划线
```
[\u4e00-\u9fa5_a-zA-Z0-9]  或者 .(通配匹配)
```

## swiper loop:true 属性  无法复制react合成事件，导致事件失效
解决: 第一和最后 单独绑定click

## swiper 4.0在APP中滑动导致activeIndex 错乱问题
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
