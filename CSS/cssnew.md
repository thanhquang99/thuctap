# Cascading Style Sheets
## Định nghĩa
- CSS (Cascading Style Sheets):mô tả cách các phần tử HTML được hiển thị trên màn hình, giấy hoặc trong các phương tiện khác
- CSS có thể kiểm soát bố cục nhiều trang web một lúc
- Các bảng định kiểu bên ngoài được lưu trữ trong các tệp CSS
ví dụ
```
body {
  background-color: lightblue;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: verdana;
  font-size: 20px;
}
```
## Cú pháp CSS
```
selector {Declaration}
```
## Bộ chọn CSS
Bộ chọn CSS được sử dụng để "tìm" (hoặc chọn) các phần tử HTML bạn muốn tạo kiểu.

### Bộ chọn phần tử CSS
```
p {
  text-align: center;
  color: red;
}
```
Bộ chọn phần tử chọn các phần tử của html dựa trên tên phần tử và không có thêm kí hiệu gì trước tên phần tử
### Bộ chọn ID
```
#para1 {
  text-align: center;
  color: red;
}
```
- Bộ chọn id sử dụng thuộc tính id của một phần tử HTML để chọn một phần tử cụ thể.

- có thêm kí tự `#` trước thuộc tính
### Bộ chọn lớp 
```
.center {
  text-align: center;
  color: red;
}
```
- Bộ chọn lớp chọn các phần tử HTML với một thuộc tính lớp cụ thể.
- có thêm kí tự `.` trước thuộc tính
```
p.center {
  text-align: center;
  color: red;
}
```
- Trong ví dụ này, chỉ các phần tử <p> có class = "center" mới được căn giữa: 
### Bộ chọn chung
```
* {
  text-align: center;
  color: blue;
}
```
### Bộ chọn nhóm
```
h1, h2, p {
  text-align: center;
  color: red;
}
```
- Tất cả các phần tử h1,h2,p viết ở giữa và có màu đỏ
## Cách thêm CSS
### CSS bên ngoài
Kiểu bên ngoài được xác định trong phần tử `<link>`, bên trong phần `<head>` của trang HTML:
```
<!DOCTYPE html>
<html>
<head>
<link rel="stylesheet" href="mystyle.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```
Đây là nội dung trong file mystyle.css
```
body {
  background-color: lightblue;
}

h1 {
  color: navy;
  margin-left: 20px;
}
```

### CSS nội bộ
```
<!DOCTYPE html>
<html>
<head>
<style>
body {
  background-color: linen;
}

h1 {
  color: maroon;
  margin-left: 40px;
}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```
- Ta dùng thẻ `style` để định nghĩa các thuộc tính dùng CSS và viết ở thẻ `head`
### CSS nội tuyến
```
<!DOCTYPE html>
<html>
<body>

<h1 style="color:blue;text-align:center;">This is a heading</h1>
<p style="color:red;">This is a paragraph.</p>

</body>
</html>
```
- Đây là kiểu CSS được dùng một lần cho phần tử duy nhất được chọn đó và nội dung CSS được viết trong thẻ cần CSS
## Border CSS
- dotted - Xác định đường viền chấm
- dashed - Xác định đường viền đứt nét
- solid - Xác định đường viền chắc chắn
- double - Xác định đường viền kép
- groove- Xác định đường viền có rãnh 3D. Hiệu ứng phụ thuộc vào giá trị màu viền
- ridge- Xác định đường viền 3D. Hiệu ứng phụ thuộc vào giá trị màu viền
- inset- Xác định đường viền in 3D. Hiệu ứng phụ thuộc vào giá trị màu viền
- outset- Xác định đường viền ban đầu 3D. Hiệu ứng phụ thuộc vào giá trị màu viền
- none - Xác định không có đường viền
- hidden - Xác định một đường viền ẩn
### Lề CSS 
CSS có các thuộc tính để chỉ định lề cho mỗi bên của phần tử:
- margin-top
- margin-right
- margin-bottom
- margin-left
```
p {
  margin: 25px 50px 75px 100px;
}
```
- các chỉ số được tính theo thứ tự top,right,bottom,left
### Các mặt riêng lẻ CSS
Thuộc paddingtính CSS được sử dụng để tạo không gian xung quanh nội dung của phần tử, bên trong bất kỳ đường viền xác định nào.

### overflow
- dùng để cố định kích thước nội dung hiển thị 
- visible- Mặc định. Phần tràn không được cắt bớt. Nội dung hiển thị bên ngoài hộp của phần tử
- hidden - Phần tràn bị cắt bớt và phần còn lại của nội dung sẽ không hiển thị
- scroll - Phần tràn được cắt bớt và một thanh cuộn được thêm vào để xem phần còn lại của nội dung
- auto- Tương tự như scroll, nhưng nó chỉ thêm thanh cuộn khi cần thiết
### float
- float dùng để định dạng xem phần tử đó được nối tiếp với phần tử trước như nào bên trái hay phải,...
- left - Phần tử nổi ở bên trái vùng chứa của nó
- right - Phần tử nổi ở bên phải vùng chứa của nó
- none - Phần tử không nổi (sẽ được hiển thị ngay tại nơi nó xuất hiện trong văn bản). Đây là mặc định
- inherit - Phần tử kế thừa giá trị float của phần tử cha của nó
