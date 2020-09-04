# wordpresswordpress
- Là hệ thống quản lý nội dung miễn phí và mã nguồn mở xây dựng dựa trên PHP và MySQL. Được phát hành vào năm 2003.
- Trước khi cài dặt wordpress ta phải tiến hành cài đặt LAMP
## Giới thiệu về LAMP
-LAMP là một hệ thống các phần mềm để tạo dựng môi trường máy chủ web được viết bằng PHP. Có khả năng chứa và phân phối các trang web động được viết bằng PHP.

-LAMP là viết tắt của LINUX, APACHE, MySQL, PHP

-Trong đó 
- LINUX là hệ đièu hành LINUX
- APACHE Là phần mềm máy chủ web, có thể thực hiện các request(Yêu cầu) được gọi tới máy chủ thông qua các giao thức HTTP.
- MySQL là hệ quản trị cơ sở dữ liệu (thường dùng mariadb)
- PHP là ngôn ngữ lập trình cho hoạt động kịch bản của máy chủ
## Tiến trình cài đặt LAMP
1. Cài đặt LINUX (centos 7)
2. Cài đặt Apache
- Tiến hành cài đặt và khởi động service
```
yum install -y httpd
systemctl start httpd
systemctl enable httpd
```
- Kiểm tra trạng thái hoạt động trên server
```
systemctl status httpd
```
- Tiến hành tắt firewall để có thể truy cập trên browser máy thực
```
systemctl stop firewalld
```
3. Cài đặt hệ quản trị cở sở dữ liệu
Chúng ta có thể sử dụng MySQL và Mariadb (ở đây chúng ta sẽ cài mariadbb)
- Cài đặt Mariadb
```
yum -y install mariadb mariadb-server
```
- Khởi động Mariadb Service
```
systemctl start mariadb
```
- Cài mật khẩu root cho cơ sở dữ liệu 
```
mysql_secure_installation
```
- Thiết lập một số cấu hình như các bước sau
1. ấn enter sau đó ấn y để đặt mật khẩu cho root
2. nhập mật khẩu mới
3. nhập lại mật khẩu 
4. sẽ có các câu hỏi tiếp theo và bạn chỉ cần bấm yes
- Xóa bỏ các user khác
- Không cho phép root đăng nhập từ xa
- xóa bỏ data base
- Khởi chạy lại bảng Privileges(Bảng phân quyền)

Sau khi thiết lập, Kích hoạt mariadb để khởi động cùng hệ thống

4. Cài đặt PHP

Để tiến hành cài đặt php chúng ta sẽ tải kho Remi centos và cập nhật kho
```
yum install epel-release
yum update epel-release
rpm -Uvh https://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
- Cài Yum-utils vì cần tiện ích yum-config-manager để cài đặt:
```
yum -y install yum-utils
```
- Tiến hành cài đặt PHP.Có rất nhiều các ver khác nhau nhưng mình sẽ cài ver 7.00
```
yum-config-manager --enable remi-php70
```
- Cài đặt các option PHP
```
yum -y install php php-opcache php-mysql
```
- Tiến hành kiểm tra kết quả ta thêm các file sau
```
echo "<?php phpinfo(); ?>" > /var/www/html/info.php
```
- restart lại apache
```
systemctl restart httpd
```
- Vào trình duyệt, gỗ trên thanh URL địa chỉ như sau:
```
[Địa chỉ IP]/info.php
```
Nếu hiện ra như hình bên dưới là đã thành công

![alt](/images/Screenshot_3.png)

## Cài đặt wordpress
1. Tạo cơ sở dữ liệu cho wordpress 
- Đăng nhập vào tài khoản root của cơ sở dữ liệu
```
mysql -u root -p
```
Bạn cần nhập Password mà bạn đã thiết lậpập cài đặt khi cài đặt Mariadb. Khi nhập xong sẽ chuyển sang màn hình Mariadb .

Tiếp theo thiết lập bạn sẽ tạo cơ sở dữ liệu cho wordpress. Có thể dùng tên bất kỳ cho tên của Database
```
CREATE DATABASE wordpress;
CREATE USER thanhquang@localhost INDENTIFIED by 'Khuongquang99';
```
Chúng ta dã tạo được tài khoản có user : khuongquang và password : Khuongquang99

`Lưu ý :không nên passwd có kí tự @`

Tiến hành cấp quyền quản lý CSDL Wordpress cho user mới tạo:
```
GRANT ALL PRIVILEGES ON wordpress.* TO thanhquang@localhost IDENTIFIED BY 'Khuongquanng99';
```
Xác thực lại những thay đổi về quyền:
```
FLUSH PRIVILEGES;
```
Hoàn tất và thoát khỏi Mariadb:
```
exit
```
2. Tải và cài đặt wordpress

- Cài gói hỗ trợ php-gd:
```
yum -y install php-gd
```
- Cài gói tải xuống wget Tiến hành tải xuống Wordpress với phiên bản mới nhất;
```
wget http://wordpress.org/latest.tar.gz
```
Lưu ý: Bạn cần để ý tới thư mục mà wget tải xuống. ở đây mình đang đứng tại thư mục /root/
- Giải nén file
```
tar xvfz latest.tar.gz
```
- Copy các file trong thư mục sau WordPress tới đường dẫn /var/www/html
```
cp -Rvf /root/wordpress/* /var/www/html
```
3. Cấu hình wordpress

- Di chuyển tới thư mục chứa Wordpress
``` 
cd /var/www/html
```
- File có cấu hình wp là file wp-config.php. Tuy nhiên ở đây chỉ có file wp-config-sample.php.Tiến hành cophy lại file cấu hình như sau:
```
cp wp-config-sample.php wp-config.php
```
- Mở file wp-config.php với trình vi để sửa:
```
vi wp-config.php
```
Trong file tìm đến dòng dưới để chỉnh sửa:

```
/** Tên database cho WordPress */
define( 'DB_NAME', 'wordpress' );

/** MySQL database tên Usern */
define( 'DB_USER', 'thanhquang' );

/** MySQL database password cho user */
define( 'DB_PASSWORD', 'Khuongquang99' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );

/** Database Charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8' );
```
Lưu và thoát khỏi trình vi.
- Phân quyền:
```
chmod -R 755 /var/www/*
chown -R apache:apache /var/www/*
```
- Khởi động lại Httpd
```
systemctl restart httpd
```
## Hoàn tất phần giao diện
Chúng ta sẽ vào browser và gõ địa chỉ ip


![alt](/images/Screenshot_4.png)


![alt](/images/Screenshot_5.png)


![alt](/images/Screenshot_6.png)


![alt](/images/Screenshot_7.png)