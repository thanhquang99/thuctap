# Tạo background trong html 
- Ta có thể tạo background bằng các tạo thêm thẻ style vào phần head
![alt](/images/Screenshot_53.png)
```
<link rel="shortcut icon" type="image/png" href="https://raw.githubusercontent.com/thanhquang99/thuctap/master/images/IMG_4141.PNG"/>
```
Đây là cú pháp ta tạo favicon với html ,ta gắn link của ảnh mà ta muốn làm favicon vào mục hreaf.Tuy nhiên cách này không chuyên nghiệp , ta có thể vào tràn web `https://convertico.com/` để tạo ảnh favicon  ,ta nên để kích thước 16*16 và say khi tạo xong nên chuyển định dạng thành favicon.ico
# Đặt kích thước chiều dài các thẻ div
```
        .row {
            display: flex;
        }
        .col {
            flex: 1;
        }
```
- Ta định nghiã thêm 2 thẻ row và col
- Đưa 2 thẻ cần vào 1 thẻ div lớn `<div class="row">`
- Thêm `class="col"` vào các thẻ cần định dạng kích thước như content và advertisement
[Ví dụ](https://github.com/thanhquang99/thuctap/blob/master/HTML/test.html)