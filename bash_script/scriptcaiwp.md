```
#!/bin/bash
cd ~
echo " ------- Tien hanh cai dat apache -------"
yum install -y httpd
systemctl start httpd
systemctl enable httpd
systemctl stop firewalld
echo "DONE"
echo " ------ Tien hanh cai dat mariadb ------ "
yum -y install mariadb mariadb-server
systemctl start mariadb
systemctl enable mariadb
cat << EOF | mysql -uroot
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY 'Khuongquang99' WITH GRANT OPTION ;FLUSH PRIVILEGES;

EOF
echo "DONE"
echo "------- Tien hanh cai dat PHP -------- "
yum install epel-release -y
yum update epel-release -y
rpm -Uvh https://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum -y install yum-utils
yum-config-manager --enable remi-php70 -y
yum -y install php php-opcache php-mysql
echo "<?php phpinfo(); ?>" > /var/www/html/info.php
systemctl restart httpd
echo "DONE"
echo "tao tai khoan user cho MySQL voi user thanhquang pass Khuongquang99 DATABASE wordpress "
mysql -uroot -pKhuongquang99 -e "CREATE DATABASE wordpress;
CREATE USER thanhquang@localhost IDENTIFIED BY 'Khuongquang99';
GRANT ALL PRIVILEGES ON wordpress.* TO thanhquang@localhost IDENTIFIED BY 'Khuongquang99';
FLUSH PRIVILEGES;"
echo "DONE"
echo " ------- Tien hanh cai dat wordpress ------- "

yum -y install php-gd
yum install wget 
wget http://wordpress.org/latest.tar.gz
tar xvfz latest.tar.gz
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
echo "tat ca moi thu da xong gio ban co the vao browser va go dia chi ip cua may da cai dat va trai nghiem "
```