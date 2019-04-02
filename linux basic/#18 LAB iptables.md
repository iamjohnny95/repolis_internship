LAB iptables

## **Lab 1**

**Mô hình**:

- Máy PC2 chỉ có thể liên hệ tới PC 1 trên cổng 22

- Máy PC1 có thể ping tới Server DC

- Server DC có thể liên hệ tới PC1 trên cổng 22 thông qua địa chỉ IP Public của Server nội bộ

- SERVER DC: 15.0.22.50

- FIREWALL: eth0 nối với SERVER DC 15.0.22.51/16
			
			eth2 nối với CLIENT 192.168.20.10/24

- CLIENT: ens33 nối với firewall 192.168.20.20/24

		  ens37 nối client2 192.168.30.20/24

**Cấu hình**:

***Trên firewall***:

- Sửa file: vi /etc/sysctl.conf để enable routing 

```
net.ipv4.ip_forward = 1
```

- Sử file cấu hình iptables:

- vi /etc/sysconfig/iptables

**Nat** 

```
*nat
:PREROUTING ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A PREROUTING -d 15.0.22.51/32 -p tcp -m tcp --dport 22 -j DNAT --to-destination 192.168.20.20
-A POSTROUTING -s 192.168.20.0/24 -d 15.0.22.50/16 -p tcp -j SNAT --to-source 15.0.22.0
COMMIT
```

- Cấu hình xong restart lại dịch vụ


***Trên Client***

- Cấu hình command:

```
iptables -t filter -A INPUT -i ens37 -p tcp --drop 22 -j ACCEPT 

iptables -t filter -A INPUT -i DROP 
```

**Kiểm tra cấu hình**



[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/2.png)


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/3.png)


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/4.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/4.png)



## Lab2 :

**Mô hình**:

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/6.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/6.png)


- Máy firewall có 3 card mạng: 

	- Card nối mạng eth1: 192.168.220.16

	- Card nối webserver eth0: 15.0.22.51

	- Card nối client eth2 : 192.168.20.10


- Máy client có 1 card mạng:

	- Card nối với client có dải địa chỉ: 192.168.20.20


- Máy webserver có 1 card mạng:

	- Card nối với firewall có dải địa chỉ: 15.0.22.50

**Yêu cầu**

- Tất cả cấu hình trên firewall 

- Cả client và web chỉ có kết nối host-only (2 dải khác nhau)

- Client chỉ có thể ping vs telnet port 80 tới máy chủ web, không được phép bỏ ra ngoài internet

- Chặn ssh từ client tới máy chủ web

- Máy chủ web có thể ra ngoài internet, ping được tới máy client 

**Cấu hình**

**Trên Firewall**

**Cấu hình các rule kết nối mạng bên trong**

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/7.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/7.png)

- Test yêu cầu 


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/8.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/8.png)

- Client chỉ có thể ping và web nhưng không ping ra ngoài internet

- Câu lệnh sử dụng:
	- iptables -A FORWARD -s 192.168.20.20 -i eth2 -p icmp -d 15.0.22.50 -j ACCEPT

	- iptables -A FORWARD -s 192.168.20.20 -i eth2 -o eth1 -j DROP

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/9.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/9.png)

- Client telnet cổng 80 trên web

- Câu lệnh sử dụng:

	- iptables -A FORWARD -s 192.168.20.20 -i eth2 -p tcp -m tcp --dport 80 -d 15.0.22.50 -j ACCEPT


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/10.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/10.png)

- Cấm kết nối SSH từ client đến web

- Câu lệnh sử dụng 

	- iptables -A FORWARD -s 192.168.20.20 -i eth2 -p tcp -m  tcp --dport 22 -d 15.0.22.50 -j DROP


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/11.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/11.png)

- Máy chủ web có thể đi được ra ngoài internet và có thể ping được với máy client

- Câu lệnh sử dụng:

	- iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE

	- iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

**Cấu hình trên web**

- Cấu hình đường dẫn website trong thư mục

```
vi /var/www/html/website/
```

- Cấu hình http trong đường dẫn thư mục

```
vi /etc/httpd/conf/httpd.conf
```
- Cấu hình DocumentRoot và Directory trỏ đến đường dẫn của web vừa lập

- Kiểm tra

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/12.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/12.png)


















