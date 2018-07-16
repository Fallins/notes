#	深入 JS 系列筆記



## 原型基礎

### Prototype
當建立一個函式時，JS會自動幫我們建立一個 prototype 屬性，其值是一個物件並且擁有 constructor 屬性。
而 constructor 會指向原來的函式，也就是原構造函數。
prototype 可以理解為你想讓所有透過這個建構函式產生出來的物件可以共享的屬性跟方法，都可以加在 prototype 上面。
```javascript=
function  Person () {}

console.log(Person)
console.log(Person.prototype)  //prototype 物件，建立函式時自動建立的屬性
console.log(Person.prototype.constructor)  //也是自動產生出來的屬性，會指向 Person
console.log(Person.prototype.constructor === Person) //true，同上

Person.prototype.name = 'Kevin'  //在prototype上設定name屬性，使實體化產生出來的物件可以共用此屬性
var person1 = new Person()
var person2 = new Person()
console.log (person1.name) // Kevin 
console.log (person2.name) // Kevin ，person1 與 person2 都能夠存取到name這個屬性

//如果想要找到父層的物件本身可以透過 constructor 
person1.__proto__.constructor === Person  //true
```

### \_\_proto__
\_\_proto__ 與 prototype 不同，其存在於每一個 JS "物件"(prototype 是存在於每一個JS函式)，代表該物件繼承而來的源頭，而 \_\_proto__ 會指向其原型的 prototype。
以下面的例子來說，如果想找 Jack 爸爸的財產（屬性或方法），可以透過 Jack.\_\_proto__
可以想像為 \_\_proto__ 可以幫你找到爸爸的保險箱（Person.prototype，也就是說Jack.\_\_proto__ === Person.prototype)，那如果爸爸的保險箱沒有你要的東西，那可以再透過 爸爸的保險箱 去找到爺爺的保險箱（Object.prototype，也可以說Jack.\_\_proto__.\_\_proto__ === Person.prototype.\_\_proto__ === Object.prototype），以此類推會一直往上找，直到找到 null為止。


```javascript=
function Person (properties) {
    this.properties = properties
}  

//例1
var Jack = new  Person ();  
Jack.__proto__ === Person.prototype    //true，Jack 的藏寶圖找到爸爸(上層)的保險箱
Jack.__proto__.__proto__ === Object.prototype    //true，爸爸 的保險箱中又有藏寶圖可以找到爺爺的保險箱
Jack.__proto__.__proto__.__proto__ === null     //true，爺爺的保險箱中也有藏寶圖可以找到曾祖父的保險箱，但是曾祖父並沒有留下任何遺產(這邊理解為沒有留下遺產，實際上是原型鍊的最底層就是null)

//例2，尋找Person的原型鍊
Person.__proto__ === Function.prototype  //true，Person透過藏寶圖找到爸爸(Function)的保險箱

Person.__proto__.__proto__ === Object.prototype  //true，Person透過藏寶圖找到爸爸(Function)的保險箱中的藏寶圖後再去找爺爺的保險箱
Function.prototype.__proto__ === Object.prototype  //true，與上面相同，只是把 Person.__proto__ 代換成 Function.prototype

Person.__proto__.__proto__.__proto__ === null  //true，找到底了

```

### new
New 關鍵字透過函數建構子（function constructor)來建立一個新的物件。

```javascript=
function Person() {
    console.log(this)    //指向Person物件
    
    this.name = 'Ben'
    this.age = 18
    
    console.log(this)    //Person {name: "Ben", age: 18}
  
    //預設是回傳this，如果有設定回傳值則是回傳該值
    // return {name: 'return', age: 'NaN'}
}

//console.log(new Person())    //{name: "Ben", age: 18}

console.log(Person())        //在沒有使用 new 的情況下，Person 裡的 this 指向的是 window 物件，所以最後能在 window 上找到 name 以及 age 等屬性
console.log(window.name)    //Ben
console.log(window.age)    //18
```


### 範例
```javascript=
function Person(name, age) {
  this.name = name
  this.age = age
  this.testFn = () => {console.log("Test Fn")}
}

//如同上述所說，所有函數都會產生一個 prototype 屬性（但只有接在 new 之後才有用處）
Person.prototype.showDetails = function() {
  return `${this.name} is ${this.age} years old`
}

//透過 new 關鍵字產生一個新物件
const ben = new Person('Ben', 18)

//可以在ben裡面找到 testFn 方法，也就是說透過 new 產生的每一個新物件都會包含這個方法，如果產生的數量多的話，會造成效能的浪費
console.log(ben)                        //Person {name: "Ben", age: 18, testFn: ƒ}

//透過 prototype 來設定 showDetails 方法，該方法只存在於 Person 上面（只有一個 Person)，所以不管 new 多少個物件出來，showDetails 還是只會有一個，但所有透過 Person 產生的物件都還是可以透過 prototype chain 來使用此方法
console.log(ben.__proto__)              //{showDetails: ƒ, constructor: ƒ}

//ben 本身並沒有定義 showDetails 方法，但仍能透過 prototype chain 來呼叫定義在 Person 的 prototype 上的  showDetails 方法，
console.log(ben.showDetails())          //Ben is 18 years old


//回應上面講過的，所有物件都會有 __proto__ 屬性且會指向其原型的 prototype（Person)。
//所以因為 ben 是透過 Person 實體化出來的，所以其 __proto__ 屬性會指向其函數建構子的 prototype 屬性
//以此類推，會沿著 prototype chain 找直到找到 null 為止
console.log(ben.__proto__ === Person.prototype)              //true

```