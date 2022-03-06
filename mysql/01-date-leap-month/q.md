## 找用户最近的生日日期

### 表结构

```mysql
CREATE TABLE `training_mysql_01_employees` (
  `first_name` varchar(255) DEFAULT NULL,
  `last_name` varchar(255) DEFAULT NULL,
  `birthday` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

### 填充数据
```mysql
INSERT INTO `training_mysql_01_employees` VALUES ('mai','0','1960-02-28 00:00:00');
INSERT INTO `training_mysql_01_employees` VALUES ('mai','1','1961-02-28 00:00:00');
INSERT INTO `training_mysql_01_employees` VALUES ('mai','2','1962-02-28 00:00:00');
INSERT INTO `training_mysql_01_employees` VALUES ('mai','3','1963-02-28 00:00:00');
INSERT INTO `training_mysql_01_employees` VALUES ('mai','4','1964-02-28 00:00:00');
INSERT INTO `training_mysql_01_employees` VALUES ('mai','8','1968-02-29 00:00:00');
```

### 问题

根据某个用户的出生日期和当前日期, 计算他最近的生日, 问题是如何正确处理闰月

在生日问题中, 一般对闰月29号生日的处理如下:

如果是闰月, 那么返回2月29日
如果不是闰月, 则返回3月1日

假设当前时间是`2020-03-05 00:00:00`, 需返回内容

```
+--------------+---------------------+---------------------+---------------------+
| name         | birthday            | today               | next_birthday       |
+--------------+---------------------+---------------------+---------------------+
| first_name 0 | 1960-02-28 00:00:00 | 2020-03-05 00:00:00 | 2021-02-28 00:00:00 |
| first_name 1 | 1961-02-28 00:00:00 | 2020-03-05 00:00:00 | 2021-02-28 00:00:00 |
| first_name 2 | 1962-02-28 00:00:00 | 2020-03-05 00:00:00 | 2021-02-28 00:00:00 |
| first_name 3 | 1963-02-28 00:00:00 | 2020-03-05 00:00:00 | 2021-02-28 00:00:00 |
| first_name 4 | 1964-02-28 00:00:00 | 2020-03-05 00:00:00 | 2021-02-28 00:00:00 |
| first_name 8 | 1968-02-29 00:00:00 | 2020-03-05 00:00:00 | 2021-03-01 00:00:00 |
+--------------+---------------------+---------------------+---------------------+
```

### other

> 生成填充数据语句

```bash
for i in $(seq 0 4); do
    seq -f "insert into training_mysql_01_employees values(\"mai\", \"$i\", \"196%1g-02-28\");" $i $i
done
for i in $(seq 5 9); do
    seq -f "insert into training_mysql_01_employees values(\"mai\", \"$i\", \"196%1g-02-29\");" $i $i
done
```
生成语句后有些年份无2月29号, 导致插入数据的birthday为`0000-00-00 00:00:00`, 需手动删除

```mysql
mysql> delete from training_mysql_01_employees where birthday='0000-00-00 00:00:00'
```