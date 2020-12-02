# Mysql workbanch là gì ?
Mysql workbanch là một chương trình giúp người dùng tương tác với  mysql bằng giao diện ma mà không cần phải tháo tác bằng các câu lệnh phức tạp
## phân quyền user 
- để có thể truy cập trực tiếp vào thì ta phải tạo và phân quyền cho user
```
 CREATE USER 'thanhquang'@'%' IDENTIFIED BY 'Khuongquang99';
 GRANT ALL PRIVILEGES ON * . * TO 'thanhquang'@'%';
 FLUSH PRIVILEGES;
 ```
- Kiểm tra user vừa tạo
```
mysql> select User,Host from mysql.user;
```

## Cài đặt Mysql workbanch
[cài Mysql workbanch tại đây](https://dev.mysql.com/downloads/workbench/)
## Hướng dẫn sử dụng Mysql workbanch
1. Tạo connection

![alt](/images/Screenshot_15.png)


2. một số thao tác cơ bản của mysql workbanch

- hướng dẫn xem bảng liên kết trong database

Bấm tổ hợp phím `ctrl +R`

![alt](/images/Screenshot_18.png)
sau đó ta tiếp tục bấm next
![alt](/images/Screenshot_19.png)
