# BASH SCRIPTS
## PART 1 : BẮT ĐẦU

1. Bash script là dòng lệnh được viết cho bash shell

Các tập dòng lệnh là tập hợp các lệnh được nhập từ bàn phím và được ghép thành các tập tin .NNói về dòng lệnh nó cho phép bạn thực hiện vài lệnh một lần và được phân tách bằng dấu [ ; ]

```
pwd ; whoami
```
Tập lệnh trên sẽ hoạt động như thế này.Đầu tien nó sẽ hiển thị thông tin về thư mục hiện tại tiếp theo nó sẽ hiển thị thông tin về người dùng đó , cái mà bạn đã đăng nhập

Sử dụng cách này bạn có thể kết hợp nhiều lệnh với nhau trên một dòng .Để biết giới hạn lệnh ta có thể dùng câu lệnh này để kiểm tra:
```
getconf ARG_MAX
 ```
Dòng lệnh là một công cụ tuyệt vời nhưng khi bạn dùng chúng bạn phải viết lại toàn bộ lệnh nhưng khi bạn lưu chúng vào một file thì bạn có thể thực hiện các lệnh đó bằng cách gọi tên file đó
2. Cách mà Bash script hoạt động

 Tạo một tập lệnh bằng ` touch ` và ở trong dòng đầu tiên chúng ta cần khai báo chúng sử dụng shell nào,chúng ta thường làm ở bash
