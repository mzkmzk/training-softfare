# 索引问题

### 表结构

```mysql
CREATE TABLE `training_mysql_03_staffs` (
  `id` int(10) DEFAULT NULL,
  `name` char(10) DEFAULT NULL,
  `age` int(10) DEFAULT NULL,
  KEY `id_name_age_index` (`id`,`name`,`age`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 填充数据