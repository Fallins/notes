# Redis

## Install
[下載安裝檔](https://redis.io/download)

## Usage
```
設定(SET) / 取(GET) 資料

SET server:name "fido" //設定 KEY 為 server:name ， value 為 fido 的資料
GET server:name        //取得 KEY 為 server:name 的值


INCR / DEL 指令

SET count 1     //設定 key => count , value => 1
INCR count      //count + 1 (必須要是數字)
INCR count      //count + 1
GET count       // 3
DEL count       //刪除 count
INCR count      // 1


EXPIRE / TTL 指令

SET resource:lock "Redis Demo"      //設定一組值
EXPIRE resource:lock 120            //設定該值 120 秒後刪除
TTL resource:lock => 113            //利用TTL指令可查詢剩餘時間
TTL resource:lock => -2             //回傳 -2 時代表已刪除
SET resource:lock "Redis Demo 2"    //重新賦值 且不指定過期時間
TTL resource:lock => -1             //回傳 -1 代表永不過期


陣列操作( RPUSH, LPUSH, LLEN, LRANGE, LPOP, RPOP)

RPUSH friends "Alice"    //在陣列 '後' 加入資料
LPUSH friends "Sam"      //在陣列 '前' 加入資料
LRANGE friends 0 -1      //第一個參數為 起始index, 第二個參數為 結束index (如果為-1 則是取至最後一個)
LLEN friends             //取得陣列長度
LPOP friends => "Sam"    //取回陣列的第一筆資料，並回傳該值
RPOP friends => "Bob"    //取回陣列的最後一筆資料，並回傳該值


SET 操作 (SADD, SREM, SISMEMBER, SMEMBERS, SUNION)
每個元素只能出現一次，但是沒有排序的


SADD superpowers "flight"           //加入新的元素
SADD superpowers "x-ray vision"     //加入新的元素
SADD superpowers "reflexes"         //加入新的元素
SADD superpowers "reflexes"         //加入重複的元素會出現錯誤
SREM superpowers "reflexes"         //移除元素
SISMEMBER superpowers "flight" => 1 // 是否有該元素(flight), 回傳1代表有找到, 0則否
SMEMBERS superpowers                //列出SET裡所有元素

SADD birdpowers "pecking"           //加入一個新的SET
SADD birdpowers "flight"
SUNION superpowers birdpowers       //將兩個(或以上)的SET 做 UNION, 會列出所有的元素


Sorted SET 
相對於無序的SET，此操作是有排序的


ZADD hackers 1940 "Alan Kay"                       //加入元素
ZADD hackers 1906 "Grace Hopper"
ZADD hackers 1953 "Richard Stallman"
ZADD hackers 1965 "Yukihiro Matsumoto"
ZADD hackers 1916 "Claude Shannon"
ZADD hackers 1969 "Linus Torvalds"
ZADD hackers 1957 "Sophie Wilson"
ZADD hackers 1912 "Alan Turing"
                                                   //會根據數字作排序返回值
ZRANGE hackers 2 4                                 // 1) "Claude Shannon", 2) "Alan Kay", 3) "Richard Stallman"



Hashes 


HSET user:1000 name "John Smith"                    //可以針對 user:1000 這個 KEY
HSET user:1000 email "john.smith@example.com"       //加入 HASH 值
HSET user:1000 password "s3cret"                    

HGETALL user:1000                                   //取回所有的值
/*
1) "name"
2) "John Smith"
3) "email"
4) "john.smith@example.com"
5) "password"
6) "s3cret"
*/

HMSET user:1001 name "Mary Jones" password "hidden" email "mjones@example.com"    //也可以一次性設定多個值

HGET user:1001 name                                //單獨取回 name 的值 => "Mary Jones"




數字的 Hash 欄位


HSET user:1000 visits 10               //可以針對數字的 HASH 欄位
HINCRBY user:1000 visits 1 => 11       //做INCR的操作
HINCRBY user:1000 visits 10 => 21
HDEL user:1000 visits
HINCRBY user:1000 visits 1 => 1
```




中文文件: http://redisdoc.com/index.html























