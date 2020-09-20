# Basic MySQL Tutorial
1. Bắt đầu với Mysql
- cài đặt máy chủ cơ sở dữ liệu với Mysql

2. Truy vấn dữ liệu

chúng ta sẽ sử dụng câu lệnh SELECT cơ bản để truy vấn dữ liệu từ một bảng
```
SELECT [select_list] FROM [table_name];
```
3. Sắp xếp dữ liệu

để sắp xếp dữ liệu đầu ra khi chúng ta sử dụng select thì ta có thể dùng `order by `

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
trong đó asc là sắp xếp tăng dần còn desc là săp xếp giảm dần 

4. lọc dữ liệu
- WHERE - học cách sử dụng WHERE mệnh đề để lọc các hàng dựa trên các điều kiện đã chỉ định.
- SELECT DISTINCT - chỉ cho bạn cách sử dụng DISTINCT toán tử trong SELECT câu lệnh để loại bỏ các hàng trùng lặp trong một tập kết quả.
- AND  - giới thiệu với bạn AND toán tử kết hợp các biểu thức logiclogic để tạo thành một điều kiện phức tạp để lọc dữ liệu.
- OR - giới thiệu cho bạn OR toán tử và chỉ cho bạn cách kết hợp OR toán tử với AND toán tử để lọc dữ liệu.
- IN  - chỉ cho bạn cách sử dụng IN toán tử trong WHERE mệnh đề để xác định xem một giá trị có khớp với bất kỳ giá trị nào trong danh sách hoặc truy vấn con hay không.
- BETWEEN  - chỉ cho bạn cách truy vấn dữ liệu dựa trên một phạm vi sử dụng BETWEEN toán tử.
- LIKE   - cung cấp cho bạn kỹ thuật truy vấn dữ liệu dựa trên một mẫu cụ thể.
 - LIMIT - sử dụng  LIMIT để hạn chế số hàng được trả về bởi SELECT câu lệnh
- IS NULL - kiểm tra xem một giá trị có NULL hay không bằng cách sử dụng IS NULL toán tử.
```
SELECT 
    select_list
FROM
    table_name
WHERE
    search_condition;
```
5. Nối các bảng
