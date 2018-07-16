# ES6 陣列操作

Default Array
```javascript=
let family = [
  {
    name: 'Ben',
    age: 27,
    title: 'father',
    favorite: 'coding'
  },
  {
    name: 'Jessica',
    age: 26,
    title: 'mother',
    favorite: 'shopping'
  },
  {
    name: 'Rico',
    age: 3,
    title: 'son',
    favorite: 'playing'
  }
]
```
## Array.prototype.filter()
filter 會回傳一個陣列，其條件是 return 後方為 true 的物件，也就是只要 return 為真的值就會被加到新的陣列當中，很適合用在搜尋符合條件的資料。
```javascript=
let filterEmpty = family.filter((item, index, arr) => {})
console.log(filterEmpty)  //will be a []
```
```javascript=
let filterAge = family.filter((item) => {
  return item.age > 18
})
console.log(filterAge)  //will be an array contain Ben & Jessica
```
```javascript=
let filterFav = family.filter((item) => item.favorite == 'coding')
console.log(filterFav)  //will be an array contain Ben
```
## Array.prototype.find()
find 與 filter 很像，但 find 只會回傳一次值，且是第一次為 true 的值。
```javascript=
let findEmpty = family.find((item, index, array) => {})
console.log(findEmpty)  //will be undefined
```
```javascript=
let findAge = family.find( item => item.age == 3)
console.log(findAge)  //it will find Rico
```
```javascript=
let findTitle = family.find( item => item.title == 'mother')
console.log(findTitle) //it will find Jessica
```
## Array.prototype.forEach()
forEach 是這幾個陣列函式最單純的一個，不會額外回傳值(永遠回傳 undefined)，只單純執行每個陣列內的物件或值。
```javascript=
let foreachIt = family.forEach((item, index, arr) => {
  console.log(item, index, arr) //item: 當前物件  index: 當前索引  arr: 整個陣列 })
```
```javascript=
let foreachAgeIncrecement = family.forEach( item => item.age = item.age + 1)
console.log(family) 
```
## Array.prototype.map()
map 會回傳一個新的陣列，陣列中的值會是其 return 後方的值，適合將原始的變數運算後重新組合一個新的陣列。

如果不回傳則是 undefined，回傳數量等於原始陣列的長度
```javascript=
let mapEmpty = family.map((item, index, arr) => {})
console.log(mapEmpty)  //it will be 3 undefined element
```
```javascript=
let mapAge = family.map((item) => item.age > 18)
console.log(mapAge) 
```
```javascript=
let mapForFav = family.map((item) => {
  return `${item.name} like ${item.favorite}`
})
console.log(mapForFav)
```
## Array.prototype.every()
every 會遍歷整個陣列，並回傳 布林值。
其 return 後方的條件式若全為 true 則最後會回傳 true。若為 false 則會中斷遍歷並回傳 false。
```javascript=
let isAllAdulthood = family.every((item, index, arr) => {
  return item.age > 18 //檢查陣列中所有元素是否符合條件，全部符合回傳 true，反之 false
})
console.log(isAllAdulthood)
```
## Array.prototype.some()
some 與 every 非常類似，同樣會遍歷整個陣列，並回傳 布林值。
其 return 後方的條件式只要有一個 true 則會中斷遍歷，並回傳 true，若全為 false 則回傳 false。 
```javascript=
let hasAdulthood = family.some((item, index, arr) => {
  return item.age > 18 //檢查陣列中所有元素是否符合條件，有一符合就回傳 true，全不符合則為 false
})
console.log(hasAdulthood)
```

## Array.prototype.reduce()
reduce 和其他幾個差異就很大了，他可以與前一個回傳的值再次作運算。reduce 可傳入兩個參數，第一為 callback，第二個參數則是callback 中的參數，累加器(accumulator) 的初始值。
    callback 中的參數為以下
* accumulator: 前一次的值，如果是第一次則是由 reduce 的第二個參數提供，若第二個參數為空，其值會是呼叫 reduce 方法的陣列的第一個值
* currentValue: 當前變數
* currentIndex: 當前索引
* array: 全部陣列
```javascript=
let reduceEmpty = family.reduce((accumlator, currentVal, currentIndex, arr) => {})
console.log(reduceEmpty)   //沒有給條件，undefined
```
```javascript=
let reducePlus = family.reduce((accumulator, currentVal) => {
  return accumulator + currentVal.age
}, 0)
console.log(reducePlus)
```
```javascript=
let reduceMax = family.reduce((accumulator, currentVal) => {
  console.log('reduce', accumulator, currentVal)
  return Math.max(accumulator, currentVal.age)
}, 0) //取出最大的年齡
console.log(reduceMax)
```

```javascript=
arr.reduce((acc, next) => {
    console.log({acc,next})	
    return acc += " " + next
})
// {acc: "Ben", next: "like"}
// {acc: "Ben like", next: "reading"}
// "Ben like reading" //this is reduce return value 
```