## **nuttcp command**

Nuttcp là công cụ đo lượng hiệu năng mạng và cả thệ thống. Công việc cơ bản nhất của nó là xác định lưu lượng mạng TCP(UDP) ở network layer 

trong OSI Model bằng cách chuyển các buffer từ các địa chỉ nguồn tới hệ thống đích trong một khoảng thời gian nhất định hay timing một số 

byte được chỉ định. Ngoài việc báo cáo luồng dữ liệu trong các Mbps, nuttcp còn cung cấp các thông tin liên quan đến người dùng, system, mức 

độ sử dụng CPU, phần trăm mất mát dữ liệu. Hiện nay nuttcp đã hỗ trợ IPv6 . IPv4 ( bao gồm gói muticast ) . Nuttcp hoạt động trên hầu hết 

các distributions của Unix.

|**Option**|**Description**|
|--|--|
|-h| Liệt kê danh sách các option và description|
|-V| Hiển thị phiên bản nuttcp đang sử dụng|
|-t| Chỉ định host này là receiver|
|-S| Chỉ định host server|
|-b| Chỉ định output one-line, đây là kiểu output mặc định|
|-B| Chỉ hoạt động trên host-receiver, bắt buộc host đọc hết các bản buffer|
|-s| Sử dụng input thay vì memory bufer để làm dữ liệu transfer|
|-u| Sử dụng UPD protocol thay vì TCP|
|-v| Cung cấp thêm thông tin về dữ liệu transfer|
|-p| Port sử dụng thông qua quá trình kết nối, mặc định 5501|
|-P| Trong mode client/server, chỉ định cổng kiểm soát kết nối, mặc định cổng 5000|
|-N| Số luồng dành cho data transfer|
|-T| Giới hạn thời gian mà các host transfer gửi data đến host receiver|
|-R| Điều chỉnh tốc độ truyền data của host transmitter|
|-w| Điều chỉnh window site cho data transfer|
|-i| Thời gian nhận báo cáo(mặc định 1s)|
|-l| Packet length|

**Một số command**

Bắt đầu server với port 5003:

```
nuttcp -S -P 5003
```

**Transmitter Commands**

Chạy kiểm tra 10s, đưa kết quả mỗi giây

```
nuttcp -i 1 <server>
```

Kiểm tra yêu cầu dài hơn với option -T, bạn có thể chỉ rõ khoảng như :

```
-T30 = 30 sec, -T1m = 1 min, and -T1h = 1 hr
```

**Receiver Commands**

Chạy kiểm tra truyền nhận giữa client và server 

```
nuttcp -r -i 1 <server>
```

## **iperf**

Hướng dẫn sử dụng iperf

Iperf là một công cụ hữu hiệu giúp chúng ta tính toán băng thông của mạng 

**Cài đặt** 

Trên Ubuntu 

```
apt-get install iperf
```

Trên CentOS

```
yum install iperf
```

**Một số tham số phổ biến của iperf**

|**Tham số**|**Tác dụng**|
|--|--|
|-c|Chỉ ra địa chỉ IP của server để iperf kết nối đến|
|-f,--fomat|Chỉ ra định dạng của kết quả hiển thị. 'b'=bps, 'B'= Bps, 'k' = Kbps , 'K' =KBps,..|
|-i, --interval|Thời gian lấy mẫu để hiển thị kết quả|
|-p,--port|Định ra cổng để nghe, mặc định nếu không sử dụng tham số này là cổng 5001|
|-u,udp|Sử dụng giao thức udp, mặc định iperf sử dụng TCP|
|-P, --parallel	|Chỉ ra số kết nối song song được tạo, nếu là Server mode thì đây là giới hạn số kết nối mà server chấp nhận|
|-b|Định ra băng thông tối ta có thể truyền, chỉ sử dụng với UDP, client mode|
|-t|Tổng thời gian của kết nối, tính bằng giây|
|-M|Max segment size|
|-l|Buffer size|
|-w, --window|Trường Windows size của TCP|

**3. Thực hiện các bài test với IPerf**

Mô hình chung:

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/15.jpg)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/15.jpg)

Để kiểm tra băng thông của mạng ta có thể sử dụng một trong 2 giao thức TCP hoặc UDP, nhưng điểm chung giữa hai phương pháp này đều cần 1 

máy làm server để lắng nghe, một máy client kết nối đến giống như trong hình. IPerf sẽ tính toán và đưa ra được băng thông của mạng giữa 

Server và client.

**Sử dụng TCP** 

Cả máy server và client đều cần cài iperf. Nếu sử dụng tham số cổng (-p) thì trên cả server và client đều phải giống cổng nhau 

- Ví dụ một bài test đơn giản

Server

```
iperf -s
```

Client:

```
iperf -c ip-server
```

Sau 10s kết quả sẽ trả về màn hình 

- Ví dụ bài test TCP với Buffer size: 16 MB, Window Size: 60 Mbps, Max segment size 5 trong thời gian 5 phút, kết quả hiển thị dưới dạng

 mbps

