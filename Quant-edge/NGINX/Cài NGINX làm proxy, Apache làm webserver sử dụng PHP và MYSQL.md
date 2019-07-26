
##**Làm việc tại Quantedge**

##**Tìm hiểu Nginx**

###**Hướng dẫn cài đặt web server dùng Nginx**

Máy chủ Web(Web Server) là máy tính mà trên đó cài đặt phần mềm phục vụ web, đôi khi người ta cũng gọi chính phần mềm đó là web server. Tất 

cả các web server đều hiểu và chạy được các file *.htm và *.html. Tuy nhiên mỗi web service lại phục vụ một số kiểu file chuyên biệt chẳng 

hạn như IIS của Microsoft dành cho *.asp, *.aspx; Apache, Nginx dành cho *.php...; 

##**Mô hình lab**

##**Cài đặt NGINX, APACHE, PHP7, MARIADB(MYSQL), SAMBA làm môi trường lập trình web**

**Bước 1: Cài các gói epel**

```
 yum install epel-release
```

 **Bước 2: Cài NGINX**

```
yum install nginx
```

**Bước 3: Mở dịch vụ NGINX**

```
systemctl enable nginx
```

**Bước 4: Sửa file SELINUX**

Vào trong thư mục ở bên trong đường dẫn sau ` vi /etc/selinux/config` để disable SELINUX

```
 edit SELINUX=enforcing --- SELINUX=disabled

```

**Bước 5: Dừng và tắt hệ thống tường lửa**

```
systemctl stop firewalld.service

systemctl disable firewalld.service
```

**Bước 6: Sửa file cấu hình của NGINX**

Vào sửa file trên đường dẫn `vi /etc/nginx/nginx.conf` rồi xóa file từ dòng file config từ server sau đó copy toàn bộ mục này

```
 server {
  listen       80 default_server;
  listen       [::]:80 default_server;
  server_name  _;
  root         /var/www/html;
  index index.php index.html index.htm;

  # proxy settings
  proxy_redirect     off;

  # Load configuration files for the default server block.
  include /etc/nginx/default.d/*.conf;

  location / {
   try_files $uri $uri/ /index.php;
  }

  location ~ \.php$ {

   proxy_set_header X-Real-IP  $remote_addr;
   proxy_set_header X-Forwarded-For $remote_addr;
   proxy_set_header Host $host;
   proxy_pass http://127.0.0.1:8888;

  }

  error_page 404 /404.html;
      location = /40x.html {
  }

  error_page 500 502 503 504 /50x.html;
      location = /50x.html {
  }
     }
```

**Bước 7: Cài đặt Apache**

```
yum install httpd
```

Sửa port APACHE để tránh đụng port với NGINX

```
 vi /etc/httpd/conf/httpd.conf 

tìm Listen 80 == Listen 8888
```

Sau đó reboot lại server

**Bước 8: Khởi động và bật service httpd**

```
 systemctl start httpd.service

 systemctl enable httpd.service
```

**Bước 9: Tắt firewalld**

```
systemctl stop firewalld.service

systemctl disable firewalld.service
```

**Bước 10: Tạo 1 file index.htm trong thư mục /var/www/html chứa noi dung hello**

**Bước 11: Vào web**

Vào web bằng cách gõ địa chỉ đường dẫn như sau `dải ip/index.htm`

**Bước 12: Cài đặt MariaDB**

```
 yum install mariadb-server mariadb

 khởi động dịch vụ lên

 systemctl start mariadb

 mysql_secure_installation  == đặt mật khẩu cho MariaDB

 systemctl enable mariadb.service

 ```

 **Bước 13: Cài đặt PHP version 7.1.7**

 ```
  yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

  vi /etc/yum.repos.d/remi-php71.repo edit enabled=1

  yum -y install php php-mbstring php-gettext php-mysqli php-pecl-zip

  systemctl restart httpd.service
 ```

Download PHPMyAdmin tool quan lý MySQL database 

Cài đặt PHP Version 7.1.7
     + yum -y install http://rpms.famillecollet.com/enterpr...
       vi /etc/yum.repos.d/remi-php71.repo edit enabled=1
     + yum -y install php php-mbstring php-gettext php-mysqli php-pecl-zip
     + systemctl restart httpd.service

  ===================================================
Cài tool wget:
   - yum install wget

   - Download PHPMyAdmin tool quan lý MySQL database https://www.phpmyadmin.net/downloads/
     cd /var/www/html
     wget https://files.phpmyadmin.net/phpMyAdm...

     Giải nén và đổi tên:
     tar -xzvf phpMyAdmin-4.7.3-english.tar.gz     
     mv phpMyAdmin-4.7.3-english phpmyadmin
     chown -Rf apache:apache phpmyadmin
     cd phpmyadmin
     cp config.sample.inc.php config.inc.php
     vi config.inc.php tìm AllowNoPassword = false; chuyển thành true
     
     Ra trình duyet chay lai: http://your_server_IP_address/phpmyadmin là ok






