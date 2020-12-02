# HTML(Hypertext Markup Language)
HTML là chữ viết tắt của Hypertext Markup Language. Nó giúp người dùng tạo và cấu trúc các thành phần trong trang web hoặc ứng dụng, phân chia các đoạn văn, heading, links, blockquotes, vâng vâng.

HTML không phải là ngôn ngữ lập trình, đồng nghĩa với việc nó không thể tạo ra các chức năng “động” được. Nó chỉ giống như Microsoft Word, dùng để bố cục và định dạng trang web.

Khi làm việc với HTML, chúng ta sẽ sử dụng cấu trúc code đơn giản (tags và attributes) để đánh dấu lên trang web. Ví dụ, chúng ta có thể tạo một đoạn văn bằng cách đặt văn bản vào trong cặp tag mở và đóng văn bản `<p>` và `</p>`
# TAG
## Cấu trúc cơ bản của HTML:
```
<head>
    <title>Tiêu đề của trang web</title>
</head>
<body>
    Phần trình bày nội dung
</body>
</html>
```
ta thấy tag head dùng để hiển thị ở menubar còn tag body sẽ là nơi mô tả những gì hiển thị của trang web
## Các thẻ cơ bản trong HTML
Một tài liệu HTML được tạo nên từ các cặp thẻ html

- Thẻ được bắt đầu bằng dấu < và kết thúc bằng dấu >
- Tên thẻ nằm giữa cặp dấu <>
### Các thẻ tiêu đề (HTML Headings):
- Bao gồm các thẻ từ `<h1>` đến `<h6>`
```
<h1>Content of tag h1</h1>
<h2>Content of tag h2</h2>
<h3>Content of tag h3</h3>
<h4>Content of tag h4</h4>
<h5>Content of tag h5</h5>
<h6>Content of tag h6</h6>
```
### Đoạn văn bản trong html (HTML Paragraphs):
- Nội dung văn bản được thể hiện trong cặp thẻ `<p></p>`
### HTML link 
- Ta dùng cặp thẻ a/a để làm công việc liên kết các trang web với nhau
- Thẻ thuộc tính`<a></a>`  gồm

- href: qui định địa chỉ mà url trỏ tới
- target: qui định liên kết sẽ được mở ra ở đâu
```
 _blank: cửa sổ mới

 _self: trang hiện tại

```
vd:
```
<a href="https://google.com.vn" target="_blank">Go to google page</a>
```
### xuống dòng
- Ta dùng thẻ `<br />` để xuống dòng trong một đoạn văn bản

ví dụ:
```
<p>Break line <br />in <br />paragraph</p>
```
### Line 
- Ta dùng thẻ `<hr />` để tạo một đường kẻ ngang trong trang HTML
vd :
### Images
- Ta dùng thẻ `<img>` để chèn ảnh vào trang web
- Thuộc tính của thẻ `<img>` gồm:
- src: chỉ ra đường dẫn file ảnh
- alt: để mô tả nội dung sẽ hiển thị khi đường dẫn tới file ảnh không tồn tại
- title=”Tiêu đề”: nội dung hiển thị khi đưa trỏ chuột lên hình.
- width, height: độ rộng và độ cao của file được tính bằng excel, nếu không có width và height thì mặc định sẽ lấy kích thước gốc của file
### Các thẻ định dạng text
- `<b>` (bold): Chữ In đậm
- `<u>` (Underline): Chữ gạch chân
- `<i>` (italic): Chữ in nghiêng
- `<big>` (Big): Chữ lớn hơn
- `<sub>` (Subscrip) Chỉ số dưới, ví dụ: H2O
- `<sup>` (Superscript): Chỉ số trên, ví dụ: x2y
-  `<strong>` In đậm (nhấn mạnh `<b>)`
- `<em>`(emphasized): Chữ in nghiêng, Nhấn mạnh hơn `<i>`

### bảng
- Thẻ `<table>` dùng để xác định một cái bảng.
- Thẻ `<tr>` dùng để xác định một hàng bên trong bảng.
- Thẻ `<th>` dùng để xác định một ô (tiêu đề) bên trong hàng.
- Thẻ `<td>` dùng để xác định một ô (bình thường) bên trong hàng.
```
<!DOCTYPE html>
<html>
<head>
    <title>Xem ví dụ</title>
    <meta charset="utf-8">
</head>
<body>
    <table border="1">
        <tr>
            <th>Họ tên</th>
            <th>Ngày sinh</th>
            <th>Giới tính</th>
        </tr>
        <tr>
            <td>Trần Anh Đức</td>
            <td>03/08/1993</td>
            <td>Nam</td>
        </tr>
        <tr>
            <td>Kiều Thị Thu Hằng</td>
            <td>04/09/1991</td>
            <td>Nữ</td>
        </tr>
        <tr>
            <td>Vương Thị Lê Na</td>
            <td>06/10/1991</td>
            <td>Nữ</td>
        </tr>
    </table>
</body>
</html>
```
Các thuộc tính được dùng trong việc tạo bảng
- border :- Thiết lập độ dày của cái đường viền bao xung quanh bảng và các ô.
- cellspacing :- Thiết lập khoảng cách nằm giữa mỗi hai đường viền lân cận.

- cellpadding :- Thiết lập khoảng cách vùng đệm bên trong các ô.

- bgcolor : - Thiết lập màu nền cho bảng hoặc các ô.

- width :- Thiết lập chiều rộng cho bảng hoặc các ô.

- height : - Thiết lập chiều cao cho bảng hoặc các ô.

- align : - Canh lề cho nội dung bên trong ô (theo chiều ngang)

- valign :- Canh lề cho nội dung bên trong ô (theo chiều dọc)

#### Cách gộp ô trong bảng
- theo chiều ngang
`colspan="số ô muốn gộp lại với nhau"`
- theo chiều dọc
`rowspan="số ô muốn gộp lại với nhau"`

## [link tài liệu tham khảo](https://viblo.asia/p/tim-hieu-ve-html-va-css-co-ban-7ymwGXV0R4p1)