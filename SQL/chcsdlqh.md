# Phụ thuộc hàm và chuẩn hóa CSDL quan hệ
##  Một số nguyên tắc thiết kế
- Rõ ràng về ý nghĩa (quan hệ thuộc tính) ,tránh phụ thuộc (về ý nghĩa) giữa các thuộc tính với nhau
- Tránh các khả năng phát sinh dị thường cập nhật trong các quan hệ (như dư thừa ,trùng lặp thông tin)
- Tránh đặt các thuộc tính có nhiều giá trị null 
- Các lược đồ quan hệ kết nối với đièu kiện bằng các thuộc tính nên là khóa chính hoặc khóa ngoài theo cách đmar bảo không sinh ra các bô giả
## Hàm phụ thuộc 
