# **Network interfaces**

 - Network interfaces là kênh kết nối giữa device và network. Về mặt vật lý, network interface chính là network interface card (NIC). Một hệ thống có thể có nhiều card mạng cùng hoạt động. Các card mạng có thể được lắp vào hoặc ngắt ra bất cứ lúc nào.
 - Để kiểm tra các card mạng đang hoạt động dùng lệnh `ifconfig` hoặc `ip addr`
 - Đối với RedHat, file cấu hình nằm trong file `/etc/sysconfig/network-scripts/`. Đối với Debian, file cấu hình nằm trong `/etc/network/interfaces`.
 - Cấu hình tĩnh trong Ubuntu,sửa file `/etc/network/interfaces` như sau:

 ```
 auto eth0
iface eth0 inet static

address 10.0.0.41
netmask 255.255.255.0
network 10.0.0.0
broadcast 10.0.0.255
gateway 10.0.0.1
dns-nameservers 10.0.0.1 8.8.8.8
dns-domain acme.com
dns-search acme.com
```
- Muốn để nhận ip từ dhcp server thì cấu hình như sau:

```
auto eth0
iface eth0 inet dhcp
```
# Routing table

- Lệnh `route -n` được sử dụng để xem hoặc chỉnh sửa bằng định tuyến IP, thêm, xóa hoặc thay đổi IP.

```
johnny@ubuntu:/etc/network/interfaces.d$ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.220.2   0.0.0.0         UG    0      0        0 ens33
192.168.220.0   0.0.0.0         255.255.255.0   U     0      0        0 ens33
```
 - Một số câu lệnh để thêm hoặc xóa các route trong bảng định tuyến

 ```
route add 192.168.0.110  gw 192.168.0.1
route delete 192.168.0.110  gw 192.168.0.1
route add -net 192.168.0.0 netmask 255.255.255.0 gw 192.168.60.0 ens33
route delete -net 192.168.0.0 netmask 255.255.255.0 gw 192.168.60.0 ens33
```


