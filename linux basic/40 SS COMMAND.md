## **SS Command**

Lệnh `ss` trong linxu có khả năng cung cấp thông tin về `network/socket` kết nối tới máy chủ linux với ưu điểm đơn giản hơn và nhanh hơn 

nhiều so với công cụ truyền thống `netstat` 

Lý do `ss` nhanh hơn `nestat` là do `netstat` phải đọc thông tin files trong thư mục `/proc` để thu thập dữ liệu hiển thị, sẽ rất mất thời 

gian nếu dùng `netstat` trên một hệ thống có quá nhiều kết nối tới, còn `ss` sẽ lấy dữ liệu trực tiếp từ `kernel space` nên nhanh hơn rất 

nhiều. Sau đây là các câu lệnh `ss` trên linux.

**1. List Established Connections**

Theo mặc định, nếu chúng ta chạy lệnh `ss` mà không có tùy chọn nào khác, nó sẽ hiển thị một danh sách các non-listening sockets đã thiết 

lập kết nối, ví dụ như cổng tcp,udp hoặc unix

```
[root@centos7 ~]# ss | head -n 5

Netid  State      Recv-Q Send-Q Local Address:Port      Peer Address:Port

u_str  ESTAB      0      0       * 23740                * 23739

u_str  ESTAB      0      0       * 23707                * 23706

u_str  ESTAB      0      0       * 87021                * 88383

u_str  ESTAB      0      0       * 17056                * 17112
```

Trong ví dụ trên, đầu ra giới hạn có hơn 500 dòng được in bằng cách chạy lệnh ss, vì vậy bạn có thể muốn piple nó vào gì đó như để đọc dễ hơn

, hoặc bổ sung các tùy chọn vào phần cuối chỉ hiển thị những gì bạn theo dõi.

**2. Show Listening Sockets**

Thay vì liệt kê tất cả các sockets, có thể sử dụng tùy chọn -l để liệt kê cụ thể các socket đang lắng nghe kết nối.

```
[root@centos7 ~]# ss -lt
State       Recv-Q Send-Q  Local Address:Port                Peer Address:Port
LISTEN      0      2                   *:kerberos-adm        *:*
LISTEN      0      128                 *:sunrpc              *:*
LISTEN      0      5                   *:kpasswd             *:*
LISTEN      0      10       192.168.1.14:domain              *:*
LISTEN      0      10          127.0.0.1:domain              *:*
LISTEN      0      5       192.168.122.1:domain              *:*
LISTEN      0      128                 *:ssh                 *:*
```

Trong ví dụ này đã sử dụng tùy chọn -t để liệt kê TCP. Trong các ví dụ sau này, bạn sẽ thấy kết hợp nhiều tùy chọn -t để liệt kê TCP. Trong 

các ví dụ sau này, bạn sẽ thấy sự kết hợp nhiều tùy chọn như thế này để nhanh chóng lọc xuống những gì đang theo dõi. 

**3. Show Process**

Chúng ta có thể in ra quá trình hoặc số PID sở hữu một socket với tùy chọn -p 

```
[root@centos7 ~]# ss -pl
Netid  State      Recv-Q Send-Q Local Address:Port     Peer Address:Port
tcp    LISTEN     0      128    :::http                :::*    
```

Trong ví dụ trên chỉ liệt kê một kết quả duy nhất, không có thêm bất kỳ tùy chọn nào thì toàn bộ kết xuất trong ss in ra trên 500 dòng tới 

stdout. Dù vậy, ta có thể thấy process ID của các chương trình Apache khác nhau chạy trên server này.

**4. Không xử lý service name**

Theo mặc định ss sẽ chỉ giải quyết số cổng -port number như chúng ta đã thấy trước đây, ví dụ trong dòng dưới đây chúng ta có thể thấy 

192.168.1.14:ssh trong đó ssh được liệt kê là cổng cục bộ.

```
[root@centos7 ~]# ss
Netid  State      Recv-Q Send-Q Local Address:Port    Peer Address:Port
tcp    ESTAB      0      64     192.168.1.14:ssh      192.168.1.191:57091
```
Tuy nhiên, nếu chỉ định tùy chọn -n, độ phân giải này sẽ không xảy ra và thay vào đó ta sẽ thấy số cổng thay vì tên dịch vụ

```
[root@centos7 ~]# ss -n
Netid  State      Recv-Q Send-Q Local Address:Port    Peer Address:Port
tcp    ESTAB      0      0      192.168.1.14:22       192.168.1.191:57091
```

