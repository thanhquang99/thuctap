# các loại dữ liệu được sử dụng trong Mysql 
## BIT 
- Các bit cho phép bạn lưu trữ giá trị bit dưới cú pháp :
```
BIT(n)
```
- n có giá trị từ 1-64 .Khi n=1 thì ta có thể không viết
- ta có thể chỉ định giá trị củ một kí tự vói giá trị bit 
```
b01
B11
```
có nghĩa là kí tự b có giá tri 01 và kí tự B có giá trị 11
## BOOLEAN 
- MySQL không cung cấp BOOLEAN hoặc BOOL mà nó sử dụng giống như TINYINT(1) để thay thế . BOOLEAN thường mang các giá trị TRUE hoặc FALSE tương ứng với 1 và 0 
- Nếu bạn muốn xuất ra kết quả TRUE hoặc FALSE thì có thể sử dụng câu lệnh IF
```
SELECT 
    IF(completed, 'true', 'false') completed
```
Trong đó completed là tên cột mangh giá trị BOOLEAN
## CHAR
- CHAR dữ liệu kí tự có độ dài mà chúng ta cần khai báo, nếu khai báo không hết thì khoẳng trắng sẽ được sử dụng để lấp đầy . NÓ có độ dài từ 1-255

VD: name char(20): cột name có kiểu dữ liệu là kí tự và có độ dài là 20 
- ta có thể sử dụng LENGTH để lấy độ dài của mỗi char giá trị (không tính khoảng trắng)
- Khi so sánh các char MySQL sẽ không tính đến khoảng trắng còn LIKE thì lại có 
## DATE AND DATE FUNCTION 
- DATE là một dạng dữ liệu quản lí ngày tháng năm ,nó có dạng : `yyyy-mm-dd` và đây là định dạng chuẩn không thể thay đổi
- NOW(): là hàm để lấy ngày và giờ hiện tại
- DATE(NOW()) : là hàm để lấy ngày hiện tại và không lấy giờ
- CURDATE(): lấy ngày hệ thống hiện tại
- DATE_FORMAT(CURDATE(), '%m/%d/%Y') : ta dùng để định dạng ngày tháng mà ta hiển thị ra ngoài (lưu ý: nhập vào ngày tháng thì không thể thay đổi định dạng.)
- DATEDIFF : để tính toán khoảng cách giữa hai ngày
-  DATE_ADD : để thêm một số ngày ,tuàn tháng ,năm vào giá trị ngày 
```
SELECT 
    '2015-01-01' start,
    DATE_ADD('2015-01-01', INTERVAL 1 DAY) 'one day later',
    DATE_ADD('2015-01-01', INTERVAL 1 WEEK) 'one week later',
    DATE_ADD('2015-01-01', INTERVAL 1 MONTH) 'one month later',
    DATE_ADD('2015-01-01', INTERVAL 1 YEAR) 'one year later';
```
-  DATE_SUB : dùng để giảm bớt giá trị thời gian
## DATETIME :
- Datetime có kiểu định dạng : YYYY-MM-DD HH:MM:SS
## DECIMAL : 
- được sử dụng để lưu trữ giá trị số thập phân trong cơ sở dữ liệu:
```
column_name  DECIMAL(P,D);
```
- trong đó P: biểu thị chính xác chữ số có nghĩa còn D thể hiện số chữ số sau dấu thập phân (D<=P). Ta có thể hiểu rằng cột có thể lưu trữ tối đa P chữ số và D chữ số thập phân
## ENUM : 
- ENUM là một chuỗi giá trị mà ta đã có sẵn mà cái có sẵn ở đây là do taọ ra 
```
CREATE TABLE table_name (
    ...
    col ENUM ('value1','value2','value3'),
    ...
);
```
```
CREATE TABLE tickets (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    priority ENUM('Low', 'Medium', 'High') NOT NULL
);
```
cột priority chỉ lấy được 3 giá trị Low, Medium, High

## INT : 
kiểu số nguyên 
## JSON :


## VARCHAR : 
- tương tự như CHAR nhưng có dung lượng lớn hơn nhiều so với nó.
