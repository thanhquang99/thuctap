# Signals and Background Tasks
## Linux signals (Tín hiệu linux)
- SHIGUP : Nếu bash nhận được một tín hiệu shigup thì khi bạn đóng termial thì nó sẽ gửi đến tất cả các chương trình đang chạy và đóng nó lại 

- SHIGNT : Tín hiệu này dùng để tạm dừng công việc

## Sending signals to scripts
### Terminating the process
- Khi bạn gõ ` ctrl + C ` thì nó sẽ gửi đi một tín hiệu `SHIGNT` cho tất cả các chương trình đang chạy trong shell
### Temporarily stopping the process
- Khi bạn gõ `ctrl + Z` thì sẽ gửi đi một tín hiệu `SHIGTP` nó sẽ tạm dừng các chương trình đang chạy.Một quá trình như thế vẫn còn trong trí nhớ và có thể được tiếp tục chạy lệnh trong shell
```
$ sleep 100
^Z
[1]+   Stopped            sleep 100
```
Số trong ngoặc vuông là số công việc mà shell gán cho quá trình. Shell đối xử với các quá trình chạy trong đó là những công việc được đánh số duy nhất. Quá trình đầu tiên được gán số 1, thứ hai là số 2, vân vân. 

Bạn có thể xem các tác vụ bị tạm ngưng với lệnh sau: `ps -l`
```
F S   UID    PID   PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
4 S     0   1873   1865  0  80   0 - 28886 do_wai pts/0    00:00:00 bash
0 T     0   2107   1873  0  80   0 - 27013 do_sig pts/0    00:00:00 sleep
4 S     0   2214   1873  0  80   0 - 28886 do_wai pts/0    00:00:00 bash
0 R     0   2510   2214  0  80   0 - 38337 -      pts/0    00:00:00 ps
```
Nếu bạn muốn chấm dứt quá trình tạm dừng bạn có thể dùng câu lệnh `kill`
```
kill processID
```
## Intercept signals
Để bật theo dõi tín hiệu linux trong tập lệnh, ta có thể sử dụng lệnh `trap` 

Nếu script nhận được tín hiệu chỉ định khi gọi lệnh này, nó sẽ tự xử lý nó, và shell sẽ không xử lý tín hiệu như thế. 

```
#!/bin/bash
trap "echo ' Trapped Ctrl-C'" SIGINT
echo This is a test script
count=1
while [ $count -le 10 ]
do
echo "Loop #$count"
sleep 1
count=$(( $count + 1 ))
done
```
```
./myscript
This is a test script
Loop #1
Loop #2
Loop #3
^C Trapped Ctrl-C
Loop #4
Loop #5
Loop #6
Loop #7
^C Trapped Ctrl-C
Loop #8
Loop #9
Loop #10
```
Ở đây ta đã gắn mỗi khi ta nhấn tổ hợp phím `CTRL +C` thì nó sẽ tạo ra một tín hiệu `SHIGNT` và script này chỉ dừng khi đã chạy hết shell không can thiệp vào quá trình này

## Intercept the script exit signal
```
#!/bin/bash
trap "echo Goodbye..." EXIT
count=1
while [ $count -le 5 ]
do
echo "Loop #$count"
sleep 1
count=$(( $count + 1 ))
done
```
```
./myscript
Loop #1
^CGoodbye...
raevskym@DESKTOP-JNF3L6H:~/bash_course$ ./myscript
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Goodbye...
```
Khi nhận được tín hiệu `exit` thì nó sẽ dừng luôn script và không thực hiện nữa .Bạn có thể dùng `ctrl +C` để thử

