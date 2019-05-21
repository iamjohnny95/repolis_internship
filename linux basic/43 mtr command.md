## **Câu lệnh mtr**

**1.Giới thiệu mtr**

**mtr** là một công cụ chẩn đoán mạng mạnh mẽ cung cấp chức năng 

của 2 lệnh là ping và traceroute. Nó là một công cụ đơn giản và 

đa nền tảng in thông tin về toàn bộ tuyến đường mà các gói mạng 

thực hiện. Lệnh `mtr` lợi thế hơn `traceroute` vì nó cũng in tỷ 

lệ phần trăm phản hồi và thời gian đáp ứng cho tất cả các bước 

nhảy mạng giữa hai hệ thống.

**2. Cài đặt mtr**

Hệ điều hành Linux

- Đối với bản ubuntu

```
apt update && apt upgrade
apt install mtr-tiny
```

- Đối với bản phân phối CentOS

```
yum update
yum install mtr
```

**3.Sử dụng lệnh mtr trên hệ thống dựa trên Unix**

Tạo báo cáo mtr bằng cú pháp sau:

```
mtr [tùy chọn] [destination_host]
```

Các tùy chọn thường dùng:

- Tùy chọn `r` cờ tạo ra các báo cáo (viết tắt -report)

- Tùy chọn `w` cờ sử dụng long-version của hostname để các kỹ 

thuật viên và bạn sẽ nhìn thấy tên hostname đầy đủ 

- Tùy chọn `c` cờ đặt bao nhiêu gói tin được gửi đi và được ghi 

trong báo cáo. Khi không được sử dụng, thông thường mặc định sẽ 

là 10, nhưng trong khoảng thời gian nhanh hơn, bạn có thể muốn 

đặt thành 50 hoặc 100.

- Tùy chọn `i` cờ chạy báo cáo với tốc độ nhanh để lộ mất gói tin

có thể xảy ra chỉ trong thời gian tắc nghẽn mạng. Cờ này hướng 

dẫn mtr gửi một gói trong n giây. Mặc định là 1 giây, do đó 

chúng ta có thể đặt nó thành (0,1, 0,2, v.v)

- Tùy chọn `--xml` in đầu ra dạng xml

**Ví dụ 1** Hiển thị cả thên máy chủ và địa chỉ IP

Tùy chọn `-b` trong lệnh `mtr` cho phép bạn hiển thị cả địa chỉ 

IP và tên máy chủ trong báo cáo theo dõi. Được thực hiển như bên

dưới:

```
[root@test1 ~]# mtr -b google.com
                                                         My traceroute  [v0.85]
test1.novalocal (0.0.0.0)                                                                                       Wed Apr  3 08:45:52 2019
Resolver: Received error response 2. (server failure)er of fields   quit
                                                                                                Packets               Pings
 Host                                                                                         Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. gw-102-96-126-130.static.host.vn (102.96.126.130)                                          0.0%     7    0.9  11.5   0.8  75.3  28.2
 2. 210.211.114.109                                                                            0.0%     7    2.4   3.2   2.3   7.0   1.6
 3. 210.211.112.241                                                                            0.0%     7    1.0   1.1   1.0   1.2   0.0
 4. 115.84.180.45                                                                              0.0%     7    1.1   1.3   1.1   1.6   0.0
 5. localhost (27.68.236.110)                                                                  0.0%     7    1.1   1.1   1.0   1.2   0.0
 6. localhost (27.68.236.109)                                                                  0.0%     7   34.2  34.2  30.4  35.7   1.7
 7. localhost (27.68.250.210)                                                                  0.0%     6   28.5  28.9  28.5  29.8   0.0
 8. ???
 9. 209.85.242.200                                                                             0.0%     6   43.3  43.3  43.2  43.4   0.0
1.  108.170.254.227                                                                            0.0%     6   41.7  41.6  41.4  41.9   0.0
2.  216.239.35.168                                                                             0.0%     6   45.4  45.4  45.3  45.6   0.0
3.  172.253.66.78                                                                              0.0%     6   46.2  46.1  45.9  46.2   0.0
4.  216.239.35.150                                                                             0.0%     6   56.0  56.5  55.9  58.4   0.8
5.  108.170.241.33                                                                             0.0%     6   45.9  45.9  45.8  46.0   0.0
6.  108.170.235.11                                                                             0.0%     6   53.5  53.5  53.3  54.2   0.0
7.  hkg07s29-in-f14.1e100.net (172.217.161.174)                                                0.0%     6   44.8  44.8  44.7  44.9   0.0
```

