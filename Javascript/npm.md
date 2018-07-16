# NPM (Node Package Manager)

## Install
Node.js 在 0.6.3 版本開始內建 npm，不需另外安裝

## Usage
```shell=
# 透過 package.json 安裝依賴
npm install

# 安裝套件至全域
npm install packageName --global （-G）

# 安裝套件並記錄至 package.json
npm install packageName --save （-S）

# 安裝套件並記錄至 package.json 中的 devDependencies
npm install packageName --save-dev （-D）

# 移除套件 (記錄至package.json)
npm uninstall packageName （--save)

# 查詢全域中安裝的套件
npm list -g --depth 0

# 移除全域套件
npm uninstall -g [module name] [module name]

# 查詢 config
npm config list

# 搜尋套件資料
npm search <package name>
```