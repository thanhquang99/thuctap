# Phụ thuộc hàm và chuẩn hóa CSDL quan hệ
##  Một số nguyên tắc thiết kế
- Rõ ràng về ý nghĩa (quan hệ thuộc tính) ,tránh phụ thuộc (về ý nghĩa) giữa các thuộc tính với nhau
- Tránh các khả năng phát sinh dị thường cập nhật trong các quan hệ (như dư thừa ,trùng lặp thông tin)
- Tránh đặt các thuộc tính có nhiều giá trị null 
- Các lược đồ quan hệ kết nối với đièu kiện bằng các thuộc tính nên là khóa chính hoặc khóa ngoài theo cách đmar bảo không sinh ra các bô giả
## Hàm phụ thuộc 
Cho lược đồ quan hệ R ; X và Y là các tập thuộc tính trên R với 2 bộ bất kì trên X cũng bằng nhau trên Y thì ta nói Y phụ thuộc vào hàm X hay X xác định hàm Y ,X là vế trái Y là vế phải của hàm phụ thuộc

Kí hiệu : X->Y
### Thể hiện hàm phụ thuộc trên lược đồ
![alt](/images/Screenshot_50.png)
### Quy tắc suy diễn phụ thuộc hàm 
![alt](/images/Screenshot_52.png)
### Bao đóng của tập phụ thuộc hàm
Cho lược đồ R (A), F là một tập các phụ thuộc hàm trên R; 
Tập tất cả các phụ  thuộc hàm suy dẫn ra được từ F gọi là bao đóng của F, kí hiệu là F+

Ví dụ:
BANGDIEM(Masv,  Dtoan,  Dtin, Dtb,  Xeploai)

F= {Dtoan, Dtin->Dtb; Dtb->Xeploai}

F= {Dtoan, Dtin->Dtb; Dtb->Xeploai}
### Bao đóng của tập thuộc tính
Cho lược đồ quan hệ R (U), tập phụ thuộc hàm F; X là một  tập thuộc tính của R; gọi X+F  là bao đóng của X theo F 
### Tập Phụ thuộc hàm tương đương
-  Tập phụ thuộc hàm E được phủ bởi  tập  phụ thuộc  hàm F nếu mỗi phụ thuộc hàm trong E đều thuộc F+
  hay mỗi phụ thuộc hàm trong E có thể suy dẫn ra được từ F
- Hai tập phụ thuộc hàm E và F là tương đương  nếu
E+ = F+
- Hai tập phụ thuộc hàm Tương đương có nghĩa là mỗi phụ thuộc hàm trong trong tập này có thể suy dẫn từ tập kia. 
### Tập phụ thuộc hàm tối thiểu
Tập phụ thuộc hàm F gọi là tối thiểu  nếu F thỏa mãn các điều kiện sau:
- Vế phải của mọi phụ thuộc hàm trong F chỉ có 1 thuộc tính
- Không thể thay thế  X -> A  trong F bằng Y -> A với Y  -> X mà vẫn còn là tập phụ thuộc hàm tương đương với F.
- Không thể bớt được bất kỳ phụ thuộc hàm nào  khỏi F mà vẫn là tập phụ thuộc hàm tương đương F
## Các dạng chuẩn dựa trên khóa chính
Thủ tục chuẩn hoá   
- Một cơ cấu hình thức để phân tích các lược đồ quan hệ dựa trên khoá và các phụ thuộc hàm.
- Một loạt các kiểm tra dạng chuẩn có thể thực hiện trên các lược đồ quan hệ riêng rẽ sao cho cơ sở dữ liệu quan hệ có thể được chuẩn hoá đến một mức cần thiết. 

Chuẩn hóa cần đảm bảo tính chất:
- Nối không mất mát (hoặc nối không phụ thêm- không thêm bộ giả)
 -Bảo toàn sự phụ thuộc đảm bảo rằng từng phụ thuộc hàm sẽ được biểu hiện trong các quan hệ riêng rẽ nhận được sau khi tách.
### Dạng chuẩn 1 (1NF)
Một quan hệ gọi là 1NF nếu :
- Miền giá trị của mỗi thuộc tính chỉ chứa giá trị nguyên tử (đơn, ko phân chia được) 
- Giá trị của mỗi thuộc tính trong các bộ là một giá trị đơn (đơn trị)
### Dạng chuẩn 2 
Một  lược đồ quan hệ R ở dạng chuẩn 2 (2NF) nếu: 
- R thỏa mãn chuẩn 1
- Mọi thuộc tính không khóa của R phụ thuộc hàm đầy đủ vào khóa chính

tức là: Mỗi thuộc tính không khóa không phụ thuộc bộ phận vào khóa của R
### Dạng chuẩn 3 
Lược đồ R là dạng chuẩn 3 nếu:
- Thỏa mãn chuẩn 2
- Không có thuộc tính không khoá nào của R là phụ thuộc bắc cầu vào khoá chính. 

Tức là: mỗi phụ thuộc hàm X -> Y thì
Hoặc X siêu khóa
Hoặc Y là thuộc tính khóa. 
### Dạng chuẩn Boyce-Codd (BCNF) 
Lược đồ quan hệ R được gọi là ở dạng chuẩn Boyce-Codd (BCNF) nếu:
- Thỏa mãn dạng chuẩn 3NF 
- Không có thuộc tính khóa phụ thuộc hàm vào thuộc tính không khóa.
