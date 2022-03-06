# 索引问题

### 表结构

```mysql
CREATE TABLE `training_mysql_03_staffs` (
  `id` int(10) NOT NULL AUTO_INCREMENT,
  `name` varchar(10) DEFAULT NULL,
  `age` int(10) DEFAULT NULL,
  KEY `id_name_age_index` (`id`,`name`,`age`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 问题

> 1. 推断索引长度

请填写`___???___`的值

```
mysql > explain select * from training_mysql_03_staffs where id = 1 and name = "mai1"\G;
           id: 1
  select_type: SIMPLE
        table: training_mysql_03_staffs
         type: ref
possible_keys: id_name_age_index
          key: id_name_age_index
      key_len: ___???___
          ref: const,const
         rows: 1
        Extra: Using where; Using index
```

```
mysql > explain select * from training_mysql_03_staffs where id > 1 and   name ='mai1'  and age > 20\G;
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: training_mysql_03_staffs
         type: range
possible_keys: id_name_age_index
          key: id_name_age_index
      key_len: ___???___
          ref: NULL
         rows: 8
        Extra: Using where; Using index
```

### 填充数据

```bash
for i in $(seq 0 8); do
    seq -f "insert into training_mysql_03_staffs(name, age) values(\"mai$i\", 2%1g);" $i $i
done

```