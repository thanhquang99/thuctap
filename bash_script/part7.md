# Part 7 — Word Processing With Sed
## Sed basics
Câu lệnh `Sed` được dùng để chỉnh sửa file  bàn phím ,có thể được dùng để thêm ,xóa, thay đổi văn bản

Cấu trúc của câu lệnh `sed`
```
sed options file
```
```
echo "This is a test" | sed 's/test/another test/'
This is a another test
```
Như ở ví dụ trên thì khi sử dụng câu lệnh `sed` đã chỉnh sửa từ `test` thành từ `another test` trong câu lệnh `echo` 

```
cat myfile
This is a test
```
```
sed 's/test/another test' ./myfile
This is a another test
```
Khi chúng ta sử dụng lệnh sed như này thì sẽ không làm thay đổi data trong myfile đâu .Nó tương tự như một câu lệnh cat là hiển thị nội dung file nhưng khác biệt ở đây là nó đã chỉnh sửa nội dung .
```
cat myfile
This is a test
```
## Executing command sets when invoking sed
Để thực hiện nhiều thay đổi trong câu lệnh sed thì ta dùng từ khóa `-e`
```
sed -e 's/This/That/; s/test/another test/' ./myfile
That is a another test
```
Dấu `;` dùng để ngăn cách các từ được thay thế
## Reading commands from a file
Ta có thể đưa nhiều lệnh vào một tập tin và khi dùng nó để chỉnh sửa với câu lệnh `sed` thì dễ dàng hơn và không phải liệt kê lại .Nhưng khi ta muốn sử dụng tính năng này ta phải sử dụng từ khóa `-f`

Đây là nội dung trong file mycommands
```
s/This/That/
s/test/another test/
```
Và khi ta chạy lệnh sau thì màn hình hiển thị

```
sed -f mycommands myfile
That is a another test
```

## Replacement command flags
```
cat myfile
This is a test and I like this test.
This is the next test of the test scripts.

sed 's/test/another test/' myfile
This is a another test and I like this test.
This is the next another test of the test scripts.
```
Ở ví dụ trên ta thấy từ `test` chỉ được thay thế ở mỗi từ đầu tiên xuất hiện trong mỗi dòng.Để khắc phục điều đó ta hãy sử dụng `flags`. Ta sẽ thêm từ flags vào mỗi cặp từ thay thế-được thay thế.
```
s/pattern/replacement/flags
```

- `g` xử lí tất cả các từ trùng với từ được thay thế 
- `p` hiển thị nội dung của chuỗi gốc
- `w file` Ghi kết quả xử lí vào một file
```
sed 's/test/another test/2' myfile
This is a test and I like this another test.
This is the next test of the another test scripts.
```
```
sed 's/test/another test/g' myfile
This is a another test and I like this another test.
This is the next another test of the another test scripts.
```
Khi chúng ta sử dụng flag `p` và kèm theo key `-n` thì nó sẽ chỉ hiển thị ra dòng thay đổi.
```
cat myfile
This is a test.
This is a different one.

sed -n 's/test/another test/p' myfile
This is a another test.
```
```
~$ sed 's/test/another test/w output' myfile
This is a another test.
This is a different one.
~$ cat output
This is a another test.
```

## Separators 


## Selecting text fragments for processing

Trong một số trường hợp chỉ cần sửa một phần của văn bản như là một dòng hay một nhóm dòng thì ta có 2 cách
- Đặt giới hạn về số lượng hàng sử lí
- Chỉ định bộ lọc mà các hàng sử lí

```
cat myfile
This is a test.
This is the second test.
This is the third test.
This is the fourth test.
```
```
sed '2,3s/test/another test/' myfile
This is a test.
This is the second another test.
This is the third another test.
This is the fourth test.
```
Ở đây ta thấy rằng chỉ sử chữ ở dòng thứ 2 và 3

