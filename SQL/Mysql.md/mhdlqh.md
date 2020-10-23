# Mô hình dữ liệu quan hệ
## Quan hệ 
Các thông tin lưu trữ trong CSDL được tổ chưc thành bảng 2 chiều gọi là quan hệ
![alt](/images/Screenshot_39.png)
1. Quan hệ gồm :Tên + Tập hợp các cột + Tập hợp các dòng
2. Cấp của quan hệ là số thuộc tính trong quan hệ
3. Thuộc tính là tên các cột của quan hệ mô tả ý nghĩa cho các giá trị tại cột đó

Tất cả các giá trị trong một cột đều có cùng một kiểu dữ liệu và các gía trị là nguyên tố

4. Miền giá trị :tập các giá trị nguyên tố găn với một thuộc tính 

Kí hiệu :dom(A): tức là miền giá trị của A

5. Bộ (tuple)

Là các dòng của quan hệ thể hiện dữ liệu của một thực thể
6. Lược đồ quan hệ

[tên quan hệ]([tên tập thuộc tính])

ví dụ :hocsinh(mahs,tenhs,date,country)

7. Lược đồ CSDL : là tập các lược đồ quan hệ và các ràng buộc 
8. Một số kí hiệu thường dùng 
![alt](/images/Screenshot_40.png)
## Ràng buộc toàn vẹn
- Thứ tự các bộ trong quan hệ không quan trọng
- Thứ tự các giá trị trong bộ là quan trọng
1. Các đặc trưng của quan hệ 
- Mỗi giá trị trong một bộ có thể là nguyên tố hoặc null
- Không có bộ nào trùng nhau
2. Ràng buộc 
- là nhứng quy tắc, điều kiện cần thỏa mãn trong một thể hiện của CSDL quan hệ 
- Các loại ràng buộc :
+ràng buộc miên
+ràng buộc khóa
+ràng buộc toàn ven thực thể 
+ràng buộc toang vẹn tham chiếu
- Ràng buộc miền [t(A)] phải thuộc dom(A)
- Ràng buộc khóa 
+Khóa chính 
- Ràng buộc toàn vẹn thực thể : Khóa chính luôn phải có giá trị cụ thể
- Ràng buộc tham chiếu :
+Khóa ngoại

`Nhận xét:`
- Trong một lược đồ quan hệ vừa có thể là khóa chính vừa có thể là khóa ngoại
- Khóa ngoài có thể tham chiếu đến khóa chính trong cùng một lược đồ quan hệ
- Có thể có nhiều khóa ngoại tham gia tham chiếu đến khóa chính
- Ràng buộc tham chiếu bằng ràng buộc khóa ngoại
## Chuyển đổi lược đồ ER sang mô hình quan hệ
### Quy tắc
- Mỗi thực thể(trừ thực thể yếu) chuyển thành một quan hệ và giữa nguyên tên và tập thuộc tính của nó
- Thực thể yếu chuyển thành một quan hệ có cùng tên ,giữ lại tập thuộc tính và thêm khóa của thực thể chủ vào
- Liên kết 1-1 :Thêm vào quan hệ thứ nhất thuộc tính khóa của quan hệ thứ 2 làm khóa ngoại hoặc trộn 2 quan hệ khi cả 2 đều tham gia toàn bộ 
- Liên kết 1-nhiều :Thêm vào quan hệ phía nhiều thuộc tính khóa của quan hệ phía ít
- Liên kết nhiều-nhiều :Tạo một quan hệ mới ,giữ nguyên tên và thêm các khóa của của các kiểu thực thể liên quan + Thuộc tính liên kết
- Thuộc tính đa trị :chuyên thành một quan hệ có tên là thuộc tính đa trị với thuộc tính gồm tên thuộc tính đa trị + khóa của liên kết trở thành khóa ngoại
- Liên kết đa ngôi chuyển thành một quan hệ có tên trùng với thuộc tính đa ngôi có thuộc tính gồm thuộc tính liên kết và các khóa của liên kết
Ví dụ:
![alt](/images/Screenshot_41.png)

Thisinh(sbd,tents,demts,hots,ngaysinh,mapt)

Phongthi(mapt,dd,sl)

nganh(man,motan,tenn,mat,makt)

truong(mat,tent,dc)

khoithi(makt,motakt)

monthi(mamt,tenmt,hinhthuc,thoigian,makt)

cbcoithi(macb,hocb,demcb,tencb,mapt,giamsat)

diem(diem,sbd,mamt)

dangki(sbd,man)
