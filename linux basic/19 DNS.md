## **DNS**

## **Khái niệm DNS**

- DNS là hệ thống phân giải tên miền Domain Name Server (hay gọi là DNS) là một giao thức mạng internet. 

## **Các kiểu tên miền**

Một tên miền được chia làm nhiều cấp bậc:

- gTLD (Generic Top Level Domain) – tên miền kết thúc bằng .com, .net, .org, .gov, .edu và .name.

- ccTLD (Country Code Top Level Domain) – tên miền riêng của mỗi quốc gia (ví dụ .il, .ru, .uk, ,us, .cn, .vn).

- Infrastructure TLD – Xử lý và điều hướng chuyển đổi từ địa chỉ IP sang tên miền, Ví dụ IPv4 48.199.81.in-addr.arpa. Sử dụng trong bản ghi PTR (được giải thích bên dưới).

- Cấp 2ld, 3ld, 4ld – Ví dụ www.somedomain.co.uk, uk là ccTLD, co là 2ld, somedomain là 3ld và www là 4ld.

Các bản ghi DNS được phân loại như sau:

- A

Bản ghi A xác định địa chỉ IPV4 hoặc IPV6. Ví dụ bản ghi:

www      IN        A         12.34.56.78

trong tên miền somedomain.co.uk định nghĩa www.somedomain.co.uk được truy cập duy nhất tại địa chỉ IPv4 12.34.56.78.
 
- CNAME

Bản ghi CNAME xác định một định danh khác hay gọi là bí danh (alias) sẽ được phân giải đến khi tìm thấy bản ghi A. Ví dụ bản ghi:

www      IN        CNAME          www.somedomain.co.uk

Trong tên miền somedomain.com định nghĩa định danh duy nhất www.somedomain.com là bí danh cho www.somedomain.co.uk.

- MX

Bản ghi MX (mail exchange) xác định tên tài nguyên và danh sách máy chủ mail theo thứ tự ưu tiên cho tên miền đó. Ví dụ bản ghi:

somedomain.co.uk     IN        MX      10       mailsrv1

somedomain.co.uk     IN        MX      20       mailsrv2

Xác định mailsrv1.somedomain.co.uk là máy chủ mail được ưu tiên gửi đến đầu tiên và tiếp sau đó là mailsrv2.somedomain.co.uk.

- NS

Bản ghi NS (name server) xác định authoritative name server của domain. Ví dụ bản ghi:

somedomain.co.uk     IN        NS       ns1.somedomain.co.uk

somedomain.co.uk     IN        NS       ns2.somedomain.co.uk

- PTR

Bản ghi PTR (pointer) trỏ một địa chỉ IP đến một bản ghi A trong chế độ ngược (reverse)  và được sử dụng trong kiểu tên miền infrastructure

 TLD.

- TTL

TTL là thời gian cache của bản ghi DNS trên một máy chủ tên miền trước khi máy chủ đó tìm kiếm một phiên bản cập nhật


## Bản ghi SOA – Start of Authority là gì

Thông thường, mỗi tên miền sẽ sử dụng 1 cặp DNS nào đó để trỏ về 1 hoặc nhiều máy chủ DNS, và ở đây, các máy chủ DNS có trách nhiệm cung cấp 

thông tin bản ghi DNS của hệ thống cho tên miền này để nó hoạt động. SOA được coi như dấu hiệu nhận biết của hệ thống về tên miền này.

- Một cấu trúc của bản ghi SOA thông thường sẽ bao gồm:

```
@ IN SOA dns.abc.local. root.abc.local. (
2011071001 ; dns update time for new zone (yyyy-mm-dd-hh-mm)
3600 ; Refresh to new update
1800 ; Retry time for error
604800 ; Expire Time after remove record from system
86400 ;Minimum TTL
```
Trong đó:

- dns.abc.local: Giá trị DNS chính của tên miền hoặc máy chủ 

- root.abc.local: Tên account admin của tên miền này 

- 2011071001: Thời gian cập nhật dns cho tên miền mới nhất 

- 3600: Số giây bản tin tự động cập nhật mới 

- 1800: Thời gian trước khi bị lỗi không thể tự động cập nhật lại và cần lấy lại thông tin DNS ở lần tiếp theo.

- 604800: Giới hạn thời gian tính bằng giây sau khi gỡ bỏ bản ghi trên serve và không còn hiệu lực trên server

- 86400: TTL xác định thời gian cache của bản ghi


## Cấu hình DNS:

- Cài đặt DNS:

```
#yum install bind bind-utils -y
```

- Cấu hình 

- Tạo file thuận bên trong file `named.conf`

```
#vi /etc/named.conf

listen-on port 53 { 127.0.0.1; 192.168.1.100; }; ### Địa chỉ ip master dns ###

zone"abc.local" IN {
type master;
file "abc.zone";
allow-update { none; };
};
```

- Tạo file nghịch bên trong file `named.conf`


zone"1.168.192.in-addr.arpa" IN {
type master;
file "1.168.192.zone";
allow-update { none; };
};

- Tạo file zone:


- Tạo một file zone thuận như đã cài đặt ở trên,trong thư mục `var/named/abc.zone`

```
@ IN SOA dns.abc.local. root.abc.local. (
2011071001 ; dns update time for new zone (yyyy-mm-dd-hh-mm)
3600 ; Refresh to new update
1800 ; Retry time for error
604800 ; Expire Time after remove record from system
86400 ;Minimum TTL

)
@ IN NS dns.abc.local.
@ IN MX 1 mail. abc.local.
dns IN A 192.168.1.100
www IN A 192.168.1.100
mail IN A 192.168.1.101
```

- Tạo một file zone nghịch như đã cài đặt ở trên, trong thư mục `/var/named/1.168.192.zone`

```
@ IN SOA dns.abc.local. root.abc.local. (

2011071001 ;Serial

3600 ;Refresh

1800 ;Retry

604800 ;Expire

86400 ;Minimum TTL

)

@ IN NS dns.abc.local.

100 IN PTR dns.abc.local.

101 IN PTR www.abc.local.

102 IN PTR mail.abc.local.

```











