# temp_table
temp_table
```
-- create table
CREATE TABLE [#tmp_people]
(
    username NVARCHAR(100),
    age int
)

-- 2 rows
INSERT INTO [#tmp_people] (username,age)
VALUES
('Wang',20),('Lin',28)

-- select 
select * from #tmp_people

-- drop
DROP TABLE #tmp_people
```
Result:
```
username	age
Wang	20
Lin	28
```