**Ví dụ 2: Giới hạn cho số lượng gói tin gửi đi**

Chúng ta có thể giới hạn số lượng gói tin bằng cách sử dụng tùy 

chọn `-c [number]`

```
[root@test1 ~]# mtr -c 5 google.com
                                                         My traceroute  [v0.85]
test1.novalocal (0.0.0.0)                                                                                       Wed Apr  3 08:49:43 2019
Resolver: Received error response 2. (server failure)er of fields   quit
                                                                                                Packets               Pings
 Host                                                                                         Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. gw-102-96-126-130.static.host.vn                                                        0.0%     5    0.7   0.8   0.7   0.9   0.0
 2. 210.211.114.109                                                                            0.0%     5    2.6   3.1   2.5   4.1   0.0
 3. 210.211.112.237                                                                            0.0%     5    1.1   1.2   1.0   1.5   0.0
 4. 115.84.180.41                                                                              0.0%     5    3.8   5.8   1.5  12.7   5.0
 5. localhost                                                                                  0.0%     5    1.0   2.2   1.0   6.1   2.1
 6. localhost                                                                                  0.0%     5   33.4  32.5  28.6  35.8   2.5
 7. localhost                                                                                  0.0%     5   28.5  28.7  28.5  29.2   0.0
 8. ???
 9. 74.125.251.206                                                                             0.0%     5   31.0  30.9  30.7  31.1   0.0
1.  108.170.240.242                                                                            0.0%     5   44.8  44.8  44.6  44.8   0.0
2.  216.239.50.192                                                                             0.0%     5   29.2  29.2  29.1  29.4   0.0
3.  172.253.66.78                                                                              0.0%     5   46.0  46.0  45.8  46.1   0.0
4.  209.85.142.202                                                                             0.0%     5   45.3  45.6  45.3  46.8   0.0
5.  108.170.241.33                                                                             0.0%     5   46.0  45.9  45.7  46.1   0.0
6.  108.170.233.3                                                                              0.0%     5   47.3  46.7  45.6  47.6   0.7
7.  hkg07s21-in-f14.1e100.net                                                                  0.0%     5   68.4  68.3  68.2  68.4   0.0
```

Qua ví dụ trên ta thấy khi giới hạn số lượng gói tin là 5 thì 

cột `SNT` chỉ chạy đến 5 và dừng lại. Cột `Snt` đến số gói tin 

gửi đi.

**Ví dụ 3**: Sử dụng chế độ báo cáo

Thay vì hiển thị đầu ra của lệnh `mtr` trên màn hình, chúng ta 

có thể sử dụng chế độ báo cáo bằng tùy chọn `-r` như bên dưới:

