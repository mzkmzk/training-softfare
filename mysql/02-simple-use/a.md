# Answer

```mysql
select a.customer_id, count(b.order_id) as count_order
    from training_mysql_02_customers as a
    left join training_mysql_02_orders as b
    on a.customer_id = b.customer_id
    where a.city = 'ShenZhen'
    group by a.customer_id
    having count(b.order_id) >= 2

```
