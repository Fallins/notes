# BABEL
最基礎的 babel 設定

## INSTALL
安裝 Babel 主程式以及 presets，如果沒有裝過 babel-cli 也需要安裝。

babel-preset-env: 包含最新的 es2015 ~ es2017 版

```shell=
# babel-cli 安裝在全域
npm install -g babel-cli

npm install --save-dev babel-core babel-preset-env
```

## USAGE
### .babelrc
Babel 的設定檔
```json=
{
  "presets": ["env"]
}
```

### package.json
一般的幾個用法:

* 將 `script.js` 轉譯後輸出至目錄 dist 下的 `script-compiled.js`，也可用 `-o`來取代`--out-file`
`babel script.js --out-file dist/script-compiled.js`
* `--watch` 或是 `-w`，會監看檔案，有變動時重新編譯
`babel script.js --watch --out-file script-compiled.js`
* 編譯整個 src 資料夾並且輸出至 lib 資料夾
`babel src --out-dir lib`
* 複製文件或資料夾（不會進行編譯）
`babel src --out-dir lib --copy-files`
```json=
"scripts": {
    "build": "babel src -d dist"
}
```

### Run file after compiled
```javascript=
npm run build && npm start
```