```
[root@test1 ~]# mtr -r -c 5 google.com
Start: Wed Apr  3 09:42:05 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%     5    0.9   0.8   0.8   0.9   0.0
  2.|-- 210.211.114.109            0.0%     5    2.5   2.5   2.4   2.7   0.0
  3.|-- 210.211.112.241            0.0%     5    1.2   1.1   1.0   1.2   0.0
  4.|-- 115.84.180.45              0.0%     5    1.0   1.2   1.0   1.4   0.0
  5.|-- localhost                  0.0%     5    1.0   1.2   1.0   2.0   0.0
  6.|-- localhost                  0.0%     5   35.0  33.1  29.5  35.0   2.2
  7.|-- localhost                  0.0%     5   28.6  28.6  28.6  28.7   0.0
  8.|-- ???                       100.0     5    0.0   0.0   0.0   0.0   0.0
  9.|-- 209.85.242.200             0.0%     5   30.8  30.7  30.5  31.2   0.0
 10.|-- 108.170.254.227            0.0%     5   30.1  29.0  28.7  30.1   0.5
 11.|-- 216.239.35.174             0.0%     5   38.3  43.8  28.9  69.1  16.2
 12.|-- 216.239.63.214             0.0%     5   68.6  69.0  68.5  69.7   0.0
 13.|-- 216.239.63.230             0.0%     5   58.8  55.9  52.7  61.5   3.9
 14.|-- 108.170.241.1              0.0%     5   44.8  44.8  44.8  44.8   0.0
 15.|-- 74.125.252.89              0.0%     5   64.0  64.6  64.0  66.6   1.0
 16.|-- hkg07s29-in-f14.1e100.net  0.0%     5   44.8  44.8  44.7  44.9   0.0
 ```

 **Ví dụ 4: Chuyển đầu ra báo cáo và file**

 Chuyển đầu ra của báo cáo vào file chúng ta thực hiện như sau;

 ```
 [root@test1 ~]# mtr -r -c 5 google.com > mtr-report
[root@test1 ~]# cat mtr-report
Start: Wed Apr  3 09:44:51 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%     5    0.8   0.7   0.7   0.8   0.0
  2.|-- 210.211.114.109            0.0%     5    2.9   2.7   2.4   2.9   0.0
  3.|-- 210.211.112.241            0.0%     5    1.1   1.3   0.9   2.3   0.5
  4.|-- 115.84.180.45              0.0%     5    1.1   1.2   1.0   1.5   0.0
  5.|-- localhost                  0.0%     5    1.0   1.0   0.9   1.1   0.0
  6.|-- localhost                  0.0%     5   33.3  30.7  28.5  33.3   1.7
  7.|-- localhost                  0.0%     5   28.6  28.6  28.5  28.8   0.0
  8.|-- ???                       100.0     5    0.0   0.0   0.0   0.0   0.0
  9.|-- 108.170.237.234            0.0%     5   44.7  44.6  44.6  44.7   0.0
 10.|-- 74.125.242.34              0.0%     5   44.9  44.9  44.8  44.9   0.0
 11.|-- 72.14.235.152              0.0%     5   36.4  38.2  36.4  45.5   4.0
 12.|-- 172.253.66.78              0.0%     5   46.3  46.3  46.1  46.5   0.0
 13.|-- 216.239.35.150             0.0%     5   60.7  63.6  56.1  88.9  14.3
 14.|-- 108.170.241.33             0.0%     5   46.0  46.0  46.0  46.1   0.0
 15.|-- 209.85.243.23              0.0%     5   63.8  63.8  63.6  64.2   0.0
 16.|-- hkg07s24-in-f14.1e100.net  0.0%     5   69.5  69.8  69.2  71.7   1.0
 ```

Báo cáo được lưu trong thư mục home của người dùng hiện tại theo

mặc định. Chúng ta có thể chỉ định một đường dẫn thích hợp để 

báo cáo được lưu.

**Ví dụ 5: Sử dụng gói TCP SYN hoặc datagram UDP

CHúng ta có thể sử dụng TCP SYN hoặc UDP datagram để yêu cầu mtr

thay vì các yêu cầu ICMP ECHO mặc định bằng cách chúng ta sử 

dụng cờ `--udp` và `--tcp` như bên dưới:

