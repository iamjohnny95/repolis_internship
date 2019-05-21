## **Sử dụng lệnh trace route**

**trace route** là một công cụ xác định đường đi được sử dụng để đến đích của gói tin. Công cụ này sử dụng giao thức ICMP, nhưng không giống 

như ping, xác định mọi bộ định tuyến trong đường đi. Lệnh `traceroute` rất hữu ích khi xử lý sự cố mạng. `traceroute` thường hoạt động bằng 

cách gửi một loạt các gói yêu cầu echo ICMP đến đích. 


Trong linux, theo mặc định traceroute sử dụng các gói UDP ở port (33434 - 33534). Lệnh `traceroute` thể hiện các tuyến đường thực hiện các 

tuyến đường thực hiện và chỉ IP và hostname của các router trên mạng.

1.1. Nguyên lý hoạt động của traceroute

Lệnh `traceroute` hoạt động bằng cách gửi các gói có giá trị TTL bắt đầu từ 1 và sau đó tăng từng lần một. Mỗi khi bộ định tuyến nhận được 

gói, nó sẽ kiểm tra trường TTL, nếu trường TTL là 1 thì nó sẽ loại bỏ gói và gửi gói lỗi ICMP chứa địa chỉ IP của nó và đây là yêu cầu của 

`traceroute`. Ví vậy, traceroute tăng dần tìm nạp IP của tất cả các bộ định tuyến giữa nguồn và đích. 

**2. Cài đặt traceroute**

Lệnh `traceroute` có sẵn trên hầu hết các bản phân phối linux. Nếu không được cài đặt sẵn chúng ta thực hiện như sau:

- Đối với bản phân phối Debian/Ubuntu:

```
apt-get install traceroute
```

- Đối với bản phân phối RHEL/Centos

```
yum install traceroute
```

**3. Sử dụng traceroute**

**3.1 Theo dõi đường đi đến máy chủ**

Để theo dõi đường đi địa chỉ ip hoặc tên của máy chủ bạn muốn kết nối. Sử dụng cú pháp như bên dưới: 

```
root@test1 ~]# traceroute google.com
traceroute to google.com (216.58.200.14), 30 hops max, 60 byte packets
 1  gw-102-96-126-130.static.host.vn (102.96.126.130)  1.135 ms  1.337 ms  1.587 ms
 2  210.211.114.109 (210.211.114.109)  2.986 ms  3.047 ms  3.129 ms
 3  210.211.112.241 (210.211.112.241)  0.825 ms  0.814 ms 210.211.112.237 (210.211.112.237)  0.765 ms
 4  115.84.180.41 (115.84.180.41)  1.994 ms 115.84.180.45 (115.84.180.45)  0.806 ms 115.84.180.41 (115.84.180.41)  1.942 ms
 5  localhost (27.68.236.110)  0.944 ms  0.944 ms  0.872 ms
 6  localhost (27.68.236.109)  29.499 ms  32.649 ms  32.589 ms
 7  localhost (27.68.250.210)  28.877 ms  28.868 ms  28.841 ms
 8  74.125.242.34 (74.125.242.34)  44.900 ms * 108.170.254.226 (108.170.254.226)  74.014 ms
 9  216.239.35.168 (216.239.35.168)  42.105 ms 216.239.50.192 (216.239.50.192)  31.823 ms 216.239.35.168 (216.239.35.168)  42.189 ms
10  172.253.66.78 (172.253.66.78)  55.441 ms  55.382 ms 74.125.242.35 (74.125.242.35)  41.020 ms
11  216.239.35.168 (216.239.35.168)  41.984 ms 72.14.232.220 (72.14.232.220)  41.589 ms 216.239.35.154 (216.239.35.154)  65.106 ms
12  216.239.63.214 (216.239.63.214)  69.887 ms 108.170.241.65 (108.170.241.65)  66.678 ms 108.170.241.97 (108.170.241.97)  58.832 ms
13  209.85.240.9 (209.85.240.9)  52.684 ms 216.239.62.241 (216.239.62.241)  64.269 ms 209.85.240.9 (209.85.240.9)  52.608 ms
14  hkg12s11-in-f14.1e100.net (216.58.200.14)  46.108 ms  55.572 ms 108.170.241.65 (108.170.241.65)  66.295 ms
```

Kết quả cho thấy :

- Dòng đầu tiên hiển thị tên máy chủ và ip địch, số bước nhảy tối đa đến máy chủ traceroute sẽ thử và kích thước của các gói byte được gửi.

