# IP TĨNH CHO UBUNTU 20.04 server
## Cấu hình bằng Netplan
Nếu chúng ta sử dụng netplan thì ta sử dụng câu lệnh lệnh vi sửa file `/etc/netplan/00-installer-config.yaml`

```
vi /etc/netplan/00-installer-config.yaml
```
Ta hãy chỉnh sửa flie theo hình dưới đây

![alt](/images/Screenshot_13.png)

```
netplan apply
```
## Cấu hình bằng ifupdown
### disable netplan
```
echo 'GRUB_CMDLINE_LINUX = "netcfg/do_not_use_netplan = true"' >> /etc/default/grub
update-grub
```
### Cài đặt ifupdown thay thế netplan
```
apt-get update
apt-get install -y ifupdown
```
### Xóa netplan khỏi hệ thống:
```
apt-get --purge remove netplan.io
rm -rf /usr/share/netplan
rm -rf /etc/netplan
```
### Cấu hình interface
```
vi /etc/network/interfaces
```
Ta cấu hình như trong hình
![alt](/images/Screenshot_11.png)

```
reboot
```
Khi ta cấu hình bằng ifupdown thì sẽ không thể ping bằng tên miền được

Ta có cách sửa như sau:
- Disable systemd-resolved service.
```
systemctl disable systemd-resolved.service
```
- Stop service
```
systemctl stop systemd-resolved.service
```
- Bỏ link giữa 2 file sau: /run/systemd/resolve/stub-resolv.conf và /etc/resolv.conf bằng cách xóa file /etc/resolv.conf
```
rm /etc/resolv.conf
```
- Tạo mới file /etc/resolv.conf
```
vi /etc/resolv.conf
```
- Mở file và thêm DNS server mà bạn sử dụng:
```
nameserver 8.8.8.8
```
