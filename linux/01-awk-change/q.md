# 问题

现有问题内容如下`./q.log`

```
+-------------------+------------+------------+
| name              | birthday   | birth_day  |
+-------------------+------------+------------+
| LanphierXiaopeng  | 1964-02-28 | 2021-02-28 |
| DoeringMonique    | 1954-02-28 | 2021-02-28 |
| PeakOwen          | 1963-02-28 | 2021-02-28 |
| RusterholzBikash  | 1958-02-28 | 2021-02-28 |
| StasinskiFumitaka | 1956-02-29 | 2021-03-01 |
| HaddadiFei        | 1954-02-28 | 2021-02-28 |
| TaubmanRafols     | 1960-02-29 | 2021-03-01 |
| FargierMacha      | 1964-02-28 | 2021-02-28 |
| BenzakenJamaludin | 1960-02-29 | 2021-03-01 |
| GubskyNeven       | 1959-02-28 | 2021-02-28 |
+-------------------+------------+------------+
```

需通过linux命令(awk,sed等), 转换为以下内容

- 删除前三行与最后一行,
- 值改为`,`分割

```
LanphierXiaopeng,1964-02-28,2021-02-28
DoeringMonique,1954-02-28,2021-02-28
PeakOwen,1963-02-28,2021-02-28
RusterholzBikash,1958-02-28,2021-02-28
StasinskiFumitaka,1956-02-29,2021-03-01
HaddadiFei,1954-02-28,2021-02-28
TaubmanRafols,1960-02-29,2021-03-01
FargierMacha,1964-02-28,2021-02-28
BenzakenJamaludin,1960-02-29,2021-03-01
GubskyNeven,1959-02-28,2021-02-28
```