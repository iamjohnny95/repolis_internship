##**Tìm hiểu Nginx**

##**Cài đặt NGINX**

Tạo file repo:

```
cd /etc/yum.repos.d/
```

Tạo file repo cho Nginx

```
cat >> nginx.repo << "EOF"
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
EOF
```

Cài đặt bằng lệnh:

```
yum install nginx 
```

Vào file cấu hình nginx.conf trong đường dẫn `/etc/nginx/nginx.conf`

trỏ đường dẫn include vào đường dẫn cấu hình file .conf

Vào file cấu hình .conf trong đường dẫn `/etc/nginx/conf.d`

Đặt tên file xxx.conf cp file cấu hình này vào 

```

server {
       listen         80;
       server_name    test.quant-edge.com;
#       return         301 https://$server_name$request_uri;
}
server {
        listen 443 ssl;
        server_name test.quant-edge.com;
       #ssl on;
        ssl_protocols TLSv1.2 TLSv1.1 TLSv1;
        ssl_certificate /etc/test/ssl/fullchain1.pem;
        ssl_certificate_key /etc/test/ssl/privkey1.pem;
        ssl_ciphers AES256+EECDH:AES256+EDH:!aNULL;

  location / {

 root   /var/www/html;
        index  index.html index.htm;
 }

      #  location / {
      #     proxy_pass http://localhost:8006;
      #      proxy_http_version 1.1;
      #      proxy_redirect off;
      #      proxy_set_header Upgrade $http_upgrade;
      #      proxy_set_header Connection "Upgrade";
      #      #proxy_set_header Host $http_host;
      #      proxy_set_header X-Real-IP $remote_addr;
      #      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      #      proxy_set_header Host $host;
       # }

}
```
 **Note**:

```
 root   /var/www/html;
        index  index.html index.htm;
```

file cấu hình web local

```

      #  location / {
      #     proxy_pass http://localhost:8006;
      #      proxy_http_version 1.1;
      #      proxy_redirect off;
      #      proxy_set_header Upgrade $http_upgrade;
      #      proxy_set_header Connection "Upgrade";
      #      #proxy_set_header Host $http_host;
      #      proxy_set_header X-Real-IP $remote_addr;
      #      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      #      proxy_set_header Host $host;
      # }
```

Sử dụng cú pháp này khi trỏ sang webserver khác 

```
#ssl on;
        ssl_protocols TLSv1.2 TLSv1.1 TLSv1;
        ssl_certificate /etc/test/ssl/fullchain1.pem;
        ssl_certificate_key /etc/test/ssl/privkey1.pem;
        ssl_ciphers AES256+EECDH:AES256+EDH:!aNULL;
```

File cấu hình này chứa file chứng chỉ SSL của webserver. Đường dẫn đến file cấu hình /etc/test/ssl/

Tạo file index.html trong file /var/www/html

```
chmod 755 /var/www/html
chown -R root:root /var/www/html
```

Ở ngoài cấu hình window ở trong đường dẫn `C:\Windows\System32\drivers\etc` vào trong thư mục host để sửa file cấu hình 

