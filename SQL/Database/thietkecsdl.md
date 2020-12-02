## Quá trình thiết kế CSDL
![alt](/images/Screenshot_33.png)
## Mô hình E-R (Entity relationship)
- Được dùng để thiết kế CSDL ở mức quan niệm ,biểu diễn trừu tượng cấu trúc của CSDL
### Các khái niệm 
1. Thực thể (entity-sets): là đối tượng của thế giới thực
2. Thuộc tính(attributes) :là đặc trưng để mô tả thực thể, xác định giá trị cho  mỗi thuộc tính nó

Các loại thuộc tính:
- Thuộc tính đơn : không thể tách nhỏ được
- Thuộc tính phức hợp : có thể tách ra thành các thành phần nhỏ hơn
- Thuộc tính đơn vị : có giá trị duy nhất cho 1 thực thể
- Thuộc tính đa trị : có giá trị là một tập giá trị
- Thuộc tính suy diễn : có thể từ đó mà suy diễn ra được dữ liệu
- Thuộc tính phức tạp : Kết hợp đa trị và phức hợp
- Thuộc tính khóa 
3. Mối quan hệ (Relationship) :là sự liên kết giữa 2 hay nhiều thực thể 

- Cấp liên kết: là số kiểu thực thể tham gia liên kết đó
- Liên kết đệ quy :là liên kết mà một kiểu thực thể tham gia liên kết với các vai trò khác nhau (cần phải liệt kê ra các vai trò của nó)
4. Ràng buộc trên kiểu liên kết
- Ràng buộc là những quy định để giới hạn số các tổ hợp có thể của các thực thể tham gia ,phản ánh đúng điều kiện của thực tế
- Ràng buộc tỉ số :phản ánh số các thực thể tham gia liên kết mà một thực thể có thể tham gia

vd: A(1:n):thực thể A có thể tham gia liên kết ít nhất là 1 và tối đa là n
- Thực thể yếu : là thực thể không có thuộc tính khóa, được xác định bằng cách liên kết với thực thể chủ

Các kí hiệu biểu đồ E-R:
![alt](/images/Screenshot_34.png)

### Các bước thiết kế 
1. Xác định tập thực thể
2. Xác định mối quan hệ
3. Xác định thuộc tính và gắn thuộc tính cho tập thực thể và mối quan hệ 
4. Quyết định miền giá trị cho thuộc tính
5. Quyết định thuộc tính khóa 
6. Xác định ràng buộc cho mối quan hệ và thể hiện chúng lên lươc đồ

Ví dụ về thiết kế mô hình E-R
![alt](/images/Screenshot_35.png)
## Mô hình EER (enhanced entity relationship)
### Tại sao lại cần EER
- ER không đủ để biểu diễn một số ứng dụng phức tạp
- Thêm một số khái niệm trừu tượng để thể hiện các ràng buộc rõ hơn
### Một số khái niệm cơ bản của EER
1. Lớp cha/Lớp con
- Lớp cha : là kiểu thực thể mang đặc tính chung cho các nhóm thực thể
- Lớp con: là thực thể thành viên của lớp cha mang vai trò riêng 
- Lớp con kế thừa thuộc tính và quan hệ của lớp cha và có một số thuộc tính và quan hệ của riêng nó
### Chuyên biệt hóa và tổng quan hóa
- Chuyên biệt hóa : là quá trình xác định các lớp con của thực thể lớp cha .Tập con đucowj tạo ra dựa trên các đặc tính riêng biệt

![alt](/images/Screenshot_36.png)
- Tổng quát hóa :là quá trình xác định các lớp cha từ tập thể lớp con Dựa vào dặc tính chung của các lớp con
- Ràng buộc rời rạc : mô tả quan hệ giữa lơp cha và lớp con, các lớp con phải độc lập hoàn toàn với nhau và được kí hiệu bởi chữ d nằm trong vòng tròn
![alt](/images/Screenshot_37.png)
- Ràng buộc chồng chéo : tương tự như ràng buọc rời rạc nhưng các lớp con không tách biệt với nhau và được kí hiệu bởi chữ o trong vòng tròn
- Ràng buộc đầy đủ

+Ràng buộc toàn phần : tất cả các thực thể của lớp cha phải là thành viên của ít nhất một lớp con

+Ràng buộc từng phần : cho phép thực thể của lớp cha có thể không là thành viên của bất kì lớp con nào
![alt](/images/Screenshot_37.png)
### Chuyên biệt phân cấp và lưới 
- Phân cấp : tất cả các lớp con chỉ tham gia 1 liên kết với lớp cha
- Lưới : Lớp con có thể tham gia vào nhiều hơn 1 liên kết với lớp cha
- union : mô tả quan hệ của một con với nhiều lớp cha trong chuyên biệt dạng lưới

