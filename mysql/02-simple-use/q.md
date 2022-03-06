# 语句应用

### 表结构

```mysql
CREATE TABLE `training_mysql_02_customers` (
  `customer_id` varchar(255) DEFAULT NULL,
  `city` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `training_mysql_02_orders` (
  `order_id` int(11) NOT NULL AUTO_INCREMENT,
  `customer_id` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`order_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

### 问题

查询在`ShenZhen`并且订单量大于等于2单的公司

### 填充数据 
```mysql
INSERT INTO training_mysql_02_customers values ("163", "ShenZhen");
INSERT INTO training_mysql_02_customers values ("9you", "ShangHai");
INSERT INTO training_mysql_02_customers values ("baidu", "ShenZhen");
INSERT INTO training_mysql_02_customers values ("Thunder", "ShenZhen");

INSERT INTO training_mysql_02_orders(customer_id) values ("163");
INSERT INTO training_mysql_02_orders(customer_id) values ("163");
INSERT INTO training_mysql_02_orders(customer_id) values ("Thunder");
INSERT INTO training_mysql_02_orders(customer_id) values ("Thunder");
INSERT INTO training_mysql_02_orders(customer_id) values ("Thunder");
INSERT INTO training_mysql_02_orders(customer_id) values ("9you");
INSERT INTO training_mysql_02_orders values ();
```