Server:

```
iperf -s -P 0 -i 1 -p 5001 -w 60.0m -l 16.0M -f m
```

Client:

```
iperf -c ip-server -i 1 -p 5001 -w 60.0m -M 1.0K -l 16.0M -f m -t 300
```

**Sử dụng UDP**

- Ví dụ một bài test đơn giản

Server:

```
iperf -s -u
```

Client:

```
iperf -c ip-server -u
```

Sau 10 giây kết quả sẽ trả về trên màn hình.

- Ví dụ bài test UDP với Bandwidth 600 Mbps Packet size 500 Bytes trong 300s

Server:

```
iperf -s -u -P 0 -i 1 -p 5001 -f m
```

Client:

```
iperf -c ip-server -u -i 1 -p 5001 -l 500B -f m -b 600m -t 300
```

- Kiểm tra tốc độ của một cổng mạng

Để làm việc này ta có thể đẩy tải liên lục bằng UDP tại máy chủ, do UDP truyền file mà không cần phải bắt tay 3 bước như TCP nên ta có thể 

đẩy UDP liên lục từ client, thay đổi băng thông và quan sát băng thông tối đa mà nó đạt được, đó cũng chính là giới hạn của card mạng.

Giả sử có một máy chủ card eth0 có ip 10.10.10.10 và tôi muốn kiểm tra xem tốc độ eth0 tối đa là bao nhiêu, tôi thực hiện như sau:

```
iperf -c 10.10.10.1 -u -b 100m -t 100 -i 1
iperf -c 10.10.10.1 -u -b 500m -t 100 -i 1
iperf -c 10.10.10.1 -u -b 1g -t 100 -i 1
iperf -c 10.10.10.1 -u -b 2g -t 100 -i 1
```
Quan sát kết quả thu được, lấy giá trị băng thông cao nhất do tham số -b là giới hạn băng thông UDP, nên ta có thể tăng giới hạn này lên để 

xác định tốc độ thật của card.

- Kiểm tra tốc độ mạng 2 chiều 

Với tham số -d bạn có thể kiểm tra tốc độ mạng 2 chiều, sau khi kiểm tra tốc độ mạng trong client, server thì hai máy chủ sẽ đổi vai trò cho

nhau và thực hiện kiểm tra 2 lần. 

```
iperf -c 125.212.218.194 -d
```
 Với dải ip là bên máy bên kia. 

 ## **Tìm hiểu Bandwidth Test Controller (BWCTL)**

 **Mục lục**

 **1.bwctl là gì và để làm gì**

 BWCTL là một công cụ dòng lệnh sử dụng một loạt các công cụ đo lường network như iperf, iperf3, Nuttcp, Ping, Traceroute, Tracepath, và 

 OWAMP để đo băng thông TCP tối đa với một loạt các tùy chọn điều chỉnh khác nhau như sự trễ, tỷ lệ mất gói tin... Mặc định, bwctl sẽ dùng 

 iperf.

 bwctl client sẽ liên lạc với một máy chủ để thực hiện test. bwctl server sẽ quản lý và sắp xếp tài nguyên trên host mà nó chạy.

 **Các tính năng chính**

 - Hỗ trợ iperf, iperf3 và Nuttcp tests. 

 - Hỗ trợ ping tests

 - Hỗ trợ ipv6 mà không cần thêm tùy chọn nào 

 - Dữ liệu từ cả 2 phía được trả lại vì thế có thể so sánh kết quả giữa hai phía 

 - Không yêu cầu local BWCTL server, BWCTL client sẽ kiểm tra xem có local BWCTL server hay không và sử dụng nó nếu có.

 - Port ranges cho kết nối có thể được chỉ định. 

 - Giới hạn số lượng test có thể chạy.

 **Yêu cầu**

 - BWCTL server yêu cầu NTP được sử dụng để cả hai phía đều có cùng scheduled time window

 **2. Một số options phổ biến**

 |**Options**|**Descriptions**|
 |--|--|
 |-4, --ipv4|Chỉ dùng ipv4|
 |-6, --ipv6|Chỉ dùng ipv6|
 |-c, --receiver|Chỉ định host chạy Iperf, Iperf3 or Nuttcp server|
 |-s, --sender|Chỉ định host chạy Iperf, Iperf3 or Nuttcp client|
 |-T, --tool|Chỉ định tool sử dụng ( iperf, iperf3, nuttcp)|
 |-b, --bandwidth|Giới hạn bandwidth với UDP|
 |-l, --buffer_length|độ dài của read/write buffers (bytes). Mặc định 8 KB TCP, 1470 bytes UDP|
 |-t,--test_duration|Thời gian cho bài test, mặc định là 10 giây|
 |-u, --udp|Dùng UDP test, vì mặc định là dùng TCP|
 |-h, --help|Show help message|
 |-p, --print|	In kết quả ra file|
 |-V, --version|Phiên bản|
 |-P|Số luồng kết nối tới server|
 |-w|kích thước gói tin|
 |--tester_port	|port để test, mặc định được specific bởi công cụ sử dụng|	

 **3. Lab cài đặt và sử dụng bwctl trên CentOS 7**

 **Cài đặt**

 `yum install epel-release`

 2. Cài đặt RPM:

 `yum install http://software.internet2.edu/rpms/el7/x86_64/main/RPMS/Internet2-repo-0.7-1.noarch.rpm`

 3. Cài đặt:

 `yum install bwctl -y`

 4. Cài đặt NTP  `yum install -y ntp`

 5.Chỉnh sửa NTP Server trên cả các host vào file cấu hình `/etc/ntp.conf`. Thêm `server vn.pool.ntp.org iburst` để cả 2 cùng trỏ về một 

 server. 

 Khởi động lại dịch vụ ntp.

 `systemctl restart ntpd`

 Kiểm tra lại

 `ntpq -p`

 **Một số câu lệnh thông dụng**