```
[root@test1 ~]# mtr -r --tcp google.com
Start: Wed Apr  3 09:50:47 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%    10    3.1   1.1   0.7   3.1   0.7
  2.|-- 210.211.114.109            0.0%    10    2.8   3.0   2.4   4.3   0.3
  3.|-- 210.211.112.241            0.0%    10    1.2   1.3   0.8   2.1   0.0
  4.|-- 115.84.180.45              0.0%    10    1.1   1.4   1.1   2.0   0.0
  5.|-- localhost                  0.0%    10    1.1   1.1   1.0   1.4   0.0
  6.|-- localhost                  0.0%    10   45.1  45.0  41.4  48.5   1.8
  7.|-- localhost                  0.0%    10  7058. 2049.  41.9 7062. 2794.3
  8.|-- 108.170.240.172            0.0%    10   45.0  73.6  41.8 128.5  38.3
  9.|-- 74.125.242.35              0.0%    10  125.3  88.8  36.7 128.1  40.9
 10.|-- 216.239.35.174             0.0%    10   73.3  72.5  46.1 129.0  31.5
 11.|-- 216.239.63.217             0.0%    10   82.3  66.0  45.4  84.1  14.5
 12.|-- 216.239.63.217             0.0%    10   56.4  63.7  50.8  76.6   7.3
 13.|-- 216.239.40.31              0.0%    10   66.1  52.1  45.8  66.5   8.6
 14.|-- 172.253.64.111             0.0%    10   46.0  90.2  45.7 134.8  46.8
 15.|-- hkg12s18-in-f14.1e100.net  0.0%    10  134.2  88.6  66.8 201.4  44.7
[root@test1 ~]# mtr -r --udp google.com
Start: Wed Apr  3 09:51:16 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%    10    2.2   1.1   0.8   2.2   0.3
  2.|-- 210.211.114.109            0.0%    10    3.0   2.6   2.3   3.0   0.0
  3.|-- 210.211.112.241            0.0%    10    1.0   1.0   0.9   1.2   0.0
  4.|-- 115.84.180.41              0.0%    10    1.7   1.5   1.1   1.8   0.0
  5.|-- localhost                  0.0%    10    1.1   1.1   1.0   1.4   0.0
  6.|-- localhost                 10.0%    10   54.6  47.8  41.6  58.1   5.3
  7.|-- localhost                 30.0%    10   50.7  57.3  50.7  64.2   4.4
  8.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
  ```

  **Ví dụ 6: Chỉ định kích thước gói**

  Sử dụng tùy chọn `-s` trong lệnh mtr chỉ định kích thước đơn 

  vị là byte thực hiện như sau:

  ```
  [root@test1 ~]# mtr -r -s 60 google.com
Start: Wed Apr  3 09:53:46 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%    10    0.7   4.6   0.7  17.1   6.6
  2.|-- 210.211.114.109            0.0%    10    2.4   2.8   2.4   4.7   0.6
  3.|-- 210.211.112.237            0.0%    10    0.9   1.1   0.9   1.3   0.0
  4.|-- 115.84.180.41              0.0%    10    1.7   1.7   1.6   2.1   0.0
  5.|-- localhost                  0.0%    10    1.0   1.0   0.9   1.2   0.0
  6.|-- localhost                  0.0%    10   31.3  32.3  29.7  35.9   2.4
  7.|-- localhost                  0.0%    10   29.0  28.8  28.6  29.0   0.0
  8.|-- 108.170.240.242            0.0%    10   44.9  44.9  44.8  45.5   0.0
  9.|-- 216.239.50.192             0.0%    10   36.5  36.3  36.2  36.5   0.0
 10.|-- 172.253.66.78              0.0%    10   46.1  46.1  45.9  46.3   0.0
 11.|-- 216.239.62.241             0.0%    10   63.8  64.7  63.8  68.2   1.7
 12.|-- 108.170.241.97             0.0%    10   56.3  56.3  56.2  56.5   0.0
 13.|-- 216.239.40.31              0.0%    10   45.9  46.0  45.6  46.9   0.0
 14.|-- hkg12s18-in-f14.1e100.net  0.0%    10   45.1  45.1  45.1  45.2   0.0
 ```

 **VÍ dụ 7: In đầu ra dạng XML**

 Lệnh `mtr` hỗ trợ định dạng XML để in báo cáo theo dõi bằng 

 việc sử dụng tùy chọn `--xml`:

 ```
 [root@test1 ~]# mtr --xml google.com
<MTR SRC="test1.novalocal" DST="google.com" TOS="0x0" PSIZE="64" BITPATTERN="0x00" TESTS="10">
    <HUB COUNT="1" HOST="gw-103-97-125-129.static.123host.vn">
        <Loss%>  0.0%</Loss%>
        <Snt>    10</Snt>
        <Last>   1.0</Last>
        <Avg>   0.8</Avg>
        <Best>   0.7</Best>
        <Wrst>   1.0</Wrst>
        <StDev>   0.0</StDev>
    </HUB>
    <HUB COUNT="2" HOST="210.211.114.109">
        <Loss%>  0.0%</Loss%>
        <Snt>    10</Snt>
        <Last>   2.4</Last>
        <Avg>   2.4</Avg>
        <Best>   1.8</Best>
        <Wrst>   2.6</Wrst>
        <StDev>   0.0</StDev>
    </HUB>
    ...
    ```

    **4 Đọc báo cáo mtr**

    Các báo cáo `mtr` chứa rất nhiều thông tin. Báo cáo được tạo

    với `mtr --report google.com` sử dụng tùy chọn `--report`,sẽ

    gửi mặc định 10 gói đến máy chủ google.com và tạo một báo 

    cáo. Mỗi dòng được đánh số trong báo cáo đại diện cho một 

    hop. Hop là các nút internet mà các gói đi qua để đến đích. 

    Nếu chúng ta muốn bỏ qua phần ta chứ rDNS có thẻ sử dụng tùy

    chonj` --no-dns` như sau:

    ```
    [root@test1 ~]# mtr --report --no-dns google.com
Start: Tue Apr  2 18:41:11 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 102.96.126.130             0.0%    10    1.0   1.1   0.8   2.5   0.3
  2.|-- 210.211.114.109            0.0%    10    2.7   2.6   2.2   3.0   0.0
  3.|-- 210.211.112.241            0.0%    10    1.1   1.2   0.9   1.9   0.0
  4.|-- 115.84.180.45              0.0%    10    1.2   1.2   1.1   1.4   0.0
  5.|-- 27.68.236.110              0.0%    10    1.1   1.1   0.9   1.9   0.0
  6.|-- 27.68.236.109              0.0%    10   30.7  34.1  30.7  38.4   2.8
  7.|-- 27.68.250.210              0.0%    10   31.1  30.8  30.7  31.1   0.0
  8.|-- 108.170.254.227            0.0%    10   54.3  47.8  46.1  54.3   3.3
  9.|-- 216.239.35.174             0.0%    10   45.9  50.1  45.1  86.2  12.7
 10.|-- 216.239.63.214             0.0%    10   71.9  73.2  69.5 100.5   9.6
 11.|-- 216.239.63.217             0.0%    10   69.0  69.0  68.9  69.4   0.0
 12.|-- 108.170.241.65             0.0%    10   65.7  65.7  65.6  65.9   0.0
 13.|-- 209.85.143.119             0.0%    10   45.5  45.5  45.4  45.7   0.0
 14.|-- 172.217.24.206             0.0%    10   53.2  53.2  53.2  53.4   0.0
 ```
