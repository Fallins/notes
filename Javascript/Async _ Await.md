# Async / Await

## Intro
當使用 async 時，會將一般的 return 包裝上 Promise，相當於 ``` return new Promise((resolve) => resolve("Ben"))```
```javascript=
const getName = () => {
    return 'Ben'
}

const getNameAsync = async () => {
    return 'Ben'
}

console.log( getName() )  //Ben
console.log( getNameAsync() ) //Promise {<resolved>: "Ben"}

getNameAsync().then((name) => console.log(name))  //Ben
```
---
await 關鍵字會等待 Promise resolve 後才執行後續動作，並且 name 會接到的是 resolve 的值，如果有例外，則會進拋出例外
```javascript=
const getName = () => {
    return Promise.resolve('Ben')
    //return Promise.reject('ERR')                
}
const logName = async () => {
    const name = await getName() //if get reject status, it will throw error
    console.log(name)
}
```

## Comparison 
定義取得 user 以及 grade 兩個方法，在有需要做同步執行時，才寫 async function，一般情況下維持 Promise 寫法即可
```javascript=
//data
const users = [
  { id: 1, name: 'A', schoolId: 101},
  { id: 2, name: 'B', schoolId: 202}]

const grades = [
  { id: 1, schoolId: 101, grade: 86},
  { id: 2, schoolId: 202, grade: 88},
  { id: 3, schoolId: 101, grade: 60}]

const getUser = (id) => {
  return new Promise((resolve, reject) => {
    const user = users.find(user => user.id === id)

    if(user)
      resolve(user)
    else
      reject("Can't find user")
  })
}

const getGrades = (schoolId) => {
  return new Promise((resolve, reject) => {
    resolve(grades.filter((grade) => grade.schoolId === schoolId))
  })
}
```


### In async/await
```javascript=
// In Promise
const getStatus = (userId) => {
  let user
  return getUser(userId).then(userTemp => {
    user = userTemp
    return getGrades(user.schoolId)
  }).then(grades => {
    let average = 0
    if(grades.length > 0){
      average = grades.map( grade => grade.grade).reduce((a, b) => a + b) / grades.length
    }
    // console.log("average", average)
    return `${user.name} has a ${average}% in the class`
  })
}

// In Async / Await
const getStatusAlt = async (userId) => {
  const user = await getUser(userId)
  const grades = await getGrades(user.schoolId)
  // console.log(user)
  // console.log(grades)
  
  let average = 0
  if(grades.length > 0){
    average = grades.map( grade => grade.grade).reduce((a, b) => a + b) / grades.length
  }
  // console.log("average", average)
  return `${user.name} has a ${average}% in the class`
}
```

To use
```javascript=
getStatus(3).then((status) => {
  console.log(status)
}).catch(e => console.log(e))

getStatusAlt(1).then(status => {
  console.log(status);
}).catch(e => console.log(e))

// getUser(10).then((user) => {
//   console.log(user);
// }).catch((e) => {
//   console.log(e);
// })

// getGrades(203).then(grades => {
//   console.log(grades);
// }).catch(e => {
//   console.log(e);
// })
```