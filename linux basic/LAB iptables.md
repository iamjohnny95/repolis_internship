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





