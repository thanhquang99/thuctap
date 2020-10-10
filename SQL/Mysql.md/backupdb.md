# Backup và Restore MySQL
---
## Backup thông qua MySQL Dump - `mysqldump`
> Đây là các CMD SHELL trên Linux
### Backup toàn bộ DB
```
mysqldump -u [uname] -p [tên db] > [file backup].sql
```
### Backup toàn bộ DB
```
mysqldump -u [uname] -p --all-databases > [file backup].sql
```
### Backup tables chỉ định
```
mysqldump -u [uname] -p [tên db] [table1] [table2] > [file backup].sql
```
### Backup + nén sang dạng gzip
```
mysqldump -u [uname] -p [tên db] | gzip >  [file backup].sql.gz
```

## Restore file backup

Lưu ý : để làm được điều này ta cần phải vào trong mysql và tạo ra một database xong rồi import vào

```
mysql -u [uname] -p [dbname] < [backupfile.sql]
```