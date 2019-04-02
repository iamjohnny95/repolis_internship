# Tìm hiểu về HTTP và dựng Webserver

## Webserver

##  Apache là gì?

Apache là một phần mềm mã nguồn mở miễn phí được cài đặt trên các máy chủ web server (phần cứng) để xử lý các yêu cầu gửi tới máy chủ dưới giao thức HTTP.

## Cài đặt cấu hình dịch vụ web:

- Để cài đặt apache sử dụng lệnh 

`#yum –y install httpd` 

- Tạo thư mục cho website 

```
mkdir /var/www/html/website
```

- Tạo một website

```
vi /var/www/html/website/trangchu.html
```

- Cấu hình dịch vụ html

```
vi /etc/httpd/conf/httpd.conf
```

- Sau khi vào file cấu hình thì cần chú ý các options sau đây:

`ServerRoot "/etc/httpd"` chứa file cấu hình của dịch vụ 

`Timeout : Là khoảng thời gian trước khi nhận và gửi tính theo đơn vị giây

`KeepAlive` : Mặc định trong cùng một thời điểm 1 web browser chỉ gửi được 1 request. Nếu bật option này lên thì trong một thời điểm có thể gửi nhiều request đến server

`Listen :80` : Mặc định sẽ để cổng 80, có thể sửa nếu thích 

`ServerAdmin` : Là tài khoản email cho dịch vụ quản lý http 

`ServerName` : Là tên miền của website, có thể ghi bất kể tên miền nào mình muốn

`DocumentRoot`: Là thư mục chưa đường dẫn của website

`<Directory "/var/www/html">` : Chỉnh đến thư mục chứa website của mình

`DirectoryIndex index.html index.html.var` : Những website nào có trên thư mục website của chúng ta, option này sẽ được hoạt động từ trái sang phải. Đở đây cấu hình tên thư mục của web `trangchu.html` lên đầu

- Sau khi cấu hình xong thì lưu lại và khởi động lại dịch vụ httpd

`service httpd restart`

- Bước tiếp theo cho dịch vụ khởi động cùng hệ thống 

```
chkconfig --level 123456 httpd on
```

- Cấu hình rule của iptables sao cho máy client có thể truy cập vào web

```
iptables -t filter -A INPUT -s 192.168.220.0/24 -p tcp --dport 80 -j ACCEPT
```

- Từ máy window client từ bên ngoài truy cập đến địa chỉ của webserve `192.168.220.16`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/webserver/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/webserver/1.png)

## Trường hợp cấu hình tài khoản để đăng nhập vào web

- Bước đầu tiên tạo người dùng 

```
[root@ipmac ~]# useradd sv1
[root@ipmac ~]# useradd sv2
[root@ipmac ~]# useradd gv1
[root@ipmac ~]# useradd gv2

```

- Sau đó đặt mật khẩu cho người dùng. Để đặt mật khẩu của người dùng trên dịch vụ web thì phải sử dụng câu lệnh 

```
htpasswd -c /etc/httpd/conf/passwords sv1
```

- Câu lệnh trên có nghĩa là cấu hình mật khẩu web cho người dùng sv1 trong thư mục passwords

- Kiểm tra lại bằng câu lệnh sau:

```
[root@ipmac ~]# cat /etc/httpd/conf/passwords
sv1:KtMUL8mO91v/c
```
- Tạo mật khẩu cho các user khác sẽ không cần option -c vì thư mục password đã được tạo ra 

```
htpasswd  /etc/httpd/conf/passwords sv2
```
- Gom nhóm để phân quyền. Tạo một group

```
[root@ipmac ~]# vi /etc/httpd/conf/groups
```

- Cấu hình trong file đó:

```
[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/webserver/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/webserver/2.png)
```

- Chỉ cho phép tài khoản sinh viên được phép đăng nhập vào tài khoản 

- vào bên trong file cấu hình `vi /etc/httpd/conf/httpd.conf`. Sau đó xóa từ dòng 318 đến dòng 344

```
:318,344d
```
Sau đó sửa file đó với nội dung sau:

```
 <Directory "/var/www/html/website">
         Order allow,deny
         Allow from 192.168.220.16/24
         AuthType Basic
         AuthName "ate.vn index"
         AuthUserFile /etc/httpd/conf/passwords
         AuthGroupFile /etc/httpd/conf/groups
         Require group sinhvien
  </Directory>
```

- Kiểm tra kết quả bằng cách truy cập theo địa chỉ ở bên ngoài bằng máy client

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/webserver/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/webserver/3.png)

- Phải gõ đúng tài khoản của nhóm sinh viên mới đăng nhập được vào 

## Trường hợp một doanh nghiệp chỉ cho 1 server làm webserver nhưng lại muốn tạo lên nhiều website. Chúng ta sử dụng vitural host để nhân bản lên nhiều webserver. Nhiều tên miền nhưng đều trỏ về một địa chỉ 

- Bước đầu tiên tạo một thư mục để chứa website virtural host 

```
mkdir /var/www/html/web2 
```
- Tạo một virtural host có tên là index.html

```
touch /var/www/html/web2/index.html
```

- Vào file cấu hình `/etc/httpd/conf/httpd.conf` kéo xuống file dưới cùng copy thư mục virtual mẫu để cấu hình

- Kéo lên trên một chút sửa file `NameVirtualHost 192.168.220.16:80` để  trỏ virtual đến địa chỉ 192.168.220.16

- Cấu hình trang ate.vn ở trên xuống virtual host để sau đỡ trùng địa chỉ 

```
NameVirtualHost x.x.x.x:80
<VirtualHost  x.x.x.x:80>
        ServerAdmin webmaster@abc.com
        DocumentRoot /var/www/html/website
        ServerName ate.vn
```


 

















