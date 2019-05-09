## **Maria DB**

1. **Tổng quan**: Maria DB là một nhánh của MySQL (một trong những cơ sở dữ liệu phổ biến nhất thế giới), là máy chủ cơ sở dữ liệu cung cấp 

các 

chức năng thay thế cho MySQL. MariaDB được xây dựng bởi một số tác giả sáng lập ra MySQL được hỗ trợ của đông đảo các nhà phát triển phần mềm

mã nguồn mở. Ngoài việc thừa kế các chức năng cốt lõi của MySQL, MariaDB cung cấp nhiều tính năng cải tiến về cơ chế lưu trữ, tối ưu máy chủ.

MariaDB phát hành phiên bản đầu tiên vào 11/2008 bởi Monty Widenius, người đồng sáng lập ra MySQL. Monty Widenius sau khi nghỉ công tác cho 

MySQL (sau khi Sun mua lại MySQL) đã thành lập công ty Monty Widenius AB và phát triển MariaDB. Maria DB có các phiên bản cho các hệ điều 

hành khác nhau: Windows, Linux,... với các gói cài đặt tar, zip, MSI, rpm cho cả 32bit và 64bit. 

2. **Cài đặt Maria DB**

**Tải các gói rpm của Maria DB từ trên mạng xuống**

Trước tiên để tải gói, chúng ta phải tải gói hỗ trợ 

```
yum install yum-utils
```

Sau đó bắt đầu tải gói cần tải về máy bằng cú pháp sau, (Cú pháp này chỉ tải một gói tổng hợp có thể không đầy đủ)

```
yumdownloader --resolve --destdir=/root/b mariadb
```

Muốn tải các gói rpm đầy đủ thì ta sử dụng câu lệnh 

```
repotrack -a x86_64 -p /root/b mariadb
```

**Cấu hình một Yum Repository Server**

Copy các gói .rpm vào thư mục repository `/repos/centos/6`

```
# mkdir -p /repos/centos/6
# cp /root/b/*.rpm /repos/centos/6
```

Khởi tạo repository

```
# createrepo /repos/centos/6
```

Tạo file cấu hình repository mới

```
vim /etc/yum.repos.d/local.repo
```

Bên trong đó sửa file 

```
[local]
name=Local Repository
baseurl=file:///repos/centos/6
enabled=1
gpgcheck=0
```

Xóa bỏ cache và cài đặt qua local repo

```
# yum clean all
# yum install mc -y
```

Tiến hành cài đặt gói mariadb

```
yum install mariadb
```