- Sau đó, mỗi dòng liệt kê một bước nhảy để đến đích. Tên máy chủ được cung cấp, theo sau là ip của tên máy chủ, theo sau là thời gian 

roudtrip cần cho một gói để đến máy chủ và quay lại máy tính khởi tạo.

Ví dụ sau đây cho thấy tracerouterằng không đến đích.

```
[root@test1 ~]# traceroute google.com
traceroute to google.com (216.58.200.14), 30 hops max, 60 byte packets
 1  gw-102-96-126-130.static.host.vn (102.96.126.130)  1.135 ms  1.337 ms  1.587 ms
 2  210.211.114.109 (210.211.114.109)  2.986 ms  3.047 ms  3.129 ms
 3  210.211.112.241 (210.211.112.241)  0.825 ms  0.814 ms 210.211.112.237 (210.211.112.237)  0.765 ms
 4  115.84.180.41 (115.84.180.41)  1.994 ms 115.84.180.45 (115.84.180.45)  0.806 ms 115.84.180.41 (115.84.180.41)  1.942 ms
 5  localhost (27.68.236.110)  0.944 ms  0.944 ms  0.872 ms
 6  localhost (27.68.236.109)  29.499 ms  32.649 ms  32.589 ms
 7  localhost (27.68.250.210)  28.877 ms  28.868 ms  28.841 ms
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
```

Trong ví dụ này, các dấu sao hiển thị mất gói. Điều này có thể có nghĩa là mất mạng, lưu lượng lớn dẫn đến tắc nghẽn mạng hoặc tường lửa làm 

giảm lưu lượng. Lệnh traceroute cho thấy không đến đích được.

**3.2. Cách theo dõi đường đi bằng IPv6**

Để theo dõi tuyến đến máy chủ mạng bằng giao thức IPv6, hãy sử dụng tùy chọn -6 thực hiện như bên dưới.
```
[root@localhost ~]# traceroute -6n ipv6.google.com
traceroute to ipv6.google.com (2404:6800:4003:c03::66), 30 hops max, 80 byte packets
 1  * * *
 2  2400:8901:1011::1  0.994 ms 2400:8901:1111::1  1.015 ms  1.009 ms
 3  2001:cb0:2102:2:f::1  1.446 ms  1.881 ms  1.890 ms
 4  * * *
 5  * * *
 6  * * *
 7  2403:e800:ff00:110::2  169.493 ms  170.370 ms  169.890 ms
 8  2001:4860:1:1:0:121d:0:9  169.858 ms  169.135 ms  169.092 ms
 9  2001:4860:0:1004::e  170.143 ms 2001:4860:0:1007::f  170.028 ms 2001:4860:0:1005::f  170.337 ms
10  2001:4860::c:4001:13cf  180.581 ms  179.847 ms  179.692 ms
11  2001:4860::c:4001:155a  169.808 ms  169.748 ms  169.664 ms
12  2001:4860::c:4001:35e  198.010 ms 2001:4860::c:4001:35d  170.170 ms  169.879 ms
13  2001:4860::c:4000:d475  169.800 ms 2001:4860::c:4000:d474  171.112 ms  169.961 ms
14  2001:4860::31:4000:d362  170.260 ms  170.259 ms  170.053 ms
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * 2404:6800:4003:c03::66  169.932 ms
```

**3.3. Tắt tính năng ánh xạ địa chỉ IP và tên miền**

Lệnh traceroute cung cấp một tùy chọn -n tắt tính năng ánh xạ địa chỉ IP và tên miền.Ví dụ sau đây minh họa điều này:
```
[root@test1 ~]# traceroute -n google.com
traceroute to google.com (216.58.221.238), 30 hops max, 60 byte packets
 1  102.96.126.130  0.713 ms  1.821 ms  2.027 ms
 2  210.211.114.109  2.975 ms  3.033 ms  3.158 ms
 3  210.211.112.237  1.038 ms  1.036 ms  1.122 ms
 4  115.84.180.41  1.680 ms  1.667 ms 115.84.180.45  1.562 ms
 5  27.68.236.110  0.868 ms  0.980 ms  1.073 ms
 6  27.68.236.109  36.358 ms  35.866 ms  32.263 ms
 7  27.68.250.210  28.605 ms  28.587 ms  28.537 ms
 8  * 108.170.240.172  67.091 ms *
 9  72.14.232.100  50.615 ms 108.170.235.206  53.051 ms  53.022 ms
10  216.239.63.214  102.007 ms 172.253.66.78  82.498 ms 108.170.240.242  44.799 ms
11  216.239.35.150  56.527 ms 209.85.142.202  56.440 ms 216.239.35.150  56.059 ms
12  172.253.66.78  82.847 ms 108.170.241.1  44.668 ms 172.253.66.78  82.669 ms
13  216.239.35.150  56.041 ms 108.170.233.1  81.867 ms 216.239.35.150  55.880 ms
14  216.58.221.238  69.951 ms 108.170.241.1  44.763 ms 108.170.241.33  53.487 ms
```

