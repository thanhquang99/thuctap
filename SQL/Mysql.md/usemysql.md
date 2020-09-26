## MYSQL DATA DEFINITION
## USE
- Để chọn một c sở dữ liệu để làm việc bạn có thể dùng câu lênh use
```
USE database_name;
```
```
>mysql -u root -D classicmodels -p
```
Đây là lệnh chọn cơ sở dữ liệu khi bạn đăng nhập trong đó u là chìa khóa để miêu tả root p để miêu tả user còn D để miêu tả database name
## CREATE DATABASE
```
CREATE DATABASE [database-name];
```
đây là cấu trúc tạo database 

## DROP DATABASE
Để xóa bỏ database thì ta có thể dùng lệnh DROP
```
DROP DATABASE [IF EXISTS] database_name;
```
- IF EXISTS : đề phòng trường hợp không có database mà ta yêu cầu xóa
## SHOW DATABASES; : hiển thị database 
## MySQL CREATE TABLE
```
CREATE TABLE [IF NOT EXISTS] table_name(
   column_1_definition,
   column_2_definition,
   ...,
   table_constraints
) ENGINE=storage_engine;
```
ví dụ:
```
CREATE TABLE [IF NOT EXISTS] infoquang(
   name varchar(255) NOT NULL,
   mssv int(20) NOT NULL,
   date DATE,
   home varchar(255),
) ENGINE=INNODB;
```
- ở ví dụ này thì ta thấy `ENGINE=INNODB;` có ngĩa là ta chọn công cụ lưu trữ là INNODB 
- Một số lưu ý khi tạo bảng:

1. DEFAULT :mặc định một giá trị nào đó cho cột
2. AUTO_INCREMENT : tự động tăng giá trị cho cột đó