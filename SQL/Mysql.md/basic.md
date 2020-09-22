# Thao tác dữ liệu Mysql
1. SELECT Câu SELECTlệnh cho phép bạn đọc dữ liệu từ một hoặc nhiều bảng. Để viết một SELECTcâu lệnh trong MySQL, bạn làm theo cú pháp sau:
```
SELECT select_list
FROM table_name;
```
2. ORDER BY : Khi bạn sử dụng select để truy vấn dữ liệu nó sẽ không được sắp xếp theo trình tự nào nhưng khi ta sử dụng câu lệnh order by nó sẽ sắp xếp theo ý định mà ta mong muốn
```
SELECT 
   select_list
FROM 
   table_name
ORDER BY 
   column1 [ASC|DESC], 
   column2 [ASC|DESC],
   ...;
   ```
   Các ASCviết tắt của tăng dần và các  DESCviết tắt của giảm dần. Bạn sử dụng ASCđể sắp xếp tập kết quả theo thứ tự tăng dần và DESCsắp xếp tập kết quả theo thứ tự giảm dần.

   Nghĩa là các cột có thể sắp xếp theo ý tưởng của chúng ta

3. WHERE : Cho phép bạn chỉ định một điều kiện trả về với sự truy vấn của bạn
```
SELECT 
    select_list
FROM
    table_name
WHERE
    search_condition;
```
4. SELECT DISTINCT:Khi truy vấn dữ liệu từ một bảng, bạn có thể nhận được các hàng trùng lặp. Để loại bỏ các hàng trùng lặp này, bạn sử dụng DISTINCT mệnh đề trong SELECTcâu lệnh.
```
SELECT DISTINCT
    select_list
FROM
    table_name;
```
5. AND : khi chúng ta muón kết hợp hai điều kiện cùng thỏa mãn lại với nhau .

Ví dụ như khi ta dùng where mà muốn kết hợp 2 điều kiện lại

6. OR : tương tự như AND nhưng mà ở đây chỉ cần 1 trong 2 điều kiện đúng là được

7. IN : 
```
SELECT 
    column1,column2,...
FROM
    table_name
WHERE 
	(expr|column_1) IN ('value1','value2',...);
```
như ví dụ minh họa trên ta có thể sử chọn chính xác các biến mà ta muốn hiện 
8. BETWEEN - AND : cho phép ta xác định vùng giớ hạn nằm giữ 2 giá trị mà ta đã nêu

```
expr [NOT] BETWEEN begin_expr AND end_expr;
```
9. LIKE : Tìm kiếm sự giống nhau
```
SELECT 
    employeeNumber, 
    lastName, 
    firstName
FROM
    employees
WHERE
    firstName LIKE 'a%';
```
như ở ví dụ trên ta tìm kiếm ai có firstname bắt đầu bằng chữ a

- Ký %tự đại diện phần trăm khớp với bất kỳ chuỗi nào không hoặc nhiều ký tự.
- Ký _tự đại diện gạch dưới khớp với bất kỳ ký tự đơn nào.
10. LIMIT : hạn chế só lương hiển thị ra. Ta có thể giói hạn limit là 1,2,3...

```
SELECT 
    select_list
FROM
    table_name
LIMIT 
```
11. IS NULL : là một toán tử so sánh xem có trống hay không. Ta có thể chỉ truy suất nhưng vales trống hoặc không(IS NOT NULL)

12. ALIAS :bí danh 
```
SELECT 
   [column_1 | expression] AS descriptive_name
FROM table_name;
```
```
SELECT
   CONCAT_WS(', ', lastName, firstname) AS `Full name`
FROM
   employees;
```
ta đã đặt bí danh để gộp nhiều hàng lại