**5.Xử lý số địa chỉ / cổng**

Với tùy chọn `r` ta có thể thấy hostname của máy chủ 192.168.1.14 được liệt kê.

```
[root@centos7 ~]# ss -r
Netid  State      Recv-Q Send-Q Local Address:Port         Peer Address:Port
tcp    ESTAB      0      64     centos7.example.com:ssh    192.168.1.191:57091
```

**6. IPV4 Socket**

Ta có thể sử dụng tùy chọn -4 để hiển thị thông tin tương ứng với các IPv4 socket. Trong ví dụ dưới đây,cũng sử dụng tùy chọn -l  để liệt

kê tất cả listen trên địa chỉ IPv4

```
[root@centos7 ~]# ss -l4
Netid  State      Recv-Q Send-Q     Local Address:Port        Peer Address:Port
udp    UNCONN     0      0              127.0.0.1:323         *:*
udp    UNCONN     0      0          192.168.122.1:domain      *:*
udp    UNCONN     0      0               *%virbr0:bootps      *:*
udp    UNCONN     0      0                      *:bootpc      *:*
tcp    LISTEN     0      128                    *:sunrpc      *:*
tcp    LISTEN     0      5          192.168.122.1:domain      *:*
tcp    LISTEN     0      128                    *:ssh         *:*
tcp    LISTEN     0      128            127.0.0.1:ipp         *:*
tcp    LISTEN     0      100            127.0.0.1:smtp        *:*
```

**7. IPv6 Socket**

Tương tự, chúng tôi có thể sử dụng tùy chọn -6 để hiển thị thông tin liên quan đến IPv6 socket. Trong ví dụ dưới đây, chúng ta cũng sử dụng

tùy chọn -1 để liệt kê tất cả các listen trên địa chỉ IPV6.

```
[root@centos7 ~]# ss -l6
Netid  State      Recv-Q Send-Q     Local Address:Port          Peer Address:Port
udp    UNCONN     0      0                     :::ipv6-icmp     :::*
udp    UNCONN     0      0                     :::22834         :::*
udp    UNCONN     0      0                    ::1:323           :::*
tcp    LISTEN     0      128                   :::sunrpc        :::*
tcp    LISTEN     0      128                   :::http          :::*
tcp    LISTEN     0      128                   :::ssh           :::*
tcp    LISTEN     0      128                  ::1:ipp           :::*
tcp    LISTEN     0      100                  ::1:smtp          :::*
```

**8. TCP only**

Tùy chọn -t có thể được sử dụng để hiển thị các cổng TCP. Khi kết hợp với -1 để in ra các listen socket, ta có thể thấy mọi thứ listen trên 

TCP. 

```
[root@centos7 ~]# ss -lt
State      Recv-Q Send-Q      Local Address:Port       Peer Address:Port
LISTEN     0      128                     *:sunrpc     *:*
LISTEN     0      5           192.168.122.1:domain     *:*
LISTEN     0      128                     *:ssh        *:*
LISTEN     0      128             127.0.0.1:ipp        *:*
LISTEN     0      100             127.0.0.1:smtp       *:*
LISTEN     0      128                    :::sunrpc    :::*
LISTEN     0      128                    :::http      :::*
LISTEN     0      128                    :::ssh       :::*
LISTEN     0      128                   ::1:ipp       :::*
LISTEN     0      100                   ::1:smtp      :::*
```

**9. UDP only**

Tùy chọn -u có thể được sử dụng để chỉ hiển thị các ổ cắm UDP. vì UDP là giao thức ít kết nối, chỉ cần chạy với tùy chọn -u sẽ không hiển 

thị đầu ra. Thay vào đó, chúng ta có thể kết hợp nó với tùy chọn -a hoặc -l để xem tất cả các listening UDP socket, như hiển thị bên dưới 

```
[root@centos7 ~]# ss -ul
State       Recv-Q Send-Q  Local Address:Port       Peer Address:Port
UNCONN      0      0                   *:mdns       *:*
UNCONN      0      0                   *:kpasswd    *:*
UNCONN      0      0                   *:839        *:*
UNCONN      0      0                   *:36812      *:*
UNCONN      0      0       192.168.122.1:domain     *:*
UNCONN      0      0        192.168.1.14:domain     *:*
```

**10. Unix socket**