Qua ví dụ trên chúng ta không thấy có tên máy chủ được hiển thị trong kết quả đầu ra.

**3.4. Cấu hình thời gian chờ phản hồi**

Để cấu hình thời gian chờ phản hồi trong traceroute sử dụng tùy chọn -w. Trong ví dụ sau, khoản thời gian phản hồi là 0.01s.
```
[root@test1 ~]# traceroute -w 0.01 google.com
traceroute to google.com (172.217.25.14), 30 hops max, 60 byte packets
 1  gw-102-96-126-130.static.host.vn (102.96.126.130)  0.646 ms  1.206 ms  1.416 ms
 2  210.211.114.109 (210.211.114.109)  3.001 ms  2.976 ms  3.201 ms
 3  210.211.112.237 (210.211.112.237)  0.953 ms  0.927 ms  0.971 ms
 4  115.84.180.45 (115.84.180.45)  1.183 ms  1.351 ms 115.84.180.41 (115.84.180.41)  1.519 ms
 5  localhost (27.68.236.110)  0.977 ms  0.789 ms  0.919 ms
 6  localhost (27.68.236.109)  30.008 ms  30.194 ms *
 7  * * *
 8  * * *
 9  * * *
...
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
```

Qua ví dụ trên chúng ta thấy traceroute đã thử 30 lần và sau đó kết thúc vì không nhận được gói ICMP nào trong 0,01 giây.

**3.5. Cấu hình số lượng truy vấn trên mỗi hop**

Lệnh traceroute sẽ gửi 3 gói mỗi lần nhảy để cung cấp 3 lần khứ hồi. Giá trị mặc định 3 này có thể định cấu hình bằng tùy chọn -q. Tùy chọn 

này cho phép giá trị mới của số lượng gói trên mỗi hop.
```
[root@test1 ~]# traceroute -n -q 6 google.com
traceroute to google.com (216.58.200.14), 30 hops max, 60 byte packets
 1  102.96.126.130  1.453 ms  1.617 ms  1.928 ms  2.107 ms  2.405 ms  2.676 ms
 2  210.211.114.109  3.796 ms  3.772 ms  3.908 ms  3.963 ms  4.028 ms  4.125 ms
 3  210.211.112.237  0.877 ms 210.211.112.241  0.970 ms  1.025 ms  1.018 ms 210.211.112.237  0.740 ms 210.211.112.241  0.829 ms
 4  115.84.180.41  1.611 ms 115.84.180.45  0.974 ms  1.000 ms  0.952 ms 115.84.180.41  1.338 ms  1.586 ms
 5  27.68.236.110  0.939 ms  0.791 ms  1.097 ms  1.070 ms  0.877 ms  0.946 ms
 6  27.68.236.109  35.103 ms  30.284 ms  30.270 ms  28.726 ms  28.735 ms  28.464 ms
 7  27.68.250.210  28.424 ms  28.517 ms  28.466 ms  28.882 ms  28.789 ms  28.734 ms
 8  * * 108.170.254.227  31.643 ms 108.170.240.242  44.672 ms 74.125.242.34  44.853 ms 108.170.240.242  44.827 ms
 9  216.239.35.174  32.582 ms 108.170.232.170  31.744 ms 72.14.235.60  67.874 ms 216.239.35.174  32.371 ms 108.170.235.206  53.002 ms 216.239.35.154  64.116 ms
10  216.239.63.214  69.261 ms 108.170.240.164  66.004 ms 108.170.254.227  30.972 ms 74.125.242.34  44.903 ms 216.239.63.214  69.719 ms  69.532 ms
11  216.239.63.217  69.994 ms  69.740 ms  69.782 ms 72.14.232.222  31.088 ms 216.239.35.154  64.058 ms 72.14.232.222  29.012 ms
12  108.170.241.97  56.180 ms 108.170.241.65  66.378 ms 216.239.63.214  69.426 ms  69.566 ms  69.579 ms  69.475 ms
13  209.85.240.11  44.915 ms 209.85.142.27  48.475 ms 209.85.240.9  44.969 ms 209.85.142.27  55.064 ms 209.85.240.9  45.084 ms 209.85.142.27  56.407 ms
14  216.58.200.14  45.015 ms  45.157 ms  44.928 ms  45.696 ms  55.744 ms  44.926 ms
```

