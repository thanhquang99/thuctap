# Input and Output
## Standard file descriptors (Tập tin tiêu chuẩn)
Mọi thứ trên LINUX đều là file bao gồm cả đầu vào và đầu ra

Mỗi quy trình được phép có đến 9 tập tin mở. Bash shell dự trữ 3 descriptors đầu tiên với id 0, 1, và 2. Và nó có ý nghĩa này. 

- 0,STDIN -Đầu vào
- 1,STDOUT -Đầu ra
- 2,STDERR -Đầu ra lỗi

## STDIN (standard input)

STDIN chính là đầu vào chuẩn của shell

Ví dụ đối với terminal thì STDIN chính là bàn phím mà chúng ta dùng để nhập lệnh

Nhiều câu lệnh trong bash lấy input từ STDIN ví dụ như câu lệnh `cat` ,ngoại trừ một số lệnh đặc biệt lấy input từ việc truy suất dữ liệu

## STDOUT (standard output)
Theo mặc định thì STDOUT chính là màn hình. 
## STDERR ( standard error stream)

Theo mặc định, xử lý này chỉ ra một thứ mà nó chỉ đến stdout, đó là lý do tại sao khi một lỗi xảy ra, chúng ta thấy một thông báo trên màn hình. Nó như một STDOUT đã có sẵn để chỉ đây là lỗi

### Redirect error stream
```
ls -l xfile 2> myfile
raevskym@DESKTOP-JNF3L6H:~/bash_course$ cat ./myfile
ls: cannot access 'xfile': No such flie or directory
```
- Để sử dụng dữ liệu đầu ra thì ta sử dụng `>` Nghĩa là dữ liệu đầu ra của file trước sẽ ghi vào file sau.

### Redirecting error and output streams
```
ls –l myfile xfile anotherfile 2> errorcontent 1> correctcontent
cat ./correctcontent
myfile
cat ./errorcontent
ls: cannot access '-l': No sudh file or directory
ls: cannot access 'xfile': No such file or directory
ls: cannot access 'anotherfile': No such file or directory
```
- Ở đây ta có thể hiểu rằng nếu mô tả lỗi của `-l myfile xfile anotherfile` sẽ được chuyển hướng đến `errorcontent` và mô tả đầu ra chuẩn sẽ chuyển hướng đến `corectcontent`.Vì `myfile` của mình đã tạo ra trong lần trước nên sẽ chuyển đến `correctcontent`

`Lưu ý `: Khi chúng ta muốn dùng cả `2>` và `1>` thì ta có thể dùng `&>`

## Redirecting output in scripts
Có hai cách chuyển hướng đầu ra của script
- Temporarily redirecting output ( Chuyển tạm thời )
- Permanently redirecting (Chuyển vĩnh viến)

### Temporarily redirecting output
```
#!/bin/bash
echo "This is an error" >&2
echo "This is normal output"
```
```
./myscript
This is an error
This is normal output
```
Khi ta chạy myscript thì nó sẽ in ra tất cả vì theo mặc định lõi được hiển thị cùng một địa điểm với một dữ liệu bình thường

```
./myscript 2> content
This is normal output
cat ./content
This is an error
```
### Permanent output redirection
```
#!/bin/bash
exec 1>outfile
echo "This is a test of redirecting all output"
echo "from a shell script to another file."
echo "without having to redirect every line"
```
```
./myscript
cat outfile
This is a test of redirecting all output
from a shell script to another file.
without having to redirect every line
```

- Để sử dụng chuyển hướng vĩnh viến thì ta dùng câu lệnh `exec`. Như trong ví dụ trên ta sẽ chuyển hướng đầu ra chuẩn của myscript đến outfile , Nên khi ta chạy `myscript` sẽ không có gì in ra mà nó đã được chuyển đến `outfile` rồi .

```
#!/bin/bash
exec 2>myerror
echo "This is the start of the script"
echo "now redirecting all output to another location"
exec 1>myfile
echo "This should go to the myfile file"
echo "and this should go to the myerror file" >&2
```
```
./myscript
This is the start of the script
now redirecting all output to another location
```
```
cat ./myerror
and this should go to the myerror file
```
```
cat ./myfile
This should go to the myfile file
```

Do hai câu echo đầu là STDOUT nên không được chuyển đến `myerror`.Câu echo thứ 3 là STDOUT nên được chuyển dến `myfile` và câu echo cuối là STDERR nên được chuyển đến `myerror`

## Redirecting input in scripts
```
#!/bin/bash
exec 0< testfile
count=1
while read line
do
echo "Line #$count: $line"
count=$(( $count + 1 ))
done
```
```
./myscript
Line #1: this is the first line
Line #2: this is the second line
Line #3: this is the third line
```
Ở trong ví dụ này ta sẽ hiểu rằng testfile chính là đầu vào chuẩn của line và từng dòng trong testfile chính là $line

## Creating your own output redirection
```
#!/bin/bash
exec 3>myfile
echo "This should display on the screen"
echo "and this should be stored in the file" >&3
echo "And this should be back on the screen"
```
```
./myscript
This should display on the screen
And this should be back on the screen
```
```
cat ./myfile
and this should be stored in the file
```
Mình sẽ sử dụng số `3` để ám chỉ đầu ra của riêng mình và chỉ có câu 
echo thứ 2 là đầu ra của riêng mình được chuyển đến `myfile`

## Creating file descriptors for data input
```
#!/bin/bash
exec 6<&0
exec 0< myfile
count=1
while read line
do
echo "Line #$count: $line"
count=$(( $count + 1 ))
done
exec 0<&6
read -p "Are you done now? " answer
case $answer in
y) echo "Goodbye";;
n) echo "Sorry, this is the end.";;
esac
```
```
./myscript
Line #1: First line
Line #2: Second line
Line #3: Third line
Are you done now? y
Goodbye
```
```
./myscript
Line #1: First line
Line #2: Second line
Line #3: Third line
Are you done now? n
Sorry, this is the end.
```

Ở ví dụ này mình chọn số `6` chính là biến tham chiếu để mình sử dụng cho input của câu lệnh `read`

## Closing file descriptors

Shell sẽ tự động đóng tập tin descriptors sau khi tập lệnh kết thúc. Tuy nhiên, trong một số trường hợp, cần phải đóng thủ công trước khi tập lệnh kết thúc ,ta sử dụng  `&-` để đóng.

## Retrieving information about open handles
lsof(list open files): là lệnh được sử dụng để liệt kê thông tin về các tệp được mở bởi các quy trình khác nhau.
- -p : cho phép bạn chỉ định id của chương trình
- -d cho phép bạn chỉ định các con số mô tả mà bạn muốn xem
```
lsof -a -p $$ -d 0,1,2
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
bash    2954 root    0u   CHR  136,0      0t0    3 /dev/pts/0
bash    2954 root    1u   CHR  136,0      0t0    3 /dev/pts/0
bash    2954 root    2u   CHR  136,0      0t0    3 /dev/pts/0
```
## Output suppression
Đôi khi bạn cần đảm bảo rằng các lệnh trong tập lệnh, chẳng hạn, có thể được thực hiện như một quy trình nền, không hiển thị bất cứ thứ gì trên màn hình. Đó chính là lúc mà ta sử dụng /dev/null

```
ls -al badfile anotherfile 2> /dev/null
```
Phương pháp tương tự được sử dụng nếu, chẳng hạn bạn cần dọn dẹp một tập tin mà không xóa nó 
```
cat /dev/null > myfile
```

[Tài liệu tham khảo](https://medium.com/introduction-into-bash/bash-scripts-part-4-input-and-output-48e6b238dba3)