# temp_table
temp_table

在資料庫中有時SQL語句過長到不好理解，就可以利用temp table來做預處理。  
temp table。可以允許把已經處理好、想暫存的資料寫入進該表，再進行取用。  
此外亦可以建立index，提升使用起來的速度。  
temp table以 # 開頭，並儲存於SQL Sever記憶體中，每次重啟時會被洗掉，但為求保險使用後還是得自己drop掉。  

此外暫存表分兩種模式:
```
#Table:一個#，僅建立表的user可以使用
##Table:兩個##，所有user皆可以使用
```
```
-- create table
CREATE TABLE [#tmp_people]
(
	id int,
    username NVARCHAR(100),
    age int
)

-- set index
CREATE INDEX IX_tmp_people_id ON #tmp_people (id);
CREATE INDEX IX_tmp_people_username ON #tmp_people (username);
CREATE INDEX IX_tmp_people_id_age ON #tmp_people (id desc, age desc);

-- 2 rows
INSERT INTO [#tmp_people] (id,username,age)
VALUES
(1,'Wang',20),(2,'Lin',28)

-- select 
select * from #tmp_people

-- select by target index
select * from #tmp_people with(INDEX(IX_tmp_people_id))
where age = 28

-- drop
DROP TABLE #tmp_people
```

Result:
```
1	Wang	20
2	Lin	28
---
2	Lin	28
```
