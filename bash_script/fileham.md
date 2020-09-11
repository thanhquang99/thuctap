```
#!/bin/bash
function banthan {
echo "toi la quang."
echo "toi sinh ngay 26/11/1999."
echo "hien nay toi dang hoc truong dai hoc bach khoa ha noi"
}
function congty {
echo " Hien nay toi dang thuc tap o cong ty nhan hoa ."
echo "dia chi cong ty laf 97-99 lang ha ."
echo "toi dang theo su huong dan cua anh to thanh cong thuc tap"
}

if [ $1 = banthan ]
then
        banthan
elif [ $1 = congty ]
then
        congty
fi
```
![alt](/images/anh.png)