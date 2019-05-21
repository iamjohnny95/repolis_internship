## **Netstat Command**

**Giới thiệu*

Lệnh **netstat** trên linux là một lệnh nằm trong số các tập lệnh để giám sát hệ thống trong Linux, **netstat** giám sát chiều in và chiều 

out kết nối vào server, hoặc các tuyến đường route, trạng thái của card mạng. Lệnh **netstat** rất hữu dụng trong việc giải quyết các vấn đề,

sự cố liên quan đến network như là lượng connect kết nối, trafic, tốc độ, trạng thái của từng port, ip...

## **Hướng dẫn**

Lệnh 1

`netstat -at`

Kiểm tra các port đang sử dụng phương thức TCP

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/1.png)

Lệnh 2

`netstat -au`

Kiểm tra các port đang sử dụng phương thức UDP

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/2.png)

Lệnh 3

`netstat -l`

Liệt kê tất cả các port đang trong trạng thái active listening.

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/3.png)

Lệnh 4

`netstat -a`

Liệt kê tất cả các port TCP/UDP ở trạng thái listening

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/4.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/4.png)

Lệnh 5

`netstat -lt`

Liệt kê các port TCP ở trạng thái listening

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/5.png)

Lệnh 6

`netstat -lu`

Liệt kê tất cả các port UDP ở dạng LISTEN

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/6.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/6.png)

Lệnh 7

`netstat -lx`

Liệt kê tất cả các cổng Unix đang lắng nghe

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/7.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/7.png)

Lệnh 8

`netstat -s`

Hiển thị thống kê giao thức. Mặc định sẽ hiện thị thống kê theo TCP, UDP, ICMP và IP. Sử dụng tùy chọn -s để xác định một giao thức cụ thể 

muốn thống kê.

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/8.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/8.png)

Lệnh 9

`netstat -st`

Thống kê chỉ riêng giao thức TCP

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/9.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/9.png)

Lệnh 10

`netstat -su`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/10.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/10.png)

Lệnh 11

`netstat -tp`

Hiển thị tên dịch vụ với PID

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/11.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/11.png)

Lệnh 12

`netstat -r`

Hiển thị thông tin bảng định tuyến 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/12.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/12.png)

Lệnh 13

`netstat -i`

Hiển thị các thông tin hoạt động của các Network Interface

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/13.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/13.png)

Lệnh 14

`netstat -ie`

Hiển thị các thông tin IP, giống lệnh `ifconfig`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/CHECK/14.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/CHECK/14.png)






