Tùy chọn -x chỉ có thể được sử dụng để hiển thị các unix socket 

```
[root@centos7 ~]# ss -x
Netid  State      Recv-Q Send-Q Local Address:Port           Peer Address:Port
u_str  ESTAB      0      0      @/tmp/.X11-unix/X0 27818     * 27817
u_str  ESTAB      0      0      @/tmp/.X11-unix/X0 26656     * 26655
u_str  ESTAB      0      0       * 28344                     * 26607
u_str  ESTAB      0      0       * 24704                     * 24705
u_str  ESTAB      0      0      @/tmp/.X11-unix/X0 25195     * 24086
u_str  ESTAB      0      0      @/tmp/dbus-CRqRiw6V 28388    * 28693
```

**11. Hiển thị các thông tin**

Tùy chọn -a hiển thị cả listening sockets và non-listening sockets. Trong trường hợp này của TCP, điều này có nghĩa là các kết nối được 

thiết lập. Tùy chọn này hữu ích khi kết hợp với các tùy chọn khác, ví dụ để hiển thị tất cả UDP socket, ta có thể hiển thị thêm -a, như mặc 

định chỉ với tùy chọn -u. 

```
 ss -u
Recv-Q Send-Q       Local Address:Port           Peer Address:Port
0      0             192.168.1.14:56658          129.250.35.251:ntp
```
```
[root@centos7 ~]# ss -ua
State       Recv-Q Send-Q  Local Address:Port           Peer Address:Port
UNCONN      0      0                   *:mdns           *:*
UNCONN      0      0           127.0.0.1:323            *:*
ESTAB       0      0        192.168.1.14:56658          129.250.35.251:ntp
UNCONN      0      0                   *:21014          *:*
UNCONN      0      0                   *:60009          *:*
UNCONN      0      0       192.168.122.1:domain         *:*
UNCONN      0      0            *%virbr0:bootps         *:*
UNCONN      0      0                   *:bootpc         *:*
UNCONN      0      0                 ::1:323           :::*
UNCONN      0      0                  :::43209         :::*
```

**12. Hiển thị mức sử dụng bộ nhớ socket**

Tùy chọn -m có thể được sử dụng để hiển thị lượng bộ nhớ mà mỗi socket đang sử dụng .

```
[root@centos7 ~]# ss -ltm
State      Recv-Q Send-Q                Local Address:Port       Peer Address:Port
LISTEN     0      128                               *:sunrpc     *:*
  skmem:(r0,rb87380,t0,tb16384,f0,w0,o0,bl0)
LISTEN     0      5                     192.168.122.1:domain     *:*
  skmem:(r0,rb87380,t0,tb16384,f0,w0,o0,bl0)
LISTEN     0      128                               *:ssh        *:*
  skmem:(r0,rb87380,t0,tb16384,f0,w0,o0,bl0)
LISTEN     0      128                       127.0.0.1:ipp        *:*
  skmem:(r0,rb87380,t0,tb16384,f0,w0,o0,bl0)
LISTEN     0      100                       127.0.0.1:smtp       *:*
  skmem:(r0,rb87380,t0,tb16384,f0,w0,o0,bl0)
 ```

 **13. Hiển thị thông tin TCP nội bộ**

 Có thể yêu cầu thêm thông tin TCP nội bộ với tùy chọn -i info

 ```
 [root@centos7 ~]# ss -lti
State      Recv-Q Send-Q                Local Address:Port                        Peer Address:Port
LISTEN     0      128                               *:sunrpc                                    *:*
  cubic rto:1000 mss:536 cwnd:10 lastsnd:373620 lastrcv:373620 lastack:373620
LISTEN     0      5                     192.168.122.1:domain                                    *:*
  cubic rto:1000 mss:536 cwnd:10 lastsnd:373620 lastrcv:373620 lastack:373620
LISTEN     0      128                               *:ssh                                       *:*
  cubic rto:1000 mss:536 cwnd:10 segs_in:2 lastsnd:373620 lastrcv:373620 lastack:373620
LISTEN     0      128                       127.0.0.1:ipp                                       *:*
  cubic rto:1000 mss:536 cwnd:10 lastsnd:373620 lastrcv:373620 lastack:373620
LISTEN     0      100                       127.0.0.1:smtp                                      *:*
```

Bên dưới mỗi listen socket, chúng ta có thể sẽ thêm thông tin. Lưu ý rằng tùy chọn -i không hoạt động với UDP.





