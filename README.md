# 每日遇到的问题记录

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

## eslint配置

```
module.exports = {
    "env": {
        "browser": true,
        "es2021": true
    },
    "extends": ["eslint:recommended", "plugin:react/recommended"],
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": 13,
        "sourceType": "module"
    },
    "plugins": [
        "react"
    ],
    "rules": {
        //关闭换行符操作系统格式问题
        "linebreak-style": [
            "off",
            "unix"
        ],
        "quotes": [
            "error",
            "single"
        ],
        "semi": [
            "error",
            "always"
        ],
        // 禁止缩进错误
        "indent": 0,
        // 关闭不允许使用 no-tabs
        "no-tabs": "off",
        "no-console": 1,
        // 设置不冲突 underscore 库
        "no-underscore-dangle":0,
        // 箭头函数直接返回的时候不需要 大括号 {}
        "arrow-body-style": [2, "as-needed"],
        "no-alert":"error",
 
        // 设置是否可以重新改变参数的值
        "no-param-reassign": 0,
        // 允许使用 for in
        "no-restricted-syntax": 0,
        "guard-for-in": 0,
        // 不需要每次都有返回
        "consistent-return":0,
        // 允许使用 arguments
        "prefer-rest-params":0,
        // 允许返回 await
        "no-return-await":0,
        // 不必在使用前定义 函数
        "no-use-before-define": 0,
        // 允许代码后面空白
        "no-trailing-spaces": 0,
 
        // 关闭大括号内的换行符要求
        "object-curly-newline": 0,
 
        // 有一些 event 的时候，不需要 role 属性，不需要其他解释
        "jsx-a11y/no-static-element-interactions":0,
        "jsx-a11y/click-events-have-key-events":0,
        // 类成员之间空行问题
        "lines-between-class-members":0,
 
 
        // 不区分是否在 despendencies
        "import/no-extraneous-dependencies": 0,
        // 引用时候根据根目录基础
        "import/no-unresolved": 0,
 
        // 关闭解构赋值报错
        "react/destructuring-assignment": 0,   
        // 允许在 .js 和 .jsx 文件中使用  jsx
        "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
        // jsx > 紧跟着属性
        "react/jsx-closing-bracket-location": [1, "after-props"],
        // 不区分是否是 无状态组件
        "react/prefer-stateless-function": 0,
        // prop-types忽略children属性
        "react/prop-types": [1, { ignore: ["children"]}],
        // 关闭禁止prop-types类型
        "react/forbid-prop-types": 0,
        // 关闭default-props检查
        "react/require-default-props":0
    },
    "settings": {
        "react": {
            "version":"999"
        }
    }
};
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

## axios 返回res 多一个data

```
res.data.data 为值
```

## 关于IE9 localStorage undefined 问题
```
const data = window.localStorage  //赋值不支持
const data = window.localStorage.getItem('aa') //支持

```

## 关于IE9传递假字符串导致数据空白问题
```
解决办法 post方式 或者 假字符串转字符串
```

## react-router 不走路由渲染Html办法
```
render={}  否则输出字符串 "<div></div>"
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
