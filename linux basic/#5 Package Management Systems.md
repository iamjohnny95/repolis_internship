## **Package Management Systems**

- Phần core của các bản phân phối linux và hầu hết các add-on software đều được cài đặt qua hệ thống quản lý package. Mỗi package gồm files và các thành phần cần thiết để tạo lên một thành phần làm việc trên hệ thống.

- Có hai loại gói cài đặt một là source code, chưa được biên dịch nên khi sử dụng cần phải biên dịch để cho máy hiểu, cái này thường dùng cho dev nếu họ muốn đọc source code. Cái thứ hai là file binary (.deb, .rpm,...) file này đã được nhà phân phối biên dịch và và đóng gói cho user nên máy có thể hiểu được.

## **Các cách cài đặt** 

**Cài đặt Package từ  Repositoties**

- **yum**(yellowdog updater modified) là một công cụ quản lý và cài đặt phần mềm cho các hệ thống RedHat Linux 

- Mặc định **yum** tìm kiếm và tải về các gói nằm trong repo server, việc cài đặt phần mềm với yum yêu cầu phải có kết nối internet tốc độ cao để tải gói về được nhanh chóng. Repository(gọi tắt là repo) là hệ thống kho phần mềm của Linux được lưu trữ trên mạng internet thông qua hệ thống repo server cho phép các máy khác lấy file về cài đặt trong CentOS (và các dòng Redhat) thông tin về repo server được lưu trong các file .repo của thư mục /etc/yum.repos.d

```
# ls -l /etc/yum.repos.d
```

- File cấu hình yum **/etc/yum.conf**

```
#vi /etc/yum.conf
```
- Xóa cache **yum**

```
# yum clean all
# ls -l /var/cache/yum
```

- **EPEL** viết tắt của Extra Packages for Enterprise Linux do một nhóm người dùng Fedora (Fedora Special Interest Group) tạo ra, duy trì, và quản lý các phần mềm cho các bản phân phối Enterprise Linux như Red Hat Enterprise Linux (RHEL), CentOS và Scientific Linux (SL). EPEL là một repo mở, có thể được dùng bởi bất cứ người dùng Linux nào để cài đặt phần mềm tồn tại trên Fedora và không có phiên bản trên RHEL

```
# yum install epel-release -y
# cat /etc/yum.repos.d/epel.repo
```

**Add repo rpmforge**

**RHEL/CentOS 6 32-Bit** 

```
#wget http://apt.sw.be/redhat/el6/en/i386/rpmforge/RPMS/rpmforge-release-0.5.3-
1.el6.rf.i686.rpm
```

**RHEL/CentOS 6 64-Bit**

```
#wget http://apt.sw.be/redhat/el6/en/x86_64/rpmforge/RPMS/rpmforge-release-0.5.3-
1.el6.rf.x86_64.rpm
# rpm -ivh rpmforge-release-*.rpm
```

**Quản lý và cài đặt package với Yum Package Manager**

- Cài đặt gói phần mềm `yum install package-name`
Mặc định khi cài bằng lệnh `yum`, lệnh yêu cầu xác nhận cài đặt package, để bỏ qua bước này chỉ cần thêm option -y

- Cài đặt phần mềm morningtor hệ thống

```
# yum install htop -y
```

- Cài đặt tiện ích `yum`

```
# yum install yum-utils -y
```

Download package nhưng không cài đặt `yumdownloader package-name`

```
# yumdownloader gcc
```

Cài đặt theo repo chỉ định `yum --enablerepo=repo-name install package-name`

Cập nhật package mới `yum update package-name`

Cập nhật bash

```
# yum update bash -y
```
Gỡ bỏ gói phần mềm `yum remove package-name`

Tìm một phần mềm `yum search package-name`

Liệt kê các package có trong repo `yum list package-name`

Hiển thị thông tin cài đặt package `yum info package-name`

Kiểm tra log YUM
```
# tail -f /var/log/yum.log
```

**Cấu hình một Yum Repository Server**

- Mount đĩa cài Linux lên thư mục /media
```
# mount /dev/cdrom /media
```

- Cài đặt gói createrepo

```
# yum install createrepo -y
```

- Hoặc có thể cài đặt qua tiện ích rpm

```
# cd /media/Packages
# rpm -ivh createrepo-*.rpm python-deltarpm-*.rpm deltarpm-*.rpm
```

Copy các gói .rpm vào thư mục repository /repos/centos/6

```
# mkdir -p /repos/centos/6
# cp /media/Packages/mc-*.rpm /repos/centos/6
# cp /media/Packages/iptraf-*.rpm /repos/centos/6
```

- Khởi tạo repository
```
# createrepo /repos/centos/6
```
 - Tạo file cấu hình repository mới 
```
# vi /etc/yum.repos.d/local.repo

[local]
name=Local Repository
baseurl=file:///repos/centos/6
enabled=1
gpgcheck=0
```
- Xóa bỏ cache và cài đặt qua local repo
```
# yum clean all
# yum install mc -y
```

**Cấu hình repository qua http**

```
# yum install httpd -y
```


## **Quản lý gói Debian và Ubuntu**

- Hệ thống quản lý gói Debian, dựa trên một công cụ gọi là dpkg và hệ thống apt là một biện pháp hiệu quả, phổ biến và hữu ích của quản lý gói. Ngoài Debian, một số bản phân phối nổi bật khác của GNU/Linux có nguồn gốc từ hệ thống Debian, đáng chú ý là bản phân phối Ubuntu.

- **Công cụ nâng cao gói (APT)**
 Bạn có thể đã quen với apt-get, một lệnh trong đó sử dụng các công cụ đóng gói tiên tiến để tương tác với hệ thống gói của hệ điều hành. Các lệnh có liên quan và hữu ích nhất là (quyền được chạy với root):

 	- 




