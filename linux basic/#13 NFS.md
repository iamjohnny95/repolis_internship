# **Network Filesystem**

- NFS(the Network File System) là một giao thức được dùng cho việc chia sẻ file qua physical systems. Người quản trị gắn các thư mục của người dùng từ xa trên một máy chủ để cho phép họ truy cập vào cùng một tệp và cấu hình. Hoạt động theo cơ chế client-server
Hiện tại NFS có 4 phiên bản. NFSv4 là phiên bản đang được sử dụng nhiều nhất và hỗ trợ phát huy tối đa của giao thức NFS

Một số vấn đề với NFS

   - Không bảo mật, mã hóa dữ liệu
   - Hiệu suất hoạt động trung bình ở mức khá, nhưng không ổn định
   - Dữ liệu phân tán có thể bị phá vỡ nếu có nhiều phiên sử dụng đồng thời

File `etc/export` chứa các đường dẫn thư mục và quyền hạn mà một host muốn chia sẻ dữ liệu với host khác qua NSF.

Các máy chủ có quyền hạn sau:

    - `rw`: Đọc và ghi 
    - `ro`: Chỉ được đọc
    - `noacess`: Cấm truy cập vào các thư mục con của thư mục đc chia sẻ

 Ví dụ bạn muốn chia sẻ thư mục `/share` cho các máy có địa chỉ trong 192.168.1.1/28 có quyền đọc ghi thì thêm vào nội dung file dòng sau:

 ```
 /Share 192.168.1.1/28(rw)
 ```
 # **Cài NFS trên CentOS 7**

 ## Requirements

 Server:
 ```
 CentOS 7
 ip: 192.168.220.13
 ```
 Client:
 ```
 CentOS 7
 ip: 192.168.220.14
 ```

 **Installation**

- Cài đặt NFS trên server:

```
yum install nfs-utils
```

- Trên máy chủ, tôi sẽ tạo một thư mục để chia sẻ các tệp tin 

```
mkdir /nfs
```

- Thay đổi quyền cho tệp tin tránh việc người dùng sửa đổi tệp tin và thay đôi quyền sở hữu tệp tin thành không sở hưu bởi ai cả: 

```
chmod -R 755 /nfs
chown nobody:nobody /nfs
```
- Khởi động dịch vụ 
```
systemctl enable rpcbind 
 systemctl enable nfs-server
 systemctl enable nfs-lock
 systemctl enable nfs-idmap
 systemctl restart rpcbind
 systemctl restart nfs-server
 systemctl restart nfs-lock
 systemctl restart nfs-idmap
```

- Cấu hình cho phép client truy cập 
```
vi /etc/exports
/nfs 192.168.220.0/24(rw,sync,no-root_squash,no_all_squash)
```

- Cấu hình firewall
```
firewall-cmd --permanent --zone=publish --add-service=nfs
firewall-cmd --permanent --zone=publish --add-service=mountd
firewall-cmd --permanent --zone=publish --add-service=rpc-bind 
firewall-cmd --reload
```
- Trên NFS Client (CentOS 7)
- Cài đặt 
```
yum install nfs utils
```

- Tiếp theo đó tạo thư mục để truyền dữ liệu đến 
```
mkdir /root/son
```
 - Kết nối 
 ```
 mount -t nfs 192.168.220.13:/nfs /son
 ```
 - Cấu hình tự động kết nối khi mở máy 
 ```
 vi /etc/fstab
 ```
 192.168.220.13:/nfs    /son   deafaults   0  0
```

