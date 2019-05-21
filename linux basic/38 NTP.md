## **Cấu hình NTP**

NTP (Network Time Protocol) là một giao thức dùng để đồng bộ hóa thời gian giữa các máy chủ với nhau, đặc biệt là hệ thống tài chính, dịch vụ

, khoa học... thì nhu cầu này đặc biệt quan trọng.

## **Mô hình**

Giao thức NTP phân chia các time server ra thành nhiều lớp (statum), số stratum càng nhỏ thì thời gian càng chính xác (stratum nhỏ nhất là 0)

. Các server có stratum bằng 0 sẽ cung cấp thời gia chuẩn cho các client có stratum là 1, các client không thể truy cập vượt cấp stratum của 

mình (stratum 4 chỉ có thể truy cập stratum 3 chứ không thể lấy thời gian từ stratum 2)

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/NTP/1.jpg)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/NTP/1.jpg)

NTP hoạt động bằng cách đo thời gian RTT (round trip time) của các gói tin trao đổi giữa các client và server. Client trên máy tính để đồng 

bộ thời gian với server. Thời gian điều chỉnh sẽ dựa trên hai thông số là timestamp là thời gian di chuyển của gói tin. 

Chính vì vậy, ta nên chọn time server có độ delay thấp nhất

Quy trình cơ bản khi cấu hình NTP server là:

1. NTP Server A lấy giờ chuẩn từ 1 server khác có level stratum cao hơn 

2. Các NTP Client khác sẽ lấy giờ từ NTP Server chuẩn này.


## **Cấu hình**

**NTP Server**

Để cấu hình và cài đặt NTP Server (gói ntpd) trên CentOS 7, ta thực hiện các bước sau:

Cài đặt và cấu hình NTP server, cho phép các server trong subnet 10.0.0.0/24 truy cập tới NTP server

```
yum –y install ntp
 
vi /etc/ntp.conf
 
[…]
#Thêm dòng sau bên trong thư mục /etc/ntp.conf
 
restrict 10.0.0.0 mask 255.255.255.0 nomodify notrap
 
server vn.pool.ntp.org iburst
```
start service và enable tính năng auto start cho ntpd

```
systemctl start ntpd
 
systemctl enable ntpd
```

Kiểm tra NTP Server đã lấy được giờ chuẩn hay chưa

```
ntpq -p
```
[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/NTP/2.jpg)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/NTP/2.jpg)

NTP server đang lấy giờ từ một server chuẩn 128.9.176.30

## **NTP Client**

Đối với các client Linux lấy giờ từ NTP Server, ta có 2 cách

1. Cài đặt NTP service deamon tương tự như trên, nhưng lấy thời gian từ NTP Server mà ta chỉ định (ví dụ ở đây là 10.0.0.4)

2. Dùng ntpdate và set crontab sys time mỗi 5 phút. 

**Cách 1**

Cài đặt NTP service deamon tương tự như trên server, nhưng ta sẽ trỏ về địa chỉ IP/domain của server và không nhận request đồng bộ thời gian

từ các máy client khác.

```
yum –y install ntp
 
vi /etc/ntp.conf
 
[…]
 
#server<strong> <IP_of_your_server></strong> iburst
server<strong> 10.0.0.4</strong> iburst
 
restrict default ignore
```

Start service và enable tính năng auto start cho ntpd

```
systemctl start ntpd

systemctl enable ntpd
```

Kiểm tra NTP Client đã lấy được giờ chuẩn chưa 

```
ntpq -p 
```

**Cách 2**

Dùng lệnh ntpdate để đồng bộ thời gian + set crontab cho lệnh này check thời gian theo giờ.

Đầu tiên, tiến hành cài đặt ntpdate:

```
yum –y install ntpdate
```

Cấu hình ntpdate update thời gian từ Vietnam NTP Server pool 

```
ntpdate vn.pool.ntp.org
```
Hoặc chỉ định một IP

```
ntpdate <IP_of_your_server>
```
Enable tính năng auto start cho ntpupdate

```
systemctl enable ntpdate
```
Cấu hình sync tự động trong crontab mỗi 5 phút 

```
*/5 * * * * /usr/sbin/ntpdate 10.0.0.4 2>&1 | tee -a /var/log/ntpdate.log
```


