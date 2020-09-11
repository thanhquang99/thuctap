# Functions and Library Development
Khi chúng ta viết một tập lệnh bash và muốn sử dụng lại một đoạn mã thì ta có thể tạo ra các hàm và sử dụng lại chúng

## Function declaration (Khai báo hàm)
```
functionName {
}
```
Hoặc
```
functionName() {
}
```
## Using functions
```
#!/bin/bash
function myfunc {
echo "This is an example of using a function"
}
count=1
while [ $count -le 3 ]
do
myfunc
count=$(( $count + 1 ))
done
echo "This is the end of the loop"
myfunc
echo "End of the script"
```
```
./myscript.sh
This is an example of using a function
This is an example of using a function
This is an example of using a function
This is the end of the loop
This is an example of using a function
End of the script
```
Trong đoạn script trên hàm `myfunc` đã được gọi ra và sử dụng 4 lần 

`Lưu ý :` Hàm phải được khai báo trước xong mới được sử dụng và Tên hàm phải là duy nhất ,nếu trùng thì hàm khai báo trước sẽ bị mất và chỉ dùng được hàm khai báo sau

## Using the return command
- Câu lệnh return quy định mã số nguyên được trả về bởi hàm
```
#!/bin/bash
function myfunc {
read -p "Enter a value: " value
echo "adding value"
return $(( $value + 10 ))
}
myfunc
echo "The new value is $?"
```
```
./myscript.sh
Enter a value: 10
adding value
The new value is 20
```
Nghĩa là 20 chính là mã số được trả về khi hàm kết thúc

## Writing the output of a function to a variable

Một cách khác để trả về kết quả công việc của một hàm là viết ra dữ liệu bằng hàm cho một biến. 

```
#!/bin/bash
function myfunc {
read -p "Enter a value: " value
echo $(( $value + 10 ))
}
result=$( myfunc)
echo "The value is $result"
```
```
./myscript.sh
Enter a value: 10
The value is 20
```
Trong câu lệnh `echo` đầu tiên thì đã gắn kết quả trả về cho hàm `myfunc`

## Function arguments

```
#!/bin/bash
function myfunc {
echo $(( $1 + $2 ))
}
if [ $# -eq 2 ]
then
value=$( myfunc)
echo "The result is $value"
else
echo "Usage: myfunc  a b"
fi
```
```
./myscript.sh 10 20
./myscript.sh: line 3: +  : syntax error: operand expected (error token is "+  ")
The result is
```
Khi chúng ta chay script trên thì sẽ bị báo lỗi như vậy. nhưng khi ta sửa script trên thành

```
#!/bin/bash
function myfunc {
echo $(( $1 + $2 ))
}
if [ $# -eq 2 ]
then
value=$(myfunc $1 $2)
echo "The result is $value"
else
echo "Usage: myfunc a b"
fi
```
```
./myscript.sh 10 20
The result is 30
```
Điều này có ý nghĩa rằng nếu hàm sẽ sử dụng các thông số được chuyển đến tập lệnh khi được gọi từ dòng lệnh, bạn phải chuyển chúng đến nó khi được gọi 

## Working with variables in functions

### Global variables

- Biến global là biến được hiển thị ở bất cứ đâu trong tập lệnh bash và theo mặc định thì tất cả các biến được khai báo trong tập lệnh đều được coi là biến global 

```
#!/bin/bash
function myfunc {
value=$(( $value + 10 ))
}
read -p "Enter a value: " value
myfunc
echo "The new value is: $value"
```
```
./myscript.sh
Enter a value: 10
The new value is: 20
```
- Khi một biến được gán một giá trị mới trong một hàm, giá trị mới đó không bị mất khi tập lệnh gọi nó sau khi hàm kết thúc

### Local variables
- là các biến được khai báo bên trong hàm .Để làm được điều này ta phải thêm từ `local` trước khi khai báo biến 
```
local temp=$(( $value + 5 ))
```
Nếu có một biến cùng tên bên ngoài hàm thì nó sẽ không bị ảnh hưởng

```
#!/bin/bash
function myfunc {
local temp=$[ $value + 5 ]
echo "The Temp from inside function is $temp"
}
temp=4
myfunc
echo "The temp from outside is $temp
```
```
./myscript.sh
The Temp from inside function is 5
The temp from outside is 4
```
## Passing Arrays to Functions as Arguments
Truyên các mảng tới các hàm như đối
```
#!/bin/bash
function myfunc {
echo "The parameters are: $@"
arr=$1
echo "The received array is ${arr[*]}"
}
myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}"
myfunc $myarray
```
```
./myscript.sh
The original array is: 1 2 3 4 5
The parameters are: 1
The received array is 1
```
Mảng myarray được khai báo trong `()` và đã được truyền tới hàm .Chú ý dấu `*` có nghĩa là tất cả 

Để giải quyết vấn đề này, cần phải trích xuất dữ liệu có trong đó từ mảng và chuyển chúng đến hàm độc lập. Nếu cần, bên trong hàm, các đối nhận được bởi nó có thể được gộp lại thành một mảng: 

```
#!/bin/bash
function myfunc {
local newarray
newarray=("$@")
echo "The new array value is: ${newarray[*]}"
}
myarray=(1 2 3 4 5)
echo "The original array is ${myarray[*]}"
myfunc ${myarray[*]}
```
```
./myscript.sh
The original array is 1 2 3 4 5
The new array value is: 1 2 3 4 5
```
các số trong mảng myarray đã được truyền cho newarray 

## Recursive functions
 Đệ quy là một hàm gọi chính mình
 
 ```
 1! = 11
 x! = x * (x-1)!
 ```
 Đây chính là ví dụ về hàm đệ quy `x!` sẽ được xác định thông qua `(x-1)!`

 ```
 #!/bin/bash
function factorial {
if [ $1 -eq 1 ]
then
echo 1
else
local temp=$(( $1 - 1 ))
local result=$(factorial $temp)
echo $(( $result * $1 ))
fi
}
read -p "Enter value: " value
result=$(factorial $value)
echo "The factorial of $value is: $result"
```
```
./myscript.sh
Enter value: 5
The factorial of 5 is: 120 
```
`120 = 4*3*5`

Đệ quy ở đây chính là biến `temp` một lần là 4 và một lần là 3

## Creating and using libraries
- Để tạo một thư viện dùng trong các tập lệnh thì ta có thể dùng cách sau 
.Thêm dấu `.` trước câu tập tin

```
#!/bin/bash
. ./myfuncs
result=$(addnum 10 20)
echo "The result is: $result"
```
 Ở ví dụ này thì ta có thể sử dụng kết quả của script `myfuncs` mà không cần khai báo trong script này

 ```
 . /home/thanhquang/myfuncs
 ```
 Ta có thể gọi ra đường dẫn của hàm myfuncs

 [Tài liệu tham khảo](https://medium.com/swlh/bash-scripts-part-6-functions-and-library-development-2411adbf962)