Đầu ra của mtr có ba phần chính tùy thuộc vào cấu hình. 2 hoặc 3 hop đầu tiên thường đại diện cho ISP của máy chủ nguồn, 2 hoặc 3 hop cuối 

cùng đại diện cho ISP của máy chủ đích. Các bước nhảy ở giữa là các bộ định tuyến mà gói đi qua để đến đích.

Ngoài việc cung cấp đường dẫn giữa các máy chủ mà các gói đi đến đích, mtr cung cấp các số liệu thống kê có giá trị về độ bền của kết nối:

- Cột `Loss%` cho thấy tỷ lệ mất gói tin tại mỗi hop.

- Cột `Snt` đếm số gói tin gửi đi. Mặt định tùy chọn `--report` sẽ gửi 10 gói tin, nếu như xác định số gói tin bằng tùy chọn 

`--report-cycles=[number-of-packets]`, trong đó `number-of-packets` là tổng số các gói tin mà bạn muốn gửi đến các máy chủ từ xa.

- Bốn cột `Last, Avg, Best`, và `Wrst` là tất cả các phép đo của độ trễ trong mili giây (ms). `Last` là độ trễ của gói cuối cùng được gửi. 

`Avg` là độ trễ trung bình của tất cả các gói. `Best` và `Wrst` hiển thị thời di chuyển của gói tin mạng round-trip cho một gói đến máy chủ 

này.

- Cột `StDev` cung cấp độ lêch chuẩn của độ chễ cho mỗi máy chủ. Độ lệch chuẩn càng cao, sự khác biệt giữa các phép đo độ trễ càng lớn.

**5. Phân tích báo cáo mtr**

Khi phân tích mtr chúng ta cần chú ý hai điều: mất và độ trễ.

**5.1. Xác nhận mất gói**

```
[root@test1 ~]# mtr --report www.google.com
Start: Tue Apr  2 19:19:33 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%    10    2.2   1.0   0.7   2.2   0.5
  2.|-- 210.211.114.109           20.0%    10    2.6   3.7   2.4   8.0   1.7
  3.|-- 210.211.112.237            0.0%    10    1.4   1.3   1.0   1.9   0.0
  4.|-- 115.84.180.41              0.0%    10    2.0   1.8   1.6   2.5   0.0
  5.|-- localhost                  0.0%    10    1.1   1.0   0.9   1.2   0.0
  6.|-- localhost                  0.0%    10   35.2  32.2  29.2  35.6   2.4
  7.|-- localhost                  0.0%    10   28.7  28.8  28.5  29.5   0.0
  8.|-- 108.170.240.172            0.0%    10   71.2  70.4  67.3  76.6   2.8
  9.|-- 216.239.57.50              0.0%    10   42.1  42.8  41.9  47.9   1.8
 10.|-- 209.85.242.214             0.0%    10   44.8  45.3  44.7  48.5   1.0
 11.|-- 209.85.142.24              0.0%    10  153.6 156.6 150.3 162.0   3.5
 12.|-- 108.170.241.1              0.0%    10   44.8  44.7  44.7  44.8   0.0
 13.|-- 72.14.234.63               0.0%    10   45.4  46.0  45.4  48.9   0.9
 14.|-- hkg07s28-in-f4.1e100.net   0.0%    10   69.2  69.2  69.1  69.4   0.0
 ```

 Trong trường hợp này, tỷ lệ mất gói được báo cáo giữa các bước 1 và 2 có thể là do giới hạn tốc độ trên bước nhảy thứ 2. Mặc dù lưu lượng

