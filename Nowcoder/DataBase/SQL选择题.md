## 题号 1

一张学生成绩表score，部分内容如下：
name    course   grade
张三    操作系统   67
张三    数据结构   86
李四    软件工程   89
用一条SQL 语句查询出每门课都大于80 分的学生姓名，SQL语句实现正确的是：

```sql
Select distinct name from score where name not in(Select name from score where grade <= 80);
```

**知识点**： SQL 语句中包括 `not in`；

## 题号 2：选择插入

某打车公司将驾驶里程（drivedistanced）超过5000里的司机信息转移到一张称为seniordrivers 的表中,他们的详细情况被记录在表drivers 中，正确的sql为（）

```sql
select * into seniordrivers from drivers where drivedistanced >=5000
```

**题解**：

- `INSERT INTO` 语句用于**向表格中插入新的行**。

    ```sql
    -- 全量插入
    INSERT INTO table_name VALUES (值1, 值2,....)
    -- 指定所要插入数据的列：
    INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
    ```

- `SELECT INTO` 语句**从一个表中选取数据，然后把数据插入另一个表中**。常用于创建表的备份复件或者用于对记录进行存档。

    ```sql
    -- 把所有的列插入新表 
    SELECT *
    INTO new_table_name [IN externaldatabase] 
    FROM old_tablename
    
    -- 只把希望的列插入新表 
    SELECT column_name(s)
    INTO new_table_name [IN externaldatabase] 
    FROM old_tablename
    ```

    

## 题号3

运动会比赛信息的数据库，有如下三个表：
运动员ATHLETE（运动员编号 Ano，姓名Aname，性别Asex，所属系名 Adep）

项目 ITEM （项目编号Ino，名称Iname，比赛地点Ilocation）

成绩SCORE （运动员编号Ano，项目编号Ino，积分Score）。

写出目前总积分最高的系名及其积分，SQL语句实现正确的是：（   ）

```sql
SELECT Adep,SUM(Score)
	FROM ATHLETE, SCORE  
	WHERE ATHLETE.Ano=SCORE.Ano GROUP BY Adep  
	HAVING SUM(Score)>=ALL(SELECT SUM(Score) 
                           		FROM ATHLETE,SCORE  
                           		WHERE ATHLETE.Ano=SCORE.Ano GROUP BY Adep)
```

**注**：

All：对所有数据都满足条件，整个条件才成立；
Any：只要有一条数据满足条件，整个条件成立；
Some的作用和Any一样 .



## 题目 4

有一个名为app的MySQL数据库表，其建表语句如下：

```sql
CREATE TABLE `app` (
`app_id` int(10) DEFAULT '0',//应用ID
`version_code` int(10) DEFAULT '0',//应用的版本号
`download_count` int(10) DEFAULT '0'//当前版本的下载量
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4
```

当前表中数据记录如下，一条记录表示某个应用的某个版本的下载量记录：
+--------+--------------+----------------+
| app_id | version_code | download_count |
+--------+--------------+----------------+
|   1 |      10 |       90 |
|   1 |      11 |      100 |
|   1 |      10 |       20 |
|   2 |      15 |       10 |
|   2 |      16 |       15 |
|   2 |      17 |       30 |
|   2 |      16 |       5 |
|   3 |      2 |       50 |
+--------+--------------+----------------+

问： 下面那个MySQL语句可以查出**每个应用中总下载量最大的版本号和次数**（ ）？

```sql
SELECT t.app_id, t.version_code, MAX(t.download_sum) 
	FROM(SELECT app_id, version_code, SUM(download_count) download_sum 
         FROM app GROUP BY app_id, version_code ORDER BY download_sum DESC) AS t 
         GROUP BY t.app_id;
```

**题解**：

1，先按照哪个应用的具体哪个版号好类，`FROM app GROUP BY app_id, version_code`；

2，然后取出id，版本号，最关键的是按照聚类累加一下下载量并对其重命名，select app_id, version_code, sum(download_count) download_sum from app group by app_id, version_code；

3，之后对选出的数据按照下载量降序排序处理；select app_id, version_code, sum(download_count) download_sum from app group by app_id, version_code order by download_sum desc；

4，题目要求:**每个应用中**总下载量最大的版本号和次数，那么对整理后的新表重命名并按照应用id进行分类，(select app_id, version_code, sum(download_count) download_sum from app group by app_id, version_code order by download_sum desc) as t group by t.app_id

5，选出每一类（也就是每一个应用）中最大下载量的数据表信息。

Group by只保留分组后的第一行



## 题目 5：

1、处理效率：drop>trustcate>delete

2、drop删除整个表；trustcate删除全部记录，但不删除表；delete删除部分记录

3、delete不影响所用extent，高水线保持原位置不动；trustcate会将高水线复位。

















