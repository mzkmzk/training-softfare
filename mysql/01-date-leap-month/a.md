# Answer

知识点:

mysql中使用`date_add`如果遇到了不存在的`2月29`, 会当做2月28日处理, 如果存在则当2月29日处理

```mysql
mysql> select date_add('2016-02-29 22:51:00', interval -1 year),
    -> date_add('2016-02-29 22:51:00', interval 4 year);
+---------------------------------------------------+--------------------------------------------------+
| date_add('2016-02-29 22:51:00', interval -1 year) | date_add('2016-02-29 22:51:00', interval 4 year) |
+---------------------------------------------------+--------------------------------------------------+
| 2015-02-28 22:51:00                               | 2020-02-29 22:51:00                              |
+---------------------------------------------------+--------------------------------------------------+
1 row in set (0.00 sec)
```

但是我们现在想做的是假如遇到了不存在的2月29, 需要当做3月1日处理

步骤:

- 查询今年当年多少岁
- 按mysql逻辑计算今年的生日日期
- 因为mysql当非闰年时, 生日为2月29号的则会被改为2月28日, 所以需要进行判断是否需要加一天
- 查看今年生日是否已过, 如果是则取明年的生日

```mysql
//查询今年当年多少岁
select concat("first_name", ' ', last_name) as name,
        (year('2020-03-05 00:00:00') - year(birthday)) as diff,
        birthday,
        '2020-03-05 00:00:00' as today
    from training_mysql_01_employees;
```

```mysql
//按mysql逻辑计算今年的生日日期
select name,
    date_add(birthday, interval diff year) as cur,
    date_add(birthday, interval diff + 1 year) as next,
    birthday
 from (
    select concat("first_name", ' ', last_name) as name,
            (year('2020-03-05 00:00:00') - year(birthday)) as diff,
            birthday,
            '2020-03-05 00:00:00' as today
        from training_mysql_01_employees
  ) as a;
```

```mysql
// 因为mysql当非闰年时, 生日为2月29号的则会被改为2月28日, 所以需要进行判断是否需要加一天
select 
    name,
    birthday,
    today,
    date_add(cur, interval if (month(birthday)=2 && day(birthday)=29 && day(cur)=28, 1, 0) day) as cur,
    date_add(next, interval if (month(birthday)=2 && day(birthday)=29 && day(next)=28, 1, 0) day) as next
    from (
        select name,
            today,
            date_add(birthday, interval diff year) as cur,
            date_add(birthday, interval diff + 1 year) as next,
            birthday
        from (
            select concat("first_name", ' ', last_name) as name,
                    (year('2020-03-05 00:00:00') - year(birthday)) as diff,
                    birthday,
                    '2020-03-05 00:00:00' as today
                from training_mysql_01_employees
        ) as a
    ) as b;
```

```mysql
// 查看今年生日是否已过, 如果是则取明年的生日
select 
    name,
    birthday,
    today,
    if (cur>today, cur, next ) as next_birthday 
    from (
        select 
            name,
            birthday,
            today,
            date_add(cur, interval if (month(birthday)=2 && day(birthday)=29 && day(cur)=28, 1, 0) day) as cur,
            date_add(next, interval if (month(birthday)=2 && day(birthday)=29 && day(next)=28, 1, 0) day) as next
            from (
                select name,
                    today,
                    date_add(birthday, interval diff year) as cur,
                    date_add(birthday, interval diff + 1 year) as next,
                    birthday
                from (
                    select concat("first_name", ' ', last_name) as name,
                            (year('2020-03-05 00:00:00') - year(birthday)) as diff,
                            birthday,
                            '2020-03-05 00:00:00' as today
                        from training_mysql_01_employees
                ) as a
            ) as b
    ) as c ;
    
```