# Một số thẻ hay dùng trong html
## Thẻ `<ul>`,`<ol>`,`<li>`
- Thẻ `<ul>` là thẻ sắp xếp danh sách không có thứ tự
- Thẻ `<ol>` là thẻ sắp xếp danh sách có đánh số thứ tự từ 1 đến hết
### ví dụ:
```
<ul>
<li>Táo</li>
<li>Mận</li>
<li>Đào</li>
</ul>
```
![alt](/images/Screenshot_54.png)
```
<ol>
<li>Toán</li>
<li>Lý</li>
<li>Hóa</li>
</ol>
```
![alt](/images/Screenshot_55.png)
### Ta có thể thay đổi style trong thẻ `<li>`bằng cách thêm `list-style-type` vào thẻ `<ul>`
```
<ul style=”list-style-type: circle;”>
<li>Táo</li>
<li>Mận</li>
<li>Đào</li>
</ul>
```
- circle : chấm tròn nhạt
- square : chấm vuông đậm
- list-style-image : thêm hình ảnh mình tự làm và thêm `url` là đường dẫn của ảnh
```
<! DOCTYPE html >
<html>
<head>
</head>
<body>
<h2><u><strong>Mục tiêu nghề nghiệp:</strong></u></h2><br />
<ul>
<li><h3>Mục tiêu ngắn hạn:</h3>
<p>Trở thành nhân viên chính thức của công ty</p></li>
<li><h3>Mục tiêu dài hạn:</h3>
<p>Học được tất cả các kiếm thức liên quan về cloud</p></li>
</ul>
</body>
</html>
```
![alt](/images/Screenshot_56.png)
## Thẻ `<div>`
Thẻ `<div>` dùng để tạo các layer cho một trang web ,ta có thể hiểu là phân chia các khu vực của trang web
