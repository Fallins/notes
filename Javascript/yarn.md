# Yarn
[yarn](https://yarnpkg.com/zh-Hans/) another package manager 

## Install
[下載安裝檔](https://yarnpkg.com/zh-Hans/docs/install#windows-stable)

## Usage
```shell=
# 取得版本號
yarn --version

# 初始化
yarn init

# 添加 (等同於 npm install)
yarn add [package] --dev              // devDependencies
yarn add [package] --peer             // peerDependencies
yarn add [package] --optional         // optionalDependencies

# 安裝套件 (透過package.json)
yarn
yarn install

# 套件升級
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]

# 執行 Script (等同於 npm run)
yarn run ﹍﹍﹍(e.g. start, build....)

# 移除全域安裝套件
yarn glabal remove [module name] [module name]

# 查詢該套件詳細資料
yarn info [package]

# 查詢已安裝套件及版本
yarn list --depth=0
```