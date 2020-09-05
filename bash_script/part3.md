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

