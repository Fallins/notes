# PostgreSQL

### Install
follow by http://www.postgresqltutorial.com/install-postgresql/



### Create database
By GUI
![](https://i.imgur.com/MVh6cPS.png)

By Command
`createdb test`


### Create table
```sql=
CREATE TABLE TABLE_NAME (COL_NAME TYPE, COL_NAME TYPE, ...);

-- e.g.
CREATE TABLE weather (
    city            varchar(80),
    temp_lo         int,  
    temp_hi         int, 
    prcp            real, 
    date            date
);
```

### Insert
```sql=
INSERT INTO TABLE_NAME VALUES (....values)
-- also can specify column name to insert
INSERT INTO TABLE_NAME (COL_NAME, COL_NAME) VALUES (....values);

-- e.g.
INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');
```

### SELECT
```sql=
SELECT * FROM weather;
SELECT city, temp_lo, temp_hi, prcp, date FROM weather;

-- e.g.
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;
```



[參考資料](https://docs.postgresql.tw/qian-yan)