## Modification of intercepted signals and cancellation of interception
```
#!/bin/bash
trap "echo 'Ctrl-C is trapped.'" SIGINT
count=1
while [ $count -le 5 ]
do
echo "Loop #$count"
sleep 1
count=$(( $count + 1 ))
done
trap "echo ' I modified the trap!'" SIGINT
count=1
while [ $count -le 5 ]
do
echo "Second Loop #$count"
sleep 1
count=$(( $count + 1 ))
done
```
```
./myscript
Loop #1
^CCtrl-C is trapped.
Loop #2
Loop #3
Loop #4
Loop #5
Second Loop #1
Second Loop #2
^C I modified the trap!
Second Loop #3
Second Loop #4
Second Loop #5
```
- Để hủy tín hiệu mà ta đã gán ta có thể sử dụng lệnh `trap -- SIGINT` . Trong đó `SHIGNT` là tín hiệu mà ta đã gắn
```
#!/bin/bash
trap "echo 'Ctrl-C is trapped.'" SIGINT
count=1
while [ $count -le 5 ]
do
echo "Loop #$count"
sleep 1
count=$(( $count + 1 ))
done
trap -- SIGINT
echo "I just removed the trap"
count=1
while [ $count -le 5 ]
do
echo "Second Loop #$count"
sleep 1
count=$(( $count + 1 ))
done
```
```
./myscript
Loop #1
^C Ctrl-C is trapped.
Loop #2
Loop #3
Loop #4
Loop #5
I just removed the trap
Second Loop #1
Second Loop #2
^C
```
Ở vòng lặp thứ 2 thì đã bị mất đi tín hiêu `SHIGNT` nên script sẽ dừng luôn 
## Executing command line scripts in the background
Khi chúng ta muốn chạy script và muốn làm thêm nhiều việc khác nữa thì ta có thể để script chạy trong nên và không hiển thị ra 

Để làm được điều đó thì ta có thể thêm dấu `&` sau lệnh chạy script
```
#!/bin/bash
count=1
while [ $count -le 10 ]
do
sleep 1
count=$(( $count + 1 ))
done
```
```
./spript &
[2] 3012
```
Như vậy là trong quá trình script chạy ta có thể làm việc khác rồi . Tuy nó được thực hiện nhưng chúng ta vẫn có thể thấy nó trong câu lệnh `ps -l`

## Executing scripts that do not exit when the terminal is closed

Để thực hiện lệnh ngay cả khi termianl session đóng thì ta phải thêm `nohup` vào đầu lệnh chạy script
```
 nohub ./myscript &
 ```

## View assignments
 - Câu lệnh `jobs` cho phép bạn xem các câu lệnh đang chạy trong shell 
 ```
 #!/bin/bash
count=1
while [ $count -le 10 ]
do
echo "Loop #$count"
sleep 10
count=$(( $count + 1 ))
done
```
```
 ./myscript
Loop #1
^Z
[1]+  Stopped             ./myscript
```
```
 ./myscript > outfile &
[2] 89
```
```
jobs -l
[1]+ 99 Stopped         ./myscript
[1]- 89 Running         ./myscript > outfile &
```

## Restarting suspended jobs
 - Để restart script mà ta đã dừng khi `ctrl +z` thì ta có thể sử dụng câu lệnh `bg`
- Để khởi động lại nhiệm vụ trong chế độ bình thường, hãy sử dụng command `fg`
 
 ## Scheduling scripts to run
 Ta có thể hẹn giờ để chạy lệnh như crontab
 ```
 at [-f filename] time
 ```
 `Lưu ý :` Một số thời gian đặc biêt 

- Tiêu chuẩn xác định định dạng ngày trong đó ngày được viết trên mẫu  MMDDYY, MM/DD/YYor DD.MM.YY.

 - now, noon, midnight.
 
 -
 
now + 25 minutes.   
10:15PM tomorrow.    
10:15 + 7 days.

Để xem danh sách tác vụ cần sử lí ta có thể sử dụng câu lênh `atq`
 
 ## Removing pending jobs
 Để xóa tác vụ cần sử lí ta có thể dùng lệnh `atrm` và kèm theo thứ tự của tác vụ đó 
 ```
 atrm 1
 ```
Có nghĩa là ta đã xóa tác vụ thứ nhất

Ta còn có thể chạy một script trên một lịch cụ thể bằng tính năng crontab của linux 



[Tài liệu tham khảo](https://medium.com/swlh/bash-scripts-part-5-signals-and-background-tasks-4dbe5922aea3)