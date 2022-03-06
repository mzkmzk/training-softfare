# Answer

```bash
sed  '1,3d;$d' q.log  | awk -F ' ' '{print $2  "," $4 "," $6} '
```

## 参考链接

- https://blog.csdn.net/lijing742180/article/details/85176056
- https://cloud.tencent.com/developer/article/1659432