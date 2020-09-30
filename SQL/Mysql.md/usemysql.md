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
## PRIMARY KEY 
- Là cột hoặc tập hợp hợp các cột xác định duy nhất mỗi hàng trong bảng 
- các giá trị primary key không được nhận giá trị null
- Chỉ có duy nhất một primary key trong một bảng
```
CREATE TABLE table_name(
    primary_key_column1 datatype,
    primary_key_column2 datatype,
    ...,
    PRIMARY KEY(column_list)
);
```
ví dụ:
```
CREATE TABLE users(
   user_id INT AUTO_INCREMENT PRIMARY KEY,
   username VARCHAR(40),
   password VARCHAR(255),
   email VARCHAR(255)
);
```
Ta thấy ở ví dụ trên thì user_id chính là primary key

## foreign key
- foreign key là một cột hoặc nhóm cột trong bảng liên kết với một cột hoặc nhóm cột trong bảng khác.
```
CREATE TABLE bang_con
 (
  cot1 kieudulieu [ NULL | NOT NULL ],
  cot2 kieudulieu [ NULL | NOT NULL ],
  …
 
  CONSTRAINT fk_ten
   FOREIGN KEY (cot_con1, cot_con2, … cot_con_n)
   REFERENCES bang_me (cot_me1, cot_me2, … cot_me_n)
 );
 ```
 ví dụ :
 ```
 CREATE TABLE categories(
    categoryId INT AUTO_INCREMENT PRIMARY KEY,
    categoryName VARCHAR(100) NOT NULL
) ENGINE=INNODB;

CREATE TABLE products(
    productId INT AUTO_INCREMENT PRIMARY KEY,
    productName varchar(100) not null,
    categoryId INT,
    CONSTRAINT fk_category
    FOREIGN KEY (categoryId) 
        REFERENCES categories(categoryId)
) ENGINE=INNODB;
```
Ở ví dụ này ta thấy rằng categoryId sẽ được lấy thông tin từ bảng categories

##  MySQL Storage Engines
- Chúng ta sẽ tìm hiểu các công cụ lưu trữ trong MySQL để sử dụng một cách hiệu quả và tối ưu hóa cơ sở dữ liêụ của mình 
- Các công cụ lưu trữ trong MySQl :
1. MyISAM

MyISAM mở rộng công cụ lưu trữ ISAM trước đây.Các bảng MyISAM được tối ưu hóa về tốc độ và nén dữ liệu

Kích thước của MyISAM có thể lên tới 256TB. Nó giới hạn hiệu suất đọc và viết dữ liệu vì vậy nó thường dùng chỉ để đọc dữ liệu .Các bảng MyISAM không an toàn cho giao dịch.

Từ bản 5.5 về trước thì nó là công cụ lưu trữ mặc định còn các bản về sau thì là InnoDB

2. InnoDB

Các bảng InnoDB hỗ trợ cho đầy đủ các giao dịch và hỗ trợ ACID .Ngoài ra còn hỗ trợ các  foreign keys, commit, rollback, roll-forward 

Kích cỡ của bảng có thể lên đến 64TB

3. MERGE

Bảng MERGE là một bảng ảo kết hợp nhiều bảng MyISAM có cấu trúc tương tự như một bảng.

MySQL chỉ cho phép bạn thực hiện các thao tác SELECT,DELETE,UPDATE,INSERT cho bảng MERGE

Nếu sử dụng DROP thì bảng MERGE sẽ bị xóa và không ảnh hưởng gì tới các bảng khác mà nó lấy dữ liệu

4. Memory

Lưu trữ tất cả dữ liệu trong RAM để có thể truy suất nhanh kết quả .Engine này trước đây gọi là HEAP Engine.Nhưng giờ được sử dụng ít dần đi do InnoDB chiếm lợi thế hơn

5. Archive
