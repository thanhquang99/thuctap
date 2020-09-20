```
#!/bin/bash
function install {
if [ -e /usr/sbin/httpd ]
then
echo "installed apache"
else
	echo "--------installing apache -----------"
	sleep 5
	yum install -y httpd
	systemctl start httpd
	systemctl enable httpd
	systemctl stop firewalld
	echo "DONE"
	sleep 3 
fi
if [ -e /usr/bin/mysql ]
then 
	echo "installed mysql"
else 
	echo "--------installing mysql----------"
	sleep 5
	yum -y install mariadb mariadb-server
	systemctl start mariadb
	systemctl enable mariadb

	echo "DONE"
	sleep 3
fi
if [ -e /usr/bin/php ]
then 
	echo "installed php "
else 
	echo "---------installing php ---------"
	sleep 5
	yum install epel-release -y
	yum update epel-release -y
	yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
	yum -y install yum-utils
	yum-config-manager --enable remi-php73 -y
	yum -y install php php-opcache php-mysql
	systemctl restart httpd
	sleep 5
fi
}
function create_mysql {
cat << EOF | mysql -uroot
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY 'Khuongquang99' WITH GRANT OPTION ;FLUSH PRIVILEGES;
EOF
sleep 3
echo "tao tai khoan user cho MySQL voi user thanhquang pass Khuongquang99 DATABASE wordpress "
sleep 3



	mysql -uroot -pKhuongquang99 -e "CREATE DATABASE wordpress;
	CREATE USER thanhquang@localhost IDENTIFIED BY 'Khuongquang99';
	GRANT ALL PRIVILEGES ON wordpress.* TO thanhquang@localhost IDENTIFIED BY 'Khuongquang99';
	FLUSH PRIVILEGES;"
	echo "DONE"
	sleep 3



	echo " ------- Tien hanh cai dat wordpress ------- "
	sleep 3
	yum -y install php-gd
	yum install wget -y
	wget https://vi.wordpress.org/wordpress-4.5.22-vi.tar.gz
	tar xvfz wordpress-4.5.22-vi.tar.gz
	cp -Rvf /root/wordpress/* /var/www/html
	cd /var/www/html
	cp wp-config-sample.php wp-config.php
	sed -i 's/username_here/thanhquang/g' /var/www/html/wp-config.php
	sed -i 's/database_name_here/wordpress/g' /var/www/html/wp-config.php
	sed -i 's/password_here/Khuongquang99/g' /var/www/html/wp-config.php
	chmod -R 755 /var/www/*
	chown -R apache:apache /var/www/*
	systemctl restart httpd
	echo "DONE"
	sleep 3
	echo "tat ca moi thu da xong gio ban co the vao browser va go dia chi ip cua may da cai dat va trai nghiem "
}
	install
	create_mysql
	
	
```
`Những lưu ý cần thiết `: 
- Câu lệnh cat  << EOF |      là để ta có thể từ ngoài linux mà có thể thao tác các lệnh trong phần sau dấu `|` và khi kết thúc các câu lệnh phải có `EOF` để phân biệt là đã kết thúc thao tác trong Mysql

- Câu lệnh `cat  << EOF` phải luôn đặt ở đầu dòng 

- ` mysql -uroot -pKhuongquang99 -e "Command"` giống như khi ta `ssh` ta có thể thao tác các câu lệnh từ ngoài linux

- Cấu trúc câu lệnh thay thế từ trong file :
```
sed -i 's/[Từ cần thay thế}/[Từ thay thế]/g' [PATH of file]
```
 