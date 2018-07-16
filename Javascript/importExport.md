# Import / Export

## export
```javascript=
// 默認導出
export default "this is default export"

// 一般導出
export const ID = "3345678"            // 變數導出
export const add = (a, b) => a + b     // 函數導出
```

## import

```javascript=
// 默認導入
import str from './xxx/xxx'

// 一般導入
import { ID, add } from './yyy/yyy'
// 一般導入並取小名
import { ID as x, add as a } from './yyy/yyy'

//全導
import * as wtf from './zzz/zzz'


console.log( str )      // this is default export

//一般
console.log( ID )                   //  3345678
console.log( add(1, 2) )        //   3

//小名
console.log( x )                   //  3345678
console.log( a(1, 2) )          //   3

//全導
console.log( wtf.ID )                   //  3345678
console.log( wtf.add(1, 2) )        //   3
console.log( wtf.default )          //   印出默認導出的東西
```