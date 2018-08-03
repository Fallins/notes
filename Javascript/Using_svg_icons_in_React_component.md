# Using svg icons in React component

## Install
```javascript=
npm install --save svg-sprite-loader
```

## Setup
```javascript=
{
  test: /\.svg$/,
  loader: 'svg-sprite-loader'
}

// 正常配置
// 加在 webpack config 中的 module.rules 下
module: {
    rules: [
      {
        test: /\.js$/,
        loader: 'babel-loader'
      },
      {
        test: /\.svg$/,
        loader: 'svg-sprite-loader'
      }
    ]
}

// create-react-app 中的配置
// 1. yarn/npm run eject
// 2. 修改 webpack.config.dev.js 與 webpack.config.prod.js 中的配置
// 加在 webpack config 中的 module.rules.oneOf 下

```
![](https://i.imgur.com/EH4yZYm.png)
一般配置

![](https://i.imgur.com/3OHA6IX.png)
create-react-app 中的配置

## Usage
### 設置 SVG
新增 `icons.svg`
```htmlmixed=
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <defs>
        <symbol id="ADA" viewBox="0 0 32 32">
            <title>ADA</title>
            <path fill="#246fd3" style="fill: var(--color1, #246fd3)" d="...."></path>
        </symbol>
        
        <symbol id="XXX" viewBox="0 0 32 32">
            ...
        </symbol>
        
        <symbol id="ABC" viewBox="0 0 32 32">
            ...
        </symbol>
    </defs>
</svg>
```

### ICON 元件
新增 `Icon.js`
```javascript=
import React from 'react'
import './icons.svg'
import style from './icons.css'

const Icon = (props) => (
  <svg className={`${style.icon} icon_${props.name}`}>
    <use xlinkHref={`#icons_${props.name}`} />
  </svg>
)

export default Icon
```

使用

透過設置 webpack ，會將 `import` 的 svg 檔案加入 HTML 頁面中，並加上 icons_ 前綴。
![](https://i.imgur.com/pnTEud6.png)

因此使用上僅需將原始 SVG 檔案中的 ID 名傳入即可。
```javascript=
<Icon name="camera" />
```




---

參考資料:
[1](https://medium.com/douglas-matoso-english/build-an-svg-icon-component-with-react-de9db211ebd6)
[2](https://segmentfault.com/a/1190000015367490)
[3](https://blog.ihanai.com/2018/03/07/use-svg-sprite-loader-in-project-created-by-create-react-app/)
[4](https://www.zhangxinxu.com/wordpress/2014/07/introduce-svg-sprite-technology/)