13. JOIN :Nhiều lúc 1 bẳng là không đủ dữ liệu để sử dụng nên ta có thể dùng câu lệnh join để nối các bảng lại với nhau
```
SELECT column_list
FROM table_1
INNER JOIN table_2 ON join_condition;
```
Nếu điều kiện nối sử dụng toán tử bằng ( =) và tên cột trong cả hai bảng được sử dụng để so khớp là giống nhau, bạn có thể sử dụng USINGmệnh đề thay thế:
```
SELECT column_list
FROM table_1
INNER JOIN table_2 USING (column_name);
```
- LEFT JOIN : nó sẽ trả về bảng mà bắt đầu từ bảng 1 và kết quả phù hợp của bảng 2
- RIGHT JOIN : nó sẽ trả về bảng mà bắt dầu từ bảng 2 và kết quả phù hợp của bangr 1
```
SELECT column_list 
FROM table_1 
LEFT JOIN table_2 USING (column_name);
```
```
SELECT column_list 
FROM table_1 
RIGHT JOIN table_2 ON join_condition;
```
- CROSS JOIN : mỗi hàng của bảng thứ nhất sẽ được kết nối với mỗi hàng bảng thứ 2 . Nó sẽ lấy tất cả dòng bảng 1 kết hợp với lần lượt dòng trong bảng 2,
14. GROUP BY :với câu lệnh này nó giúp bạn tập hợp các cột hay dòng lại thành một group 
```
SELECT 
    c1, c2,..., cn, aggregate_function(ci)
FROM
    table
WHERE
    where_conditions
GROUP BY c1 , c2,...,cn;
```
15. HAVING : tương tự như where nó dùng để lọc điều kiện dùng trong GROUP 
```
SELECT 
    select_list
FROM 
    table_name
WHERE 
    search_condition
GROUP BY 
    group_by_expression
HAVING 
    group_condition;
```
16. Subquery : truy vấn con này sẽ được thực hiện trước và từ đó để làm dữ liệu cho truy ngoài thực hiện các bước lọc dữ liệu tiếp
```
SELECT 
    lastName, firstName
FROM
    employees
WHERE
    officeCode IN (SELECT 
            officeCode
        FROM
            offices
        WHERE
            country = 'USA');
```
Ở ví dụ này truy vấn con sẽ chọn officecode có country =usa để làm dữ liệu cho truy vấn lastname và firstname của những nhân viên có country =usa

18. INSERT : Câu INSERTlệnh cho phép bạn chèn một hoặc nhiều hàng vào bảng
```
INSERT INTO table(c1,c2,...)
VALUES (v1,v2,...);
```
Chúng ta sẽ chèn cột1 và cột2 vào với giá trị v1 v2
- chèn nhiều hàng : 
```
INSERT INTO table(c1,c2,...)
VALUES 
    (v1,v2,...),
    (v1,v2,...);
```
- Bên cạnh việc sử dụng các giá trị hàng trong VALUESmệnh đề, bạn có thể sử dụng kết quả của một SELECTcâu lệnh làm nguồn dữ liệu cho INSERTcâu lệnh.
```
INSERT INTO table_name(column_list)
SELECT 
   select_list 
FROM 
   another_table
WHERE
   condition;
```
19. UPDATE :

Câu UPDATElệnh cập nhật dữ liệu trong một bảng. Nó cho phép bạn thay đổi các giá trị trong một hoặc nhiều cột của một hàng hoặc nhiều hàng.
```
UPDATE [LOW_PRIORITY] [IGNORE] table_name 
SET 
    column_name1 = expr1,
    column_name2 = expr2,
    ...
[WHERE
    condition];
```
sau đâylaf ví dụ về update mail mới của nhân viên
```
UPDATE employees 
SET 
    email = 'mary.patterson@classicmodelcars.com'
WHERE
    employeeNumber = 1056;
```
20. DELETE :Dùng để xóa dữ liệu khỏi bảng
```
DELETE FROM table_name
WHERE condition;
```
21. REPLACE

Dùng đê chèn một hàng mới trong bảng
```
REPLACE [INTO] table_name(column_list)
VALUES(value_list);
```
ở ví dụ sau ta sẽ chèn thêm dân số của một số thành phố vào :
```
CREATE TABLE cities (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    population INT NOT NULL
);

INSERT INTO cities(name,population)
VALUES('New York',8008278),
	  ('Los Angeles',3694825),
	  ('San Diego',1223405);
```