```
sed '2,$s/test/another test/' myfile
This is a test.
This is the second another test.
This is the third another test.
This is the fourth another test.
```
Ở đây ta lại thấy rằng nó sẽ sửa từ dòng thứ 2 đến cuối

## Deleting lines
```
sed '3d' myfile
```
Đây là câu lệnh xóa dòng thứ 3 của text myfile

```
sed '3,$d' myfile
```
Còn đây là lệnh xóa dòng thứ 3 đến hết của text myfile

```
sed '/test/d' myfile
```
Đây là cấu trúc xóa dòng chữ có chữ test. và để xóa nhiều dòng một lúc thì ta có thể dùng từ cấu trúc lệnh sau :
```
sed '/second/,/fourth/d' myfile
```

## Inserting text into a stream
Chèn văn bản vào dòng :
- `i` : thêm một dong mới trước dòng đã cho
- `a` : thêm mọt dòng mới ssau dòng đã cho

```
echo "Another test" | sed 'i\First test '
First test
Another test
```
```
echo "Another test" | sed 'a\First test '
Another test
First test
```
Dưới đây là ví dụ về thêm 1 dòng vào sau dòng thứ 2 và thêm vào trước dòng thứ 2 thì ta chỉ việc thay chứ `i` thành chữ `a`.

```
sed '2i\This is the inserted line.' myfile
This is a test.
This is the inserted line.
This is the second test.
This is the third test.
This is the fourth test.
This is another line.
``` 

## Replacing strings

```
sed '3c\This is a modified line.' myfile
This is a test.
This is the second test.
This is a modified line.
This a the  fourth test.
This another line.
``` 
Đây là ví dụ về thay thế một chuối ctrong dòng thứ 3 của myfile

```
 cat myfile
This is a test.
This is the second test.
This is the third test.
This is the fourth test.
This is another line.


sed '/This is/c This is a changed line of text.' myfile
This is a changed line of test.
This is a changed line of test.
This is a changed line of test.
This is a changed line of test.
This is a changed line of test.
```
Tất cả các dòng nào có chữ `This is` đều được thay thế 

## Replacing characters
 Để thay thế kí tự thì ta dùng câu lệnh `y`
 ```
 cat myfile
This is a test.1
This is the second test.2
This is the third test.3
This is the fourth test.4
This is another line.5
```
```
sed 'y/123/567/' myfile
This is a test.5
This is the second test.6
This is the third test.7
This is the fourth test.4
This is another line.5
```
 Các kí tự `123` được thay thế bằng kí tự `567`tương ứng

 ## Displaying line numbers
 Ta có thể sử dụng câu lênh `=` để chỉ dòng thứ bao nhiêu ta muốn hiển thị

 ```
 sed '=' myfile
1
This is a test.
2
This is the second test.
3
This is the third test.
4
This is the fourth test.
5
This is another line
```
Và ta có thể hiện thị dòng số mấy có chữ chúng ta muốn tìm

```
sed -n '/test/=' myfile
1
2
3
4
```

## Reading data to insert from a file
Ta có thể chèn nội dung của một file vào sau dòng chỉ định của một file khác bằng câu lệnh  `r`
```
~$ cat newfile
First line in newfile
Second line in newfile
~$ sed '3r newfile' myfile
This is a test.
This is the second test.
This is the third test.
First line in newfile
Second line in newfile
This is the fourth test.
This is another line.
```
```
sed '/test/r newfile' myfile
This is a test.
First line in newfile
Second line in newfile
This is the second test.
First line in newfile
Second line in newfile
This is the third test.
First line in newfile
Second line in newfile
This is the fourth test.
First line in newfile
Second line in newfile
This is another line
```
Ở ví dụ này thì sau mỗi dòng có chứ test sẽ được thay thế bằng nội dung của newfile 

[Tài liệu tham khảo](https://medium.com/introduction-into-bash/bash-scripts-part-7-word-processing-22b1fe98c988)