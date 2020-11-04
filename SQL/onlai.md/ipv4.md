# IPv4- Internet Protocol version 4
## Định nghĩa
- Là giao thức internet phiên bản 4 và là phương thức đầu tiên được sử dụng rộng rãi
- Địa chỉ ipv4 gồm 32 bit nhị phân và được chia làm 4 octet được biểu diễn ở dạng thập phân và ngăn cách nhau bằng dấu chấm

VD: 192.168.10.119
## Phân loại ipv4
### Lớp A
- Gồm 1 octet đầu làm netwwork và 3 octet cuối làm host
- Bit đầu tiên luôn là 0
- Địa chỉ lớp A gồm 1.0.0.0-126.0.0.0 và 127.0.0.0 làm loopback
### Lớp B
- Gồm 2 octet đầu làm netwwork và 2 octet sau làm host
- 2 Bit đàu tiên là 10
- Địa chỉ lớp B gồm 128.0.0.0-191.255.0.0
### Lớp C
- Gồm 3 octet đầu là netwwork và 1 octet sau làm host
- Ba bít đầu luôn là 110
- Địa chỉ lớp C gồm 192.0.0.0-223.255.255.0
### Lớp D
224.0.0.0-239.255.255.255
### Lớp E
Từ 240.0.0.0 trở đi
## IP public và ip private
- Public ip được sử dụng cho các gói tin đi ra ngoài internet
- private ip đucowj sử dụng cho các gói tin trong mạng nội bộ,có thể được sử dụng lặp đi lặp lại trong các mạng LAN khác nhau
- Dải địa chỉ IP private
lớp A :10.X.X.X
lớp B : 172.16.X.X
Lớp C :192.168.X.X
## Các kiểu định tuyến 
### Broadcast 
 trong trường hợp này, Một gói broadcast chuyển đến tất cả những thiết bị tham gia trong một mạng cục bộ, mà không cần phải được quy định rõ ràng như một máy nhận. Do đó broadcast nên được giới hạn trong những phần riêng của mạng, và không được router chuyển tiếp. Tất cả các bit host đều bằng 1.
## Anycast
là một phương pháp sử dụng các địa chỉ mạng và định tuyến để gửi dữ liệu từ một nguồn duy nhất đến một trong những nút của một nhóm các thiết bị, dựa trên căn bản là gần nhất, ít tốn kém nhất, khỏe mạnh nhất, tuyến ít bị nghẽn nhất
## Multicast
được sử dụng để mô tả cách thức truyền tin được gửi từ 1 điểm đến nhiều điểm khác
## unicast
 được sử dụng trong mạng máy tính để mô tả cách thức truyền tin được gửi từ 1 điểm đến 1 điểm khác.
## Chia subnet
- Mượn n bit từ Host để lấy làm Network.
- Số subnet : 2^n
- Số host/subnet 2^m - 2 (m là số bit làm Host )
