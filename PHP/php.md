# Tìm hiểu về PHP
## Định nghĩa 
- PHP (từ viết tắt đệ quy của PHP: Hypertext Preprocessor) là một ngôn ngữ kịch bản mã nguồn mở được sử dụng rộng rãi, đặc biệt thích hợp cho phát triển web và có thể được nhúng vào HTML.
- PHP là một ngôn ngữ kịch bản phía máy chủ được nhúng trong HTML. Nó được sử dụng để quản lý nội dung động, cơ sở dữ liệu, theo dõi phiên, thậm chí xây dựng toàn bộ các trang thương mại điện tử
- Nó được tích hợp với một số cơ sở dữ liệu phổ biến, bao gồm MySQL, PostgreSQL, Oracle, Sybase, Informix và Microsoft SQL Server.
## Ví dụ đơn giản
```
Bản thử trực tiếp
<html>
   
   <head>
      <title>Hello World</title>
   </head>
   
   <body>
      <?php echo "Hello, World!";?>
   </body>

</html>
```
## Escaping to PHP
### Thẻ chuẩn PHP
```
<?php...?>
```
### Nhận xét mã PHP
- PHP không nhạy cảm với khoảng trắng
- PHP phân biệt chữ hoa chữ thường
- Các câu lệnh là các biểu thức được kết thúc bằng dấu chấm phẩy
## Các loại biến PHP
-Tất cả các biến trong PHP được biểu thị bằng một ký hiệu đô la đứng đầu ($).

-Giá trị của một biến là giá trị của lần gán gần đây nhất.

-Các biến được gán với toán tử =, với biến ở bên trái và biểu thức được đánh giá ở bên phải.

-PHP có tổng cộng tám kiểu dữ liệu
- Integers : số nguyên
- Doubles :là các số dấu phẩy động, như 3,14159 hoặc 49,1.
- Booleans :chỉ có hai giá trị có thể có hoặc đúng hoặc sai.
- NULL :là một kiểu đặc biệt chỉ có một giá trị: NULL.
- Strings : là chuỗi ký tự, giống như 'PHP hỗ trợ hoạt động chuỗi.'
- Arrays :Mảng - là tập hợp được đặt tên và lập chỉ mục của các giá trị khác
- Objects :Đối tượng - là các thể hiện của các lớp do người lập trình xác định, có thể đóng gói cả các loại giá trị và hàm khác dành riêng cho lớp đó.
- Resources :Tài nguyên - là các biến đặc biệt chứa các tham chiếu đến các tài nguyên bên ngoài PHP (chẳng hạn như các kết nối cơ sở dữ liệu).
### ví dụ về document
```
<?php
   $channel =<<<_XML_
   
   <channel>
      <title>What's For Dinner</title>
      <link>http://menu.example.com/ </link>
      <description>Choose what to eat tonight.</description>
   </channel>
   _XML_;
   
   echo <<<END
   This uses the "here document" syntax to output multiple lines with variable 
   interpolation. Note that the here document terminator must appear on a line with 
   just a semicolon. no extra whitespace!
   

   END;
   
   print $channel;
?>
```
```
This uses the "here document" syntax to output
multiple lines with variable interpolation. Note
that the here document terminator must appear on a
line with just a semicolon. no extra whitespace!

<channel>
<title>What's For Dinner<title>
<link>http://menu.example.com/<link>
<description>Choose what to eat tonight.</description>
```
- Ở đây ta thấy khi biến channel khi được gọi nó sẽ in tất cả các thứ trong biến channel
```
<<<[tên-biến]

[tên-biến];
```
## Hàm hằng
- Hằng số là tên hoặc mã định danh cho một giá trị đơn giản. Một giá trị không đổi không thể thay đổi trong quá trình thực thi tập lệnh.
- Để xác định một hằng số, bạn phải sử dụng hàm define () và không cần $ để truy suất biến
```
<?php
   define("MINSIZE", 50);
   
   echo MINSIZE;
?>
```
