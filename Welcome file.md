﻿# Cài đặt và cấu hình Keystone
# 1. Openstack Indentity Overview
-  Openstack indentity cung cấp một điểm tích hợp để xác thực, phân quyền hoặc và danh mục dịch vụ. Openstack indentity service tường là dịch vụ đầu tiên mà người dùng tương tác đến. Mỗi khi đã xác thực, các end-user có thể sử dụng indentify token để truy cập vào các Openstack Service khác. . Tương tụ như vậy các - - Openstack service khác sử dung các indentity khác để chắc chắn rằng người dùng và quyền của người dùng đó. Indentifty serivce có thể tích hợp vào các management system khác như ( LAPD )
-  Người dùng và dịch vụ trong openstack có thể nhận dạng các Services khác qua các catalog service mà được quản trị bởi Indentity service. Catalog nắm nhiệm vụ nắm dữ danh sách serive trong quá trình deployment. Mỗi service sẽ có nhiều endpoint , các endpoint sẽ nằm trong 3 dạng sau : public, ijnternal, admin. Trong môi trường production, các endpoint sẽ nằm trên các mạng riêng biệt để bản bảo bảo mật. Ví dụ . public API có thể được tiếp cận từ môi trường internet, khác hàng có thể sử dụng sản phẩn cloud qua API này. Admin API sử dụng cho các sysadmin để quản trị infractructure cloud. Internal API sẽ sử dụng để làm việc với các host được quản lý bởi các Openstack Service
-  Openstack Indentity cung cấp `region` để tăng khả năng mở rộng. Mặc định `RegionOne` được sử dụng làm Region đâu tiên
-  Mỗi Openstack Service cài lên cần có một endpoint trên indentity service
-  Trong Indentity gồm có 3 thành phần
      - Server : một server tập trung cung cấp chức năng xác thực và phân quyền sử dụng Restful API
      - Drivers : driver hoặc back-end được tích hợp vào server dùng để truy cập vào DB indentity có thể là external service hoặc các dịch vụ internal ( SQL, LADP )
      - Modules : middleware module có thể chạy trên các Openstack compoment đang sử dụng indentity services. Những module này chặn các reques , xuất ra các credential sau đó gửi đến Server .

# 2. Cài đặt Openstack Queens trên Controller
- Triển khai trên mô hình
- Cài đặt Openstack Queens và Openstack Client
`yum install centos-release-openstack-queens -y
  yum upgrade
  yum install python-openstackclient -y`
  - Mặc định trên Centos và RHEL đã bật `SElinux` , cài đặt `openstack-selinux` để apply các policies cho các Openstack Service 
  ` yum install openstack-selinux -y`
  - Disable SeLinux `/etc/selinux/config` Sau do reboot server
  ` This file controls the state of SELinux on the system.
   # SELINUX= can take one of these three values: 
   # enforcing - SELinux security policy is enforced. 
   # permissive - SELinux prints warnings instead of enforcing.
   # disabled - No SELinux policy is loaded. SELINUX=disabled 
   # SELINUXTYPE= can take one of these two values: 
   # targeted - Targeted processes are protected, 
   # mls - Multi Level Security protection. SELINUXTYPE=targeted`

- Cấu hình hostname resolution
` echo "
 192.168.69.130 controller
  192.168.69.131 compute1
   192.168.69.132 compute2
    " >> /etc/hosts`
# 3. Cài đặt Openstack Indentity - Keystone
Trong loạt bài này sẽ cài đặt Keystone trên Controller Node . Để phục vụ cho khả năng mở rộng, Fernet tokens và Apache HTTP Server sử được sử dụng
## 3.1 . Chuẩn bị
- Trên hầu hết các Openstack Service đểu sử dụng SQL database để lưu thông tin. Cơ sở dữ liệu thường được chạy trên Controller Node. Trên loạt tìm hiểu này sẽ sử dụng `Mysql` và `MarriaDB` .
- Cài đặt MarriaDB
` yum install mariadb mariadb-server python2-PyMySQL -y`
- Cấu hình MarriaDB Server

`echo  "[mysqld]  
 bind-address = 192.168.69.130 
 default-storage-engine =
  innodb  innodb_file_per_table = on  
  max_connections = 4096  
  collation-server = utf8_general_ci 
  character-set-server = utf8"  >> /etc/my.cnf.d/openstack.cnf`

Trong đó : bind-address : IP của network interface management

- Start MarriaDB và cho phép enable trong boot
` systemctl enable mariadb.service
 systemctl start mariadb.service`
 - Cấu hình tài khoản root cho các Database
 ` /usr/bin/mysqladmin -u root -h localhost password 123@123Aa`

# 3.2 . Cài đặt, cấu hình Keystone
# 3.2.1. Cài đặt, cấu hình các thành phần
- Trước khi cài đặt Keystone, cần khởi tạo một DB riêng cho Keystone với tài khoản `root`
``` sh
mysql -u root --password=123@123Aa -e "CREATE DATABASE keystone"; mysql -u root --password=123@123Aa -e "GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' \  IDENTIFIED BY 'keystone_123';GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' \  IDENTIFIED BY 'keystone_123';"
```
- Cài đặt Openstack_keystone, httpd, mod_wsgi và cấu hình ban dầu
``` sh
yum install openstack-keystone httpd mod_wsgi crudini crudini --set /etc/keystone/keystone.conf "database"  "connection"  "mysql+pymysql://keystone:keystone_123@controller/keystone" crudini --set /etc/keystone/keystone.conf "token"  "provider"  "fernet" su -s /bin/sh -c "keystone-manage db_sync" keystone
```
- Khởi tạo kho lưu trữ `Fernet Token`
``` sh 
keystone-manage fernet_setup --keystone-user keystone --keystone-group keystone keystone-manage credential_setup --keystone-user keystone --keystone-group keystone
```
- Khởi động các dịch vụ trong Openstack Indentity
``sh 
keystone-manage bootstrap --bootstrap-password keystone_123 \ --bootstrap-admin-url http://controller:5000/v3/ \ --bootstrap-internal-url http://controller:5000/v3/ \ --bootstrap-public-url http://controller:5000/v3/ \ --bootstrap-region-id RegionOne
``

## 3.2.2. Cài đặt, cấu hình Apace HTTP Server
- Cấu hình Apache Conf và enable service
`ln -s /usr/share/keystone/wsgi-keystone.conf /etc/httpd/conf.d/
 systemctl enable httpd.service
  systemctl start httpd.service
``
## 3.2.3 . Set biến môi trường cho tài khoản admin

![chèn link] (https://camo.githubusercontent.com/3760df997da332e149329bb19ed079a0990edcc7/68747470733a2f2f692e696d6775722e636f6d2f456f4444384c562e706e67)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1ODAxMDI2NF19
-->