```
#!/bin/bash
```
Những dòng khác trong bash thì kí hiệu [#] dùng để biểu thị một comment mà shell không sử lí .Nhưng dòng đầu tiên có thêm dấu [!] là trường hợp đặc biệt chỉ đường dẫn đến bash

Các lệnh shell được phân tách bằng nguồn cấp dữ liệu dòng, nhận xét được phân tách bằng dấu băm
```
#!/bin/bash
# This is a comment
pwd
whoami
```
Ở đây chúng ta có thể viết mỗi lệnh trên một dòng để dễ nhìn và dễ đọc hơn

3. Phân quyền cho các script file

Khi bạn tạo ra một script file thì nó sẽ không có quyền thực thi mà bạn phải cấp quyền cho nó. Để cấp quyền cho nó ta sử dụng lệnh sau :
```
chmod +x ./myscript
```
Trong đó myscript là tên script file mà ta tạo .

Để thực thi file thì ta sử dụng lệnh sau:
```
./myscript
```
4. Hiển thị messages
```
#!/bin/bash
# our comment is here
echo "The current directory is:"
pwd
echo "The user logged in is:"
whoami
```
Khi chúng ta chạy file thì mà hình sẽ hiển thị

![alt](/images/Screenshot_1.png)

5. Sử dụng các biến 

Có hai loại biến được sử dụng trong bash scripts
Biến môi trường và biến người dùng
- Biến môi trường (Environment Variables)
Biến môi trường là các biến mà hệ thống đã có sãn và được gọi ra khi chúng ta sử dụng dấu [$] trước biến đó
```
#!/bin/bash
# display user home
echo "Home for the current user is: $HOME"
```
Và khi chúng ta chạy file sẽ có hiển thị 
```
Home for the current user is: /root
```
Do tôi đang sử ở root
- Biến người dùng (User variables)

Biến người dùng là do người dùng tự tạo ra và hệ thống sẽ hiểu được
```
#!/bin/bash
# testing variables
grade=5
person="Quang"
echo "$person is a good boy, he is in grade $grade"
```
Ở đây ta gắn biến ` grade=5` và `person=Quang` và khi gọi biến ta phải thêm dấu $ vào trước biến

` Lưu ý khi gắn biến không được dùng dấu cách`

Khi chạy file thì màn hình sẽ hiển thị 
```
Quang is a good boy, he is in grade 5
```
6. Phép thay thế lệnh 

Một trong những tính năng hữu ích nhất của bash script là khả năng trích xuất thông tin từ đầu ra của lệnh và gán nó cho các biến, cho phép thông tin này được dùng ở bất cứ đâu trong tập tin tập lệnh. 
```
#!/bin/bash
mydir=$(pwd)
echo $mydir
```
```
/home/thanhquang
```
7. Phép toán

Để thực hiện các thao tác toán học trong tập tin tập lệnh, bạn có thể dùng một cấu trúc $((a + b)): 
```
#!/bin/bash
var1=$(( 5 + 5 ))
echo $var1
var2=$(( $var1 * 2 ))
echo $var2
```
Khi chạy filefile
```
10
20
```
- Câu lệnh ` if-then`
```
if <some-condition>
then
<some-commands-go-here>
fi
```
nếu thỏa mãn điều kiện trong ` if ` thì sẽ thực hiện câu lệnh sau ` then `
```
#!/bin/bash
user=thanhquang
if grep $user /etc/passwd
then
echo "The user $user Exists"
fi
```
```
 ./myscript
thanhquang:x:1000:1000::/home/thanhquang:/bin/bash
The user thanhquang Exists
```
Ở đây chúng ta sử dụng lệnh grep để tìm một nhguoiwf dùng trong tập tin ` /etc/passwd ` nếu không có thì sẽ không hiển thị gì

- Câu lệnh ` if-then-else`
```
if <some-condition>
then
<some-commands>
else
<some-commands>
fi
```
Nếu thỏa mãn điều kiện trong `if` thif thực hiện lệnh sau `then` còn nếu không thì thực hiện lệnh sau `else`
```
#!/bin/bash
user=anotherUser
if grep $user /etc/passwd
then
echo "The user $user Exists"
else
echo "The user $user doesn’t exist"
fi
```
```
The user anotherUser doesn't exist
```
```
if <condition-1>
then
<some-commands>
elif <condition-2>
then
<some-other-commands>
fi
```
nếu thỏa mãn điều kiện trong `if` thì thực hiện câu lệnh sau `then1` nếu thỏa mãn điều kiện trong `elif` thì thực hiện câu lệnh sau `then2`


- So sánh số

-eq: bằng

-ge: lớn hơn hoặc bằng

-gt: lớn hơn

-le: bé hơn hoặc bằng

-lt: bé hơn

-ne: khác

- String comparison (so sánh chỗichỗi)

Tương tự như so sánh số so sánh chuỗi cũng có các toán tử tương tự

str1 = str2 :trả về true nếu str1 = str2

str1 != str2 :trả về true nếu str1 khác str2

str1 < str2:trả về true nếu str1 < str2

str1 > str2:trả về true nếu str1 > str2

-n str1 :trả về true nếu length str1 lớn hơn 0

-z str1 :trả về true nếu lenth str1 bằng 00

```
#!/bin/bash
user ="thanhquang"
if [$user = $USER]
then
echo "The user $user  is the current logged in user"
fi
```
```
The user thanhquang is the current logged in user
```
` Lưu ý :khi dùng dấu >,< thì phải thêm \ đằng trước các dấu đó `
```
#!/bin/bash
val1=text
val2="another text"
if [ $val1 \> $val2 ]
then
echo "$val1 is greater than $val2"
else
echo "$val1 is less than $val2"
fi
```
```
./myscript: line 5: [: too many arguments
text is less than another text
```
Dù tập lệnh được thực hiện nhưng lại có cảnh báo để loại bỏ cảnh báo này ta hãy sửa 

`if [ $val1 \> "$val2" ]`

```
sort ./myfile
```
```
raevskym
Raevskym
```
Khi chúng ta sử dụng lệnh sort thì nó sẽ sắp xếp ngược lại theo ngôn ngữ hệ thống (nghĩa là nó đảo ngược lại sắp xếp)

8. File check

Các lệnh check file 

`-d file` :kiểm tra nếu tập tin tồn tại và là một thư mục

`-e file` :kiểm tra nếu tập tin tồn tại

`-f file` :kiểm tra nếu tập tin tồn tại và là file

`-r file` :kiểm tra nếu file tồn tại và có thể đọc được

`-s file П` :kiểm tra nếu file tồn tại và là file trống

`-w file` :kiểm tra nếu file tồn tại và có thể viết được

`-x file` :kiểm tra nếu file tồn tại và có thể thực thi được

`file1 -nt file2` :kiểm tra nếu file1 mới hơn file2

`file1 -ot file2 `:kiểm tra nếu file1 cũ hơn file2

`-O file` :kiểm tra xem file có tồn tại và thuộc quyền sở hữu của người dùng hiện tại hay không

`-G file` : kiểm tra xem file có tồn tại và thuộc quyền sở hữu của group hiện tại hay không

