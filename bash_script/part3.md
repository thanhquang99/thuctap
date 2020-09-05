#  Command-Line Options and Switches
## Reading command line parameters (Tham số dòng lệnh đọc)
Bash shell gán các thông số dòng lệnh được nhập khi gọi tập lệnh nầy vào các biến đặc biệt gọi là các thông số vị trí:
- $0 :Tên của script
- $1-$9 là các tham số từ 1-9
```
#!/bin/bash
echo $0
echo $1
echo $2
echo $3
```
Khi ta chạy lệnh `./myscript 5 10 15`Trong đó myscript là tên file script
```
./myscript
5
10
15
```
Các sô 5 10 15 là các tham số được gắn

```
#!/bin/bash
total=$[ $1 + $2 ]
echo "The first parameter is $1."
echo "The second parameter is $2."
echo "The sum is $total."
```
```
./myscript 5 10
```
Khi chúng ta chạy lệnh trên thì có nghĩa là chúng ta đang tính tổng của 2 số 5 và 10 . Các con số 5 và 10 có thể thay đổi vào tùy các con số mà ta muốn tính tổng

## Parameter check (kiểm tra tham số)

```
#!/bin/bash
if [ -n "$1" ]
then
echo "Hello $1."
else
echo "No parameters found."
fi
```
```
./myscript thanhquang
Hello thanhquang
```
Đây là script kiểm tra tham số thanhquang nếu có tồn tại thì in ra dòng chữ `Hello thanhquang`

## Counting parameters (Thông số đếm)
Ta có thể đếm được các tham số được chuyển đến script bằng biến `$#`
```
#!/bin/bash
echo "There were $# parameters passed."
```
```
./myscript 1 2 3 4 5
There were 5 parameters passed.
```
Ngoài ra ta có thể biết tham số cuối cùng mà script nhận bằng biến ${!#}

## Capturing all command-line options 
- Biến `$*` bao gồm tất cả các tham số được nhập từ dòng lệnh dưới dạng một cụm bao gồm cả khoảng trắng.
- Biến `$@` tương tự như `$*` nó cũng bao gồm tất cả các tham số nhưng nó phân biệt chúng thành các tham số riêng lẻ
```
#!/bin/bash
count=1
for param in "$*"
do
echo "\$* Parameter #$count = $param"
count=$(( $count + 1 ))
done
```
```
$* Parameter #1 = 1 2 5 6
```

```
#!/bin/bash
count=1
for param in "$@"
do
echo "\$@ Parameter #$count = $param"
count=$(( $count + 1 ))
done
```
```
$@ Parameter #1 = 1
$@ Parameter #2 = 2
$@ Parameter #3 = 3
$@ Parameter #4 = 4
$@ Parameter #5 = 5
```
## Shift command
- Shift sẽ làm mới biến đầu và chuyển giá trị của các biến sau lùi về một nhịp nó chỉ làm với $1 và $2


VD: Có `$1 $2 $3` khi gọi lệnh shift thì chỉ còn `$2 $3`.

`lưu ý` : máy tính sẽ hiểu là $1 mang giá trị của $2 và $2 mang giá trị của $3

```
#!/bin/bash
count=1
while [ -n "$1" ]
do
echo "Parameter #$count = $1"
count=$(( $count + 1 ))
shift
done
```
```
./myscript 1 2 3 4 5
Parameter #1 = 1
Parameter #2 = 2
Parameter #3 = 3
Parameter #4 = 4
Parameter #5 = 5
```
## Command-line switches
```
#!/bin/bash
echo
while [ -n "$1" ]
do
case "$1" in
-a) echo "Found the -a option" ;;
-b) echo "Found the -b option" ;;
-c) echo "Found the -c option" ;;
*) echo "$1 is not an option" ;;
esac
shift
done
```
```
$ ./myscript –a –b –c –d
Found the -a option
Found the -b option
Found the -c option
-d is not an option
```
-a -b -c là các nhánh mình cài đặt để có thể sử dụng lệnh.Khi ta gọi ra nhánh -a thì nó chỉ thực hiện việc của nhánh -a .Các nhánh khác cũng tương tự như vậy

## How to distinguish between keys and parameters (Cách phân biệt giữa nhánh và tham số)
- Để phân biệt giữa chúng thì ta sẽ dùng `--`
```
#!/bin/bash
while [ -n "$1" ]
do
case "$1" in
-a) echo "Found the -a option" ;;
-b) echo "Found the -b option";;
-c) echo "Found the -c option" ;;
--) shift
break ;;
*) echo "$1 is not an option";;
esac
shift
done
count=1
for param in $@
do
echo "Parameter #$count: $param"
count=$(( $count + 1 ))
done
```
```
./myscript -a -b -c -- 5 10 15
Found the -a option
Found the -b option
Found the -c option
Parameter #1: 5
Parameter #2: 10
Parameter #3: 15
```
Các nhánh sẽ là `-a -b -c` và các tham số sẽ là `5 10 15`

## Receiving data from the user
Đôi khi script cần dữ liệu mà người dùng phải nhập . Lúc đó ta sẽ nghĩ đến `read`
```
#!/bin/bash
echo -n "Enter your name: "
read name
echo "Hello $name, welcome to my program."
```
```
./myscript
Enter your name: Quang
Hello Quang, welcome to my program.
```
Lệnh read có chức năng gắn biến `name` thành `quang`

Ta có thể dùng biến `$REAPLY` để gắn giá trị mà cần người dùng nhập

```
#!/bin/bash
read -p "Enter your name: "
echo Hello $REPLY, welcome to my program.
```
```
./myscript
Enter your name: Quang
Hello Quang, welcome to my program.
```
Ta có thể giới hạn thời gian nhập từ người dùng bằng lệnh `read -t 5 -p`
```
#!/bin/bash
if read -t 5 -p "Enter your name: " name
then
echo "Hello $name, welcome to my script"
else
echo "Sorry, too slow!"
fi
```
```
./myscript
Enter your name: Sorry, to slow!
```
## Using standard keys
-a :Liệt kê tất cả đối tượng

-c :

-d : thư mục chỉ định

-e :mở rộng đối tượng

-f :Chỉ định tệp để đọc dữ liệu. 

-h : Trợ giúp lệnh hiển thị.

-i :bỏ qua

-l :Thực hiện kết xuất dữ liệu đầy đủ 

-n :sử dụng chế độ không tương tác

-o :Cho phép bạn chỉ định tệp mà bạn muốn chuyển hướng đầu ra. 

-q :Thực hiện lệnh trong chế độ tĩnh. 

-r :Tập tin và tập tin quy trình

-s :Thực hiện lệnh trong chế độ im lặng. 

-v :Thực hiện sản lượng dài dòng. 

-x :Loại trừ đối tượng. 

-y :Trả lời " có " với tất cả câu hỏi. 

