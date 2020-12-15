```
#!/bin/bash
apt update && apt upgrade -y
function install {
if [ -e /usr/sbin/httpd ]
then
echo "installed apache"
else
	echo "installing apache"
	sleep 5
	apt install apache2 -y 
fi
if [ -e /usr/bin/mysql ]
then 
	echo "installed mysql"
else 	
	echo " installing mysql"
	apt install mariadb-server mariadb-client -y

fi
if [ -e /usr/bin/php ]
then 
	echo "installed php "
else 	
	echo "installing php "
	apt install php php-mysql -y
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
}	

function wp {

	cd /tmp && wget https://vi.wordpress.org/wordpress-4.5.22-vi.tar.gz
	tar xvfz wordpress-4.5.22-vi.tar.gz
	cp -R wordpress /var/www/html/
	chown -R www-data:www-data /var/www/html/wordpress/
	chmod -R 755 /var/www/html/wordpress/
	mkdir /var/www/html/wordpress/wp-content/uploads
	chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads/
	
}

install

create_mysql

wp
```


`Lưu ý:` chúng ta bây giờ có thể vào browser gõ `[địa chỉ ip]/wordpress ` để có thể là tiếp như các phiên bản centos 7.

![alt](/images/Screenshot_9.png)