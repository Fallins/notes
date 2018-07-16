# Udemy course note - The complete web developer in 2018

## Foundemental of Internet
### How Internet works
一般使用者(Client) 透過 ISP(Internet Service Provider)來連線至網路，ISP 之間則是透過 [海底電纜](https://www.submarinecablemap.com/#/) 互相串聯來提供網際網路的服務。

![](https://i.imgur.com/qsHo7lR.gif)

![](https://i.imgur.com/K0Cbhpg.png)
(海底電纜的部分截圖)

[5分鐘了解網路如何運作](https://www.youtube.com/watch?v=7_LPdttKXPc)

### traceroute
查詢從本機至 google 中間經過的節點與時間
```shell=
#mac
traceroute google.com
#windows
tracert google.com
```
![](https://i.imgur.com/3jAyXva.png)
### The important things about performance
* Location Of Server
伺服器之間實際的物理距離會影響傳輸速度
* How Many Trips
中間經過越多節點也會影響速度
* Size Of Files
各種圖片、影片、HTML、CSS、JS等檔案的大小也會影響



## HTML
### What is doctype means?
用來告訴瀏覽器該如何解讀該 HTML 檔案，`<!DOCTYPE html>` 用來指定為HTML5。
### HTML Semantic Elements
H5 語意化標籤
![](https://i.imgur.com/Cq4QQUs.gif)
其他諸如: table、form、strong 等等也都算是。

目的主要是可以便於瀏覽器、搜索引擎解析、利於SEO、更好的無障礙閱讀體驗
[更多介紹...](https://ithelp.ithome.com.tw/articles/10195356)

## CSS
### Tools
[線上色彩選擇器-Paletton](https://paletton.com)
[青蛙教學](https://flexboxfroggy.com/)

## JS
### ES7
**includes**
```javascript=
'hello'.includes('he')    //true
'hello'.includes('123')    //false

const animals = ['dog', 'cat', 'fish']
animals.includes('dog')    //true
animals.includes('bird')    //false
```
**Exponentiation Operator(\*\* 求冪運算)**
```javascript=
let a = 2 ** 3    //2的三次方
let b = 2 ** 5    //2的五次方
console.log(a === Math.pow(2,3)) // true
console.log(b === Math.pow(2,5)) // true
```

### ES8
**padStart / padEnd**
```javascript=
//第一個參數為最大長度，第二個參數為填充物(如無則為空白)
'hello'.padStart(10)  // '     hello'
'hello'.padEnd(10)    // 'hello     '

'hello'.padStart(10, 'ab')    // 'ababahello'
'hello'.padEnd(9, 'ab')       // 'helloabab'
```

**Object.values / Object.entries**
```javascript=
const obj = {
    person1: 'Ben',
    person2: 'Jessica',
    person3: 'Rico'
}

// 在沒有 Object.values 以前，取得物件中所有值的方法
// 會印出 Ben、Jessica、Rico
Object.keys(obj).forEach((val) => {
    console.log(obj[val])
})

// 結果同上
Object.values(obj).forEach((val) => {
    console.log(val)
})

// 會印出 ["person1", "Ben"]、["person2", "Jessica"]、["person3", "Rico"]
Object.entries(obj).forEach(val => {
    console.log(val)
})
```