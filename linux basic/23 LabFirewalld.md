## **Lab Firewalld:**

Mô hình lab:
[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/Firewalld/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/Firewalld/1.png)

- Sử dụng firewalld:

	- Cả 2 client kết nối host-only

	- Cho phép PC1 và PC2 truy cập internet

	- Chặn tất cả các liên hệ giữa PC1 và PC2

	- Chặn truy cập vào website: baomoi.com

	- Máy ngoài internet có thể truy cập vào PC2 bằng IP cổng ngoài của node firewalld

**Thực hành**

- Máy firewall có 3 card mạng:
	- ens33 (kết nối internet): 192.168.220.19
	
	- ens38 (kết nối với PC1): 192.168.30.3

	- ens37 (kết nối với PC2): 192.168.230.2

- Máy PC1:
	- Máy có địa chỉ: 192.168.30.4

- Máy PC2:
	- Máy có địa chỉ: 192.168.230.3

**Cấu hình**	

**Cấu hình trên firewalld**: 

- Cấu hình cho phép Client truy cập tới máy chủ web nhưng không ra ngoài internet

	- Trên FirewallD, cấu hình cho phép forward các mạng bằng cách thêm module net.ipv4.ip_forward:

		- Sửa file `/etc/sysctl.conf`,thêm giá trị net.ipv4.ip_forward=1

- Hiện tại chưa cấu hình NAT nên mặc định Client sẽ không ra được internet

- Kiểm tra, Client Ping thành công tới WebSRV nhưng không ra được Internet.

- Cấu hình NAT cho phép ra được bên ngoài internet

```
firewalld-cmd --zone=external --change-interface=ens33
```

- Cấu hình **Direct Interface**, **Reject** các kết nối từ interface ens38(PC1) đến interface ens37 (PC2)

```
firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -i ens38 -o ens37 -j REJECT
```

- Chặn PC1 truy cập vào website: baomoi.com

```
firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -i ens38 -d 118.102.1.125 -j REJECT
```


  			

