# Module Bundler
![](https://i.imgur.com/tPPsDbS.png)

## Webpack

### Install
Install in develop environment
```javascript=
npm install --save-dev webpack webpack-dev-server webpack-cli

// 安裝 babel 相關的 module
// babel-core: Babel 的主要程式
// babel-loader: 讓 webpack 能夠使用 Babel
// babel-preset-env: 將 ES6+ 的語法轉譯為 ES5
// babel-preset-react: 編譯 JSX
npm install --save-dev babel-core babel-loader babel-preset-env babel-preset-react

// 安裝 eslint 相關的 module
// eslint: 主程式
// eslint-loader: 讓 webpack 使用 eslint
// babel-eslint: 讓 eslint 能夠提示其尚不支援的語法錯誤
npm install --save-dev eslint eslint-loader babel-eslint

// 使用 eslint-config-airbnb 的規則需要安裝以下 modules
npm install --save-dev eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react

```

### Setup
`package.json` 新增 `start` script
```javascript=
  "scripts": {
    "start": "webpack-dev-server --config ./webpack.config.js --mode development"
  }
```

`.babelrc` 設定 babel 相關的 config
```json=
{
    "presets": [
        "env",
        "react"
    ]
}
```

`.eslintrc` 設定 eslint 相關的 config
```json=
{
    "parser": "babel-eslint",
    "rules": {
        // 如果程式中有 console 則會提示 warning
        "no-console": "warn"
    },
    // 使用 eslint-config-airbnb 的規則需要增加下面 extends 設定
    "extends": [        
        "airbnb"
    ]
}
```

`webpack.config.js`
* entry: 提供程式的進入點給 webpack
* output: bundle 後檔案存放位置及檔名
* module: 當中的 rules 用來設定多個規則，供 webpack 比對檔名(透過test屬性)，並使用正確的loader
* resolve: import 檔案時，如果副檔名是 resolve 中設定的則可以省略
* devServer: 設定要給 server 提供服務的路徑
```javascript=
module.exports = {    
    entry: [
        './src/index.js'
    ],
    output: {
        path: __dirname + '/dist',
        publicPath: '/',
        filename: 'bundle.js'
    },    
    module: {
        rules: [
            {
                test: /\.(js|jsx)/,
                exclude: /node_modules/,
                use: ['babel-loader']
            },
            {
                test: /\.(js|jsx)/,
                exclude: /node_modules/,
                use: ['eslint-loader']
            }
        ]
    },
    resolve: {
        extensions: ['.js', '.jsx']
    },
    devServer: {
        contentBase: './dist'
    }
}
```

[online webpack confing creator](https://webpack.jakoblind.no/)


## Parcel

### Install
```javascript=
npm install --save-dev parcel-bundler babel-preset-env babel-preset-react
```

### Setup
* 有使用到 Babel 一樣要設置 `.babelrc`
* 在`package.json`中設定 `start` script
```javascript=
"scripts": {
    "start": "parcel index.html"
},
```

### Usage
執行 `npm start` ，Parcel 會從 `index.html` 為進入點開始解析，任何有用到的JS、CSS、IMAGE等等都會打包完成

### Refference
[官網](https://parceljs.org/)
[中文文檔](http://www.css88.com/doc/parcel/getting_started.html)