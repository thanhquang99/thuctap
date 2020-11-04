# Mô hình OSI (Open Systems Interconnection Reference Model)
Mô hình OSI gồm 7 tầng
- Physical Tầng vật lý) :Đảm bảo các yêu cầu truyền/nhận các chuỗi bit qua các phương tiện vật lý.
- Datalink (): Tạo/gỡ bỏ khung thông tin (Frames), kiểm soát luồng và kiểm soát lỗi.
- network :Thực hiện chọn đường và đảm bảo trao đổi thông tin trong liên mạng với công nghệ chuyển mạch thích hợp.
- transport : Vận chuyển thông tin giữa các máy chủ (End to End). Kiểm soát lỗi và luồng dữ liệu
- session : Quản lý các cuộc liên lạc giữa các thực thể bằng cách thiết lập, duy trì, đồng bộ hóa và hủy bỏ các phiên truyền thông giữa các ứng dụng
- Presentation layer: Tầng này trên máy tính truyền dữ liệu làm nhiệm vụ dịch dữ liệu được gửi từ tầng ứng dụng sang định dạng chung
- Present Application:Giao tiếp người và môi trường mạng
## Quy trình OSI truyền tin
### Phía máy gửi
- Ở tầng application người dùng sẽ đưa thông tin cần gửi vào máy tính
- Ở tầng presentation chyển dữ liệu thành dạng mã hóa chung và nén dữ liệu
- Ở tầng session : bổ sung thông tin cần thiết co gói tin(gửi - nhận)
- Ở tầng transport : dữ liệu sẽ được cắt ra thành các segment và cũng có tác dụng bổ xung thêm thông tin về phương thức vận chuyển
- Ở tầng network thì các segment lại tiếp tục được cắt thành các package khác nhau và bổ xung thêm thông tin định tuyến
- Ở tầng data link các package sẽ được băm nhỏ thành các frame và bổ sung thêm các thông tin về máy nhận
- Ở tângf physical thì các frame sẽ được chuyển đổi thành các bit và được gửi đi
### Phía máy nhận
- Ở tầng physical :phía máy nhận sẽ kiểm tra quá trình đồng bộ và lưu vào vùng đệm, sau đó gửi lên tầng datalink
- Ở tầng data link sẽ được kiểm tra các gói frame có lỗi không sau đó kiêmr tra đến địa chỉ MAC ,nếu trùng thì sẽ gửi tiếp đến tầng netwwork
- Ở tầng netwwork sẽ kiểm tra địa chỉ ip của gói tin có đúng là máy nhận hay không thì sẽ tiếp tục chuyển lên tầng tiếp theo
- Ở tầng transport :Tầng này sẽ sắp xếp dữ liệu phận đoạn và đưa dữa liệu đến tầng session
- Ở tầng session :kiểm tra toàn vẹn dữ liệu và gỡ header của tầng này và chuyển đến tầng kế tiếp
- ở tầng Presentation sẽ chuyển thành các dạng dữ liệu phù hợp và gử lên tâng application
- Ở tầng application sẽ tiến hành gở bỏ header cuối cùng và ta nhận được thông tin cuối cùng
## Một số ứng dungj phổ biến của tầng ứng dụng