truy cập đến 12 bước còn lại đều chạm vào bước nhảy thứ 2, nhưng không có mất gói. Nếu mất liên tục nhiều hơn một bước nhảy, thì có thể có 

một số vấn đề mất gói hoặc định tuyến.

**5.2. Độ trễ mạng**

Lệnh `mtr` giúp chúng ta đánh giá độ trễ của kết nối giữa máy chủ của bạn và máy chủ đích. Nhờ các ràng buộc vật lý, độ trễ luôn tăng theo

số hop trong một tuyến đường. Độ trễ thường tương đối và phụ thuộc rất nhiều vào chất lượng của cả kết nối của máy chủ và khoảng cách vật 

lý của chúng. Chất lượng kết nối cũng có thể ảnh hưởng đến độ trễ bạn trải nghiệm cho một tuyến đường cụ thể.

**6. Báo cáo mtr thường gặp**

Nếu bạn đang gặp một số vấn đề về mạng và muốn chẩn đoán sự cố của mình, hãy xem xét các ví dụ sau.

**6.1 Mạng máy chủ đích được cấu hình không đúng**

Trong ví dụ dưới đây mất 100% gói tin cho máy chủ đích do bộ định tuyến được cấu hình không chính xác. Có vẻ các gói không đến được máy chủ 

nhưng đây không phải là trường hợp.

