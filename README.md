# 记录
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
```
Alpha：第一个测试版本，还不稳定
Beta：特性稳定了，但还有bug
RC(Release Candidate)：除非有重大bug，否则这就是会成为正式版的Beta
Release：正式发布版本
```

## vscode主题

```
Dracula Official
```

## 记住token
```
git config credential.helper store
```



## 代码格式化

.prettierrc

```
{
  "printWidth": 100, 
    "overrides": [
        {
            "files": ".prettierrc",
            "options": { "parser": "json" }
        }
    ],
  "tabWidth": 2, 
  "useTabs": false, 
  "semi": true, 
  "singleQuote": true, 
  "proseWrap": "preserve", 
  "arrowParens": "avoid", 
  "bracketSpacing": true,
  "disableLanguages": ["vue"], 
  "endOfLine": "auto", 
  "eslintIntegration": false, 
  "htmlWhitespaceSensitivity": "ignore",
  "ignorePath": ".prettierignore", 
  "jsxBracketSameLine": false, 
  "jsxSingleQuote": false, 
  "requireConfig": false, 
  "stylelintIntegration": false, 
  "trailingComma": "es5",
  "prettier.tslintIntegration": false 
}
```

## ios软键盘会导致h5端定位样式跟webview会冲突，导致样式错位


## Scheme判断方式

```
const ua = (function () {
    const regs = {
        // 系统
        // 'ios': /iphone|ipad|ipod/,
        'android': /android/i,

        // 机型
        'iphone': /iphone/i,
        'ipad': /ipad/i,
        'ipod': /ipod/i,

        // 环境
        'weixin': /micromessenger/i,
        'mqq': /QQ\//i,
        'app': /inke/i,
        'alipay': /aliapp/i,
        'weibo': /weibo/i,

        // 浏览器
        'chrome': /chrome\//i
    }

    const ret = {}
    Object.keys(regs).forEach((key) => {
        var reg = regs[key]
        ret[key] = reg.test(navigator.userAgent)
    })

    ret.ios = ret.iphone || ret.ipad || ret.ipod
    ret.mobile = ret.ios || ret.android
    ret.pc = !ret.mobile
    ret.chrome = !!window.chrome

    return ret
})()

const openApp = (androidScheme = 'bbmm://com.bbmm.family', iosScheme = 'babamamaGroup://') => {
    if (ua.android) {
        window.location.href = androidScheme
        setTimeout(() => {
        window.location.href = 'https://sj.qq.com/myapp/detail.htm?apkName=com.bbmm.family'
        }, 500)
    } else {
        window.location.href = iosScheme
        // setTimeout(() => {
        //   window.location.href = ''
        // }, 500)
    }
}

openApp()
```

## node 事件报错以及调试

```
process.on('unhandledRejection', (reason, p) => {
  console.log('Unhandled Rejection at: Promise', p, 'reason:', reason);
  process.exit(1) //退出
  // application specific logging, throwing an error, or other logic here
});
```

## axios 取消上一次请求
```

axios 提供CancelToken属性
let CancelToken = axios.CancelToken  //返回一个取消请求的构造函数
cancelToken属性： 实例化 CancelToken  传入 （c） => c  这个c就是取消的函数 


axios({
  url:'http://jsonplaceholder.typicode.com/comments',
  type:'get',
  cancelToken: new CancelToken((c)=>{
    this.state.cancel = c
    console.log(c)
  })
}).then(res => {
  console.log(res.data)
})

//取消
this.state.cancel()
```

## webpack optimization.runtimeChunk(注意css也是按需打包)
```
设置optimization.runtimeChunk到true或"multiple"增加了一个额外的块仅包含运行时每个入口点。
就是会从公共代码(verdor)中单独抽出一个 runtime-hash.js  这里面包含所有分片载入的js文件
```



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