**3.6. Cấu hình giá trị TTL để bắt đầu**

Lệnh traceroute chấp nhận giá trị TTL mà bạn muốn bắt đầu. Theo mặc định, giá trị của nó là 1, có nghĩa là nó bắt đầu với bộ định tuyến đầu 

tiên trong đường dẫn nhưng sử dụng tùy chọn -f có thể đặt giá trị mới của trường TTL.
```
[root@test1 ~]# traceroute -n google.com
traceroute to google.com (216.58.199.110), 30 hops max, 60 byte packets
 1  102.96.126.130  2.855 ms  3.070 ms  3.387 ms
 2  * * *
 3  210.211.112.237  0.865 ms  0.860 ms  0.933 ms
 4  115.84.180.41  1.459 ms  1.464 ms 115.84.180.45  1.172 ms
 5  27.68.236.110  0.818 ms  0.966 ms  0.770 ms
 6  27.68.236.109  32.474 ms  31.046 ms  31.027 ms
 7  27.68.250.210  28.820 ms  28.861 ms  28.851 ms
 8  * 74.125.242.35  28.300 ms 108.170.254.226  63.898 ms
 9  108.170.233.64  31.301 ms 72.14.235.60  74.300 ms 108.170.237.232  46.440 ms
10  172.253.66.78  45.909 ms 108.170.240.242  44.717 ms 108.170.254.226  64.027 ms
11  72.14.235.60  80.393 ms 72.14.232.222  42.415 ms 72.14.232.220  32.767 ms
12  172.253.66.78  45.914 ms 108.170.241.33  45.838 ms 172.253.66.78  45.622 ms
13  72.14.239.95  65.596 ms 72.14.233.169  46.078 ms 209.85.142.202  45.181 ms
14  108.170.241.1  44.746 ms 216.58.199.110  51.646 ms 108.170.241.33  45.624 ms
[root@test1 ~]# traceroute -n -f 10 google.com
traceroute to google.com (216.58.199.110), 30 hops max, 60 byte packets
10  172.253.66.78  45.787 ms 216.239.63.214  77.202 ms 74.125.242.35  51.737 ms
11  72.14.232.222  51.190 ms 216.239.35.168  45.402 ms  45.396 ms
12  172.253.66.78  45.609 ms 108.170.241.33  45.868 ms 108.170.241.1  44.781 ms
13  74.125.251.10  52.517 ms 72.14.239.95  65.658 ms 209.85.142.202  45.382 ms
14  108.170.241.1  44.733 ms  44.714 ms 216.58.199.110  51.709 ms
```

Qua ví dụ trên chúng ta thấy khi sử dụng tùy chọn -f với giá trị 10, chỉ dòng thứ 10 đến cuối cùng được hiển thị.

**3.7. Cấu hình thay đổi số lượng TTL**

Time To Live xác định có bao nhiêu router lệnh traceroute sẽ theo dõi trên đường đến đích của nó. Giá trị TTL mặc định là 30, có nghĩa là, 

chỉ có 30 hop được theo dõi theo mặc định.

Để thay đổi giá trị TTL chúng ta sử dụng tùy chọn -m.

Ví dụ: Nếu bạn muốn 5 hop đầu tiên trên đường đến đích của google.com, hãy chạy lệnh sau:
```
[root@test1 ~]# traceroute -n -m 5 google.com
traceroute to google.com (216.58.197.110), 5 hops max, 60 byte packets
 1  102.96.126.130  2.172 ms  2.392 ms  2.679 ms
 2  * * *
 3  210.211.112.241  1.084 ms 210.211.112.237  1.074 ms 210.211.112.241  1.055 ms
 4  115.84.180.41  1.722 ms  1.934 ms 115.84.180.45  1.124 ms
 5  27.68.236.110  1.022 ms  1.159 ms  0.894 ms
 ```

 

 