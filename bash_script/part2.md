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