```
[root@test1 ~]# mtr --report www.google.com
Start: Tue Apr  2 19:56:51 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- gw-102-96-126-130.static.  0.0%    10    0.8   1.3   0.8   4.5   0.9
  2.|-- 210.211.114.109            0.0%    10    3.9   2.9   2.4   4.6   0.7
  3.|-- 210.211.112.241            0.0%    10    1.2   1.2   1.0   1.7   0.0
  4.|-- 115.84.180.45              0.0%    10    1.2   1.3   1.2   1.5   0.0
  5.|-- localhost                  0.0%    10    1.1   1.2   0.9   1.8   0.0
  6.|-- localhost                  0.0%    10   34.6  34.9  31.7  37.6   1.8
  7.|-- localhost                  0.0%    10   31.0  31.0  30.7  32.0   0.3
  8.|-- 108.170.240.242            0.0%    10   36.6  36.6  36.4  37.2   0.0
  9.|-- 216.239.35.154             0.0%    10   51.1  47.6  42.3  51.8   4.0
 10.|-- 216.239.63.214             0.0%    10   70.0  74.6  69.5 112.1  13.2
 11.|-- 209.85.142.27              0.0%    10   45.1  46.9  45.1  55.1   3.6
 12.|-- 108.170.241.65             0.0%    10   65.5  65.5  65.5  65.5   0.0
 13.|-- 209.85.241.209             0.0%    10   45.6  46.3  45.6  49.5   1.1
 14.|-- hkg12s17-in-f4.1e100.net  100.0    10    0.0   0.0   0.0   0.0   0.0
 ```

 Không đến được máy chủ đích. Tuy nhiên, báo cáo mtr cho thấy mất vì máy chủ đích không gửi trả lời. Đây có thể là kết quả của các quy tắc

 mạng hoặc tường lửa (iptables) được cấu hình không đúng khiến máy chủ bỏ các gói ICMP.

 **6.2. Home Router**

 Home Router đôi khi gây ra các báo cáo sai lệch như bên dưới:

 ```
 [root@test1 ~]# mtr --no-dns --report google.com
Start: Tue Apr  2 20:02:04 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 102.96.126.130             0.0%    10    0.9   0.8   0.7   0.9   0.0
  2.|-- 210.211.114.109            0.0%    10    2.5   2.8   2.4   3.5   0.0
  3.|-- 210.211.112.241            0.0%    10    1.0   1.2   0.9   1.8   0.0
  4.|-- 115.84.180.45              0.0%    10    1.1   1.4   1.0   2.8   0.5
  5.|-- 27.68.236.110              0.0%    10    1.0   1.0   0.9   1.3   0.0
  6.|-- 27.68.236.109              0.0%    10   32.0  33.8  31.3  36.8   1.9
  7.|-- 27.68.250.210              0.0%    10   30.8  30.8  30.6  31.0   0.0
  8.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
  9.|-- 72.14.232.106              0.0%    10   46.3  45.1  43.1  50.5   2.4
 10.|-- 108.170.254.226            0.0%    10   61.9  61.9  61.7  62.1   0.0
 11.|-- 72.14.235.152              0.0%    10   36.8  31.7  29.6  37.4   3.0
 12.|-- 216.239.41.95              0.0%    10   57.4  57.6  57.2  58.8   0.3
 13.|-- 74.125.252.142             0.0%    10   56.7  58.4  56.7  63.9   2.4
 14.|-- 209.85.247.199             0.0%    10  168.7 168.6 159.9 174.4   5.1
 ```

 Tỷ lệ mất gói tin tại hop thứ 8 là 100% được báo cáo không cho thấy có vấn đề. Bạn có thể thấy rằng không có mất mát trên các bước nhảy 

 tiếp theo.

 **6.3. Một bộ định tuyến ISP không được cấu hình đúng**

 Đôi khi một bộ định tuyến trên tuyến mà gói tin của bạn được cấu hình không chính xác và các gói của bạn có thể không bao giờ đến đích:

 ```
 [root@test1 ~]# mtr --no-dns --report google.com
Start: Tue Apr  2 20:02:04 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 102.96.126.130             0.0%    10    0.9   0.8   0.7   0.9   0.0
  2.|-- 210.211.114.109            0.0%    10    2.5   2.8   2.4   3.5   0.0
  3.|-- 210.211.112.241            0.0%    10    1.0   1.2   0.9   1.8   0.0
  4.|-- 115.84.180.45              0.0%    10    1.1   1.4   1.0   2.8   0.5
  5.|-- 27.68.236.110              0.0%    10    1.0   1.0   0.9   1.3   0.0
  6.|-- 27.68.236.109              0.0%    10   32.0  33.8  31.3  36.8   1.9
  7.|-- 27.68.250.210              0.0%    10   30.8  30.8  30.6  31.0   0.0
  8.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
  9.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 10.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 11.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 12.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 13.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 14.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 ```

 Đôi khi, một bộ định tuyến được cấu hình kém sẽ gửi các gói trong một vòng lặp. Bạn có thể thấy điều đó trong ví dụ sau:

 ```
 [root@test1 ~]# mtr --no-dns --report google.com
Start: Tue Apr  2 20:02:04 2019
HOST: test1.novalocal             Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 102.96.126.130             0.0%    10    0.9   0.8   0.7   0.9   0.0
  2.|-- 210.211.114.109            0.0%    10    2.5   2.8   2.4   3.5   0.0
  3.|-- 210.211.112.241            0.0%    10    1.0   1.2   0.9   1.8   0.0
  4.|-- 115.84.180.45              0.0%    10    1.1   1.4   1.0   2.8   0.5
  5.|-- 27.68.236.110              0.0%    10    0.0   0.0   0.0   0.0   0.0
  6.|-- 27.68.236.109              0.0%    10    0.0   0.0   0.0   0.0   0.0
  7.|-- 27.68.236.110              0.0%    10    0.0   0.0   0.0   0.0   0.0
  8.|-- 27.68.236.109              0.0%    10    0.0   0.0   0.0   0.0   0.0
  9.|-- 27.68.236.110              0.0%    10    0.0   0.0   0.0   0.0   0.0
 10.|-- 27.68.236.109              0.0%    10    0.0   0.0   0.0   0.0   0.0
 11.|-- 27.68.236.110              0.0%    10    0.0   0.0   0.0   0.0   0.0
 12.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 13.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 14.|-- ???                        0.0%    10    0.0   0.0   0.0   0.0   0.0
 ```

 Báo cáo này cho thấy bộ định tuyến tại hop 4 không được cấu hình đúng. Khi những tình huống này xảy ra, cách duy nhất để giải quyết vấn đề

 là liên hệ với nhóm các nhà khai thác của quản trị viên mạng tại máy chủ nguồn.








