LAB kết hợp DNS vói webserver

- Yêu cầu 1 công ty có 2 web trên cùng 1 dải địa chỉ 192.168.220.16 

	- website 1: abc.local

	- website 2: xyz.local

- Cấu hình vitural host trong đường dẫn 

`vi /etc/httpd/conf/httd.conf`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/13.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/13.png)


**Cấu hình DNS**

- Cấu hình DNS trong thư mục `vi /etc/named.conf`


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/14.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/14.png)


- Cấu hình đường dẫn đến các zone

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/15.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/15.png)



- Cấu hình zone trong thư mục `var/named`

- File `abc.net`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/16.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/16.png)

- File `xyz.net`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/17.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/17.png)

- File zone nghịch cba.net

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/18.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/18.png)

Cấu hình rule trong tường lửa cho phép truy cập từ bên ngoài vào bằng cổng 53 và truy cập địa chỉ web `abc.local` và `xyz.local`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/19.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/19.png)

- Sau khi cấu hình xong thì khởi động lại dịch vụ rồi kiểm tra

- ping kiểm tra cấu hình của 2 site `xyz.local` và `abc.local`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/20.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/20.png)



