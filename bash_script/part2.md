# BASH SCRIPT - LOOP
## FOR -LOOP
Cấu trúc vòng lặp for
```
for var in list
do
<some-commands-here>
done
```
Trong đó ta thay `list` thành danh sách các biến chúng ta chúng muốn chạy

Khi chạy cấu trúc này nó sẽ chạy tuần tự hết các biến trong `list ` từ đầu đến cuối đến khi hết thì sẽ dừng vòng lặp .
```
#!/bin/bash
for var in 1 2 3 4
do 
echo $var
done
```
Khi ta chạy file có nội dung này thì màn hình sẽ hiện
```
1
2
3
4
```
`lưu ý` :chúng ta có thể thay `var` thành bất kì biến nào khác mà chúng ta nghĩ ra nhưng không được thay đổi cấu trúc của lệnh

Vòng lặp không chỉ lặp một kí tự đơn giản mà ta có thể lặp cả cụm từ,nhưng cụm từ đó phải được đặt trong dấu `"  "`
```
#!/bin/bash
for car in mot "co hai" "co ba"
do 
echo display $car
done
```
Chúng ta cũng có thể cho các từ cần lặp vào một file riêng lẻ rồi gọi ra file đấy để lặp(có thể sử dụng lệnh cat)
```
#!bin/bash
list=myfile
for var in $(cat $list)
do
echo $var
done
```
## Field separators 
 IFS (Internal Field Separator) là một biến môi trường đặc biệt .Theo mặc định bash coi các kí tự sau là dấu phân cách trường

- Space(dấu cách)

- Tab character (Kí tự tab)

- Line feed character (Dòng mới)

Nếu bash gặp bất kỳ ký tự nào trong số này trong dữ liệu, nó giả định giá trị danh sách độc lập tiếp theo nằm trước mặt. 

Cách khắc phục vấn đề là ta có thể tạm thời thay đổi biến môi trường bằng IFS
```
#!/bin/bash
file="/etc/passwd"
IFS=$'\n'
for var in $(cat $file)
do
echo " $var"
done
```
```
root:x:0:0:root:/root:/bin/bash
 bin:x:1:1:bin:/bin:/sbin/nologin
 daemon:x:2:2:daemon:/sbin:/sbin/nologin
 adm:x:3:4:adm:/var/adm:/sbin/nologin
 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
 sync:x:5:0:sync:/sbin:/bin/sync
 shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
 halt:x:7:0:halt:/sbin:/sbin/halt
 mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
 operator:x:11:0:operator:/root:/sbin/nologin
 games:x:12:100:games:/usr/games:/sbin/nologin
 ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
 nobody:x:99:99:Nobody:/:/sbin/nologin
 systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
 dbus:x:81:81:System message bus:/:/sbin/nologin
 polkitd:x:999:998:User for polkitd:/:/sbin/nologin
 sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
 postfix:x:89:89::/var/spool/postfix:/sbin/nologin
 chrony:x:998:996::/var/lib/chrony:/sbin/nologin
 apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
 thanhquang:x:1000:1000::/home/thanhquang:/bin/bash
 mysql:x:27:27:MariaDB Server:/var/lib/mysql:/sbin/nologin
```



## Bypassing files contained in a directory(Duyệt các tập lệnh trong thư mục)
```
#!/bin/bash
for file in /home/thanhquang/*
do
if [ -d "$file" ]
then
echo "$file is a directory"
elif [ -f "$file" ]
then
echo "$file is a file"
fi
done
```
```
/home/thanhquang/file1 is a file
/home/thanhquang/file2 is a file
/home/thanhquang/file3 is a file
/home/thanhquang/kkk is a file
/home/thanhquang/myfile is a file
/home/thanhquang/spript is a file
```
Dấu [*] biểu thị tấp cả file và thư mục trong [thanhquang]

Thay vì phải ngồi viết tay tất cả các tên file thì ta chỉ cần đưa ra đường dẫn trong câu lặp for

Ta cũng có thể tự tạo vòng lặp với cấu trúc for
```
for(biến khởi tạo ; điều kiện lặp ; biểu thức thay đổi biến khoier tạo)
```

```
#!/bin/bash
for (( i=1; i <= 10; i++ ))
do
echo "number is $i"
done
```

```
number is 1
number is 2
number is 3
number is 4
number is 5
number is 6
number is 7
number is 8
number is 9
number is 10
```
## While -loop 
```
while <command-to-check-conditions>
do
<some-commands-go-here>
done
```
Trong khi điều kiện còn đúng thì làm lệnh 

```
#!/bin/bash
var1=5
while [ $var1 -gt 0 ]
do
echo $var1
var1=$[ $var1 - 1 ]
done
```
```
5
4
3
2
1
```
## Nested loops (Vòng lặp lồng nhau)
```
#!/bin/bash
for (( a = 1; a <= 3; a++ ))
do
echo "Start $a:"
for (( b = 1; b <= 3; b++ ))
do
echo " Inner loop: $b"
done
done
```
```
Start 1:
 Inner loop: 1
 Inner loop: 2
 Inner loop: 3
Start 2:
 Inner loop: 1
 Inner loop: 2
 Inner loop: 3
Start 3:
 Inner loop: 1
 Inner loop: 2
 Inner loop: 3
 ```
 Vòng lặp của b được lồng trong vòng lặp của a 

 Sử dụng phổ biến nhất của vòng lặp lồng là xử lý tập tin. Nên vòng lặp ngoài đang bận rộn trên các đường của tập tin, và bên trong đã làm việc với từng dòng. 
 ```
 #!/bin/bash
IFS=$'\n'
for entry in $(cat /etc/passwd)
do
echo "Values in $entry –"
IFS=:
for value in $entry
do
echo " $value"
done
done
```
```
Values in root:x:0:0:root:/root:/bin/bash –
 root
 x
 0
 0
 root
 /root
 /bin/bash
Values in daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin –
 daemon
 x
 1
 1
 daemon
 /usr/sbin
 /usr/sbin/nologin
Values in bin:x:2:2:bin:/bin:/usr/sbin/nologin –
 bin
 x
 2
 2
 bin
 /bin
 ```
 ## Loop management(Quản lí vòng lặp)
 - `Break` command :Ngắt kết nối vòng lặp.
 - `Continue` command : thực hiện ngay lập tức lần lặp tiếp theo cho dù lần lặp hiện tại vẫn còn câu lệnh chưa thực hiện xong.

 ```
 #!/bin/bash
for var1 in 1 2 3 4 5 6 7 8 9 10
do
if [ $var1 -eq 5 ]
then
break
fi
echo "Number: $var1"
done
```
```
Number: 1
Number: 2
Number: 3
Number: 4
```
Khi vòng lặp lặp đến số 5 thì đã không thỏa mãn điều kiện của `if` và câu lệnh `break` được thực hiện dừng vòng lặp
```
#!/bin/bash
for (( var1 = 1; var1 < 15; var1++ ))
do
if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
then
continue
fi
echo "Iteration number: $var1"
done
```
```
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
Iteration number: 5
Iteration number: 10
Iteration number: 11
Iteration number: 12
Iteration number: 13
Iteration number: 14
```
Khi biến `var1 ` thỏa mãn điều kiện if thì câu lệnh `echo` được bỏ qua và không được thực hiện


## [Tài liệu tham khảo](https://medium.com/introduction-into-bash/bash-scripts-part-2-loops-39968fdc3d61)