Trong bwctl sử dụng các tool để làm bài test nên có thể nói là model client/server hoặc theo bwctl thì máy chạy lệnh sẽ là sender và máy 

còn lại sẽ là : receiver

`bwctl -c 192.168.220.20` Host gửi sẽ là sender, host còn lại là receiver

```
SENDER START
Connecting to host 192.168.36.139, port 5878
[ 15] local 192.168.36.140 port 46065 connected to 192.168.36.139 port 5878
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[ 15]   0.00-1.01   sec   344 MBytes  2872 Mbits/sec    0    795 KBytes       
[ 15]   1.01-2.00   sec   412 MBytes  3471 Mbits/sec    0   1012 KBytes       
[ 15]   2.00-3.00   sec   416 MBytes  3492 Mbits/sec    0   1.08 MBytes       
[ 15]   3.00-4.00   sec   408 MBytes  3426 Mbits/sec    0   1.18 MBytes       
[ 15]   4.00-5.00   sec   402 MBytes  3370 Mbits/sec    0   1.30 MBytes       
[ 15]   5.00-6.00   sec   422 MBytes  3544 Mbits/sec    0   1.34 MBytes       
[ 15]   6.00-7.00   sec   421 MBytes  3536 Mbits/sec    0   1.41 MBytes       
[ 15]   7.00-8.00   sec   429 MBytes  3594 Mbits/sec    0   1.49 MBytes       
[ 15]   8.00-9.00   sec   422 MBytes  3550 Mbits/sec    0   1.55 MBytes       
[ 15]   9.00-10.00  sec   430 MBytes  3606 Mbits/sec    0   1.67 MBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[ 15]   0.00-10.00  sec  4.01 GBytes  3446 Mbits/sec    0             sender
[ 15]   0.00-10.00  sec  4.01 GBytes  3446 Mbits/sec                  receiver

iperf Done.

SENDER END
```

`bwctl -s 192.168.36.139` Host gửi lệnh là reciver, còn host còn lại là sender

```
bwctl: Using tool: iperf3
bwctl: 17 seconds until test results available
```

```
SENDER START
Connecting to host 192.168.36.140, port 5868
[ 15] local 192.168.36.139 port 48013 connected to 192.168.36.140 port 5868
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[ 15]   0.00-1.00   sec   368 MBytes  3086 Mbits/sec    0    935 KBytes       
[ 15]   1.00-2.00   sec   432 MBytes  3622 Mbits/sec    0   1.08 MBytes       
[ 15]   2.00-3.00   sec   444 MBytes  3728 Mbits/sec    0   1.23 MBytes       
[ 15]   3.00-4.00   sec   445 MBytes  3733 Mbits/sec    0   1.33 MBytes       
[ 15]   4.00-5.00   sec   406 MBytes  3406 Mbits/sec    0   1.43 MBytes       
[ 15]   5.00-6.00   sec   450 MBytes  3776 Mbits/sec   48   1.06 MBytes       
[ 15]   6.00-7.00   sec   444 MBytes  3724 Mbits/sec    0   1.16 MBytes       
[ 15]   7.00-8.00   sec   460 MBytes  3858 Mbits/sec    0   1.28 MBytes       
[ 15]   8.00-9.00   sec   431 MBytes  3610 Mbits/sec    0   1.31 MBytes       
[ 15]   9.00-10.00  sec   446 MBytes  3746 Mbits/sec    0   1.37 MBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[ 15]   0.00-10.00  sec  4.23 GBytes  3629 Mbits/sec   48             sender
[ 15]   0.00-10.00  sec  4.23 GBytes  3629 Mbits/sec                  receiver

iperf Done.
```

`bwctl -x -c somehost.example.com -s otherhost.example.com`

Sender từ một host khác, không phải từ local

- Ngoài bwctl còn có một số command đi kèm :

```
bwping -h 
bwtraceroute -h
```












