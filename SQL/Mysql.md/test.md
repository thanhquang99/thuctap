```
mysql -uroot -pKhuongquang99
create database thutap;
use thutap;
create table giangvien(
     magv int primary key ,
     hotengv char(30) ,
     luong decimal(5,2)
     makhoa refrences khoa);
create table giangvien(
     magv int primary key,
     hotengv char(30),
     luong decimal(5,2),
     makhoa char(10) references khoa
     );
create table sinhvien(
     masv int primary key ,
     hotensv char(10) ,
     makhoa char(10) references khoa ,
     namsinh int ,
     quequan char(30)
     );
create table detai(
     madt int primary key ,
     tendt char(30) ,
     kinhphi int ,
     noithuctap char(30));
create table huongdan(
     masv int primary key ,
     madt int references detai,
     magv int references giangvien,
     ketqua decimal(5,2)
     );
	
	
	
	
insert into thuctap.khoa(makhoa ,tenkhoa ,dienthoai)
     values("me1" ,"co dien tu" ,"0979459172");
insert into thutap.giangvien
     values(20177777 ,"vu thi la" ,188888 ,"me1");
insert into thutap.sinhvien 
	 values(20170875 ,"khuongthanhquang" ,"me1" ,1999 ,"namdinh");
insert into thutap.detai 
	 values(111 ,"test mysql" ,0.0 ,"nhan hoa");
insert into thutap.huongdan 
	 values(20170875 ,111 ,20177777 ,6.7);

```

![alt](/images/Screenshot_14.png)
