## **Firewalld**

Trên các Distro của Linux hầu như sử dụng netfilter bên trong kernel Linux để truy cập vào các gói dữ liệu qua network interface, cung cấp giao diện, thao tác với các gói tin để xây dựng tường lửa Để cung cấp giao diện cho người dùng, các bản Distro sử dụng IPTABLESđể làm móc nối Netfiltercho xây dựng tường lửa

.Trên CentOS 7 , *firewallD* thay thế iptables services, nhưng vẫn giao tiếp tiếp Netfilter thông qua iptable command

FirewallD được viết bằng ngôn ngữ Pyhon, cung cấp một tường lửa động trên Centos. Công cụ cho phép xác định độ tin cậy của gói tin qua các zone. FirewallD hỗ trợ IPv4, IPv6, ethernet bridges và IP sets	. Trong FirewallD, các quy tắc được cấu hình thời gian hiệu lực Runtime hoặc Permanent.

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/iptables/21.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/iptables/21.png)

**Các khái niệm trong firewallD**

**Zone**

- Trong FirewallD, zone là một nhóm các quy tắc nhằm chỉ ra những luồng dữ liệu được cho phép, dựa trên mức độ tin tưởng của điểm xuất phát luồng dữ liệu đó trong hệ thống mạng. Để sử dụng, bạn có thể lựa chọn zone mặc định ,thiết lập các quy tắc trong zone hay chỉ định giao diện mạng (Network Interface) để quy định được hành vi cho phép. 

	- **Drop**: ít tin cậy nhất- toàn bộ các kết nối đến sẽ bị từ chối mà không phản hồi, chỉ có phép duy nhất kết nối đi ra

	- **Block**: tương tự như drop nhưng các kết nối đến bị từ chối và phản hồi bằng tin nhắn từ icmp-host-prohibited hoặc (icmp6-host-prohibited)

	- **Public**: đại diện cho mạng công cộng, không đáng tin cậy. Các máy tính/services khác không được tin tưởng trong hệ thống nhưng vẫn cho phép các kết nối đến trên cơ sở chọn từng trường hợp cụ thể. 

	- **external**: hệ thống mạng bên ngoài trong trường hợp bạn sử dụng tường lửa làm gateway, được cấu hình giả lập NAT để giữ bảo mật mạng nội bộ mà vẫn có thể truy cập.

	- **internal**: đối lập với external zone, sử dụng phần nội bộ của gateway. Các máy tính/services thuộc zone này thì khá đáng tin cậy. 

	- **dmz**: sủ dụng cho các máy tính/service trong khu vực dmz - cách ly không cho phép truy cập vào phần còn lại của hệ thống mạng, chỉ cho phép một số kết nối nhất định. 

	- **work**: sử dụng trong công việc, tin tưởng hầu hết các máy tính và một vài services được cho phép hoạt động. 

	- **home**: môi trường gia đình - tin tưởng hầu hết các máy tính và một vài services được cho phép hoạt động. 

	- **trusted**: đáng tin cậy nhất- tin tưởng toàn bộ thiết bị trong hệ thống.


**Cài đặt và quản lý FirewallD**

- Để bắt đầu dịch vụ và cho phép FirewallD khi khởi động:

```
systemctl start firewalld
systemctl enable firewalld
```

- Để dừng và vô hiệu hóa nó:

```
systemctl stop firewalld
systemctl disable firewalld
```

- Kiểm tra tình trạng tường lửa. Đầu ra phải thể hiện tình trạng chạy hay không chạy 

```
firewall-cmd --state
```

- Để xem trạng thái của daemon FirewallD:

```
 systemctl status firewalld
 ```

 - Để reload cấu hình tường lửa:

 ```
 firewall-cmd --reload
 ```

 **Cấu hình FirewallD**

 - Firewalld được cấu hình với các tệp tin XML

 - Cấu hình tệp tin đang nắm trong 2 thư mục:

 - /usr/lib/FirewallD giữ cấu hình mặc định như default zones và các dịch vụ thông thường. Tránh cập nhật chúng bởi vì các tệp tin sẽ bị ghi 

 đè bởi mỗi lần cập nhật gói firewalld 

 - /etc/firewalld giữ các tệp tin cấu hình hệ thống. Những tệp tin này sẽ ghi đè lên tệp tin cấu hình mặc định.

 **Thiết lập cấu hình**

 - Firewalld sử dụng hai thiết lập cấu hình: **Runtime** và **Permanent**. Thay đổi cấu hình **Runtime** không được lưu giữ khi khởi động lại hoặc khi khởi động lại FirewallD trong khi thay đổi **Permanent** không được áp dụng khi hệ thống đang chạy.

 - Theo mặc định, lệnh firewall-cmd áp dụng cho runtime nhưng cách sử dụng cờ --**permanent** sẽ thiết lập một cấu hình ổn định. Để thêm và kích hoạt một quy tắc cố định, bạn có thể sử dụng một hoặc 2 phương pháp. Thêm quy tắc cho cả 2 thiết lập `Runtime` và `Permanent`:

 ```
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=http
```

- Thêm các quy tắc đến thiết lập **Permanent** và khởi động lại các FirewallD.

```
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload
```

- Lệnh khởi động sẽ drop tất cả các thiết lập **Runtime** và áp dụng các thiết lập **permanent**. Bởi vì firewalld quản lý ruleset động, nó sẽ không phá vỡ một kết nối và phiên hiện tại. 

**Firewall Zones** 

- Show các zone trên server:

```
firewall-cmd--getzones
```

- Show zone mặc định, thường là zone Public

```
firewall-cmd--get-default-zone
```

- Show các zone đang được Active trên Server

```
firewall-cmd--get-active-zone
```

- Set zone mặc định từ Public sang External 

```
firewall-cmd--set-default-zone=external
```

- Show các rules trong zone mặc định 

```
firewall-cmd--list-all
```

- Show các rules trên một zone cụ thể, ví dụ zone external

```
firewall-cmd--list-all--zone=external
```

**Rules cho Port hoặc Service**

- Show các service trong zones

```
firewall-cmd--list-services--zone=external
```

- Show các port trong zones

```
firewall-cmd--list-ports--zone=external
```

- Show các Service đã được định nghĩa trong firewalld các file thông tin service nằm trong thư mục `/usr/lib/firewalld/services/`

```
firewall-cmd--get-services
```

- Cấu hình tạm thời cho phép client kết nối tới service HTTP (mặc định 80/TCP) trên server. Reload FirewallD hoặc Restart Service Rules sẽ mất hiệu lực ( Runtime Rules)

```
firewall-cmd--zone=public--add-service=http 
firewall-cmd--zone=public--list-services
```

- Cấu hình tạm thời cho phép client kết nối tới port 80/TCP trên server. Reload Firewalld hoặc restart service rules sẽ mất hiệu lực (Runtime Rules). Nếu đã cấu hình Allow Service HTTP thì không cần cấu hình thêm port 80 và ngược lại 

```
firewall-cmd --zone=public --add-port=80/TCP
firewall-cmd --zone=public --list-ports
```

- Xóa các rules đã cấu hình

```
firewall-cmd --zone=public --remove-port=80/TCP
firewall-cmd --zone=public --remove-service=http
firewall-cmd --zone=public --list-ports
```

- Thêm Rules cho phép Service , Reload để có hiệu lực, không bị mất khi restart server

```
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload
firewall-cmd --zone=public --list-services
```

- Thêm Rules cho phép Port , Reload để có hiệu lực, không bị mất khi restart server

```
firewall-cmd --zone=public --add-port=80/TCP --permanent
firewall-cmd --reload
firewall-cmd --zone=public --list-services
```

- Thêm theo Range Port

```
firewall-cmd --zone=public --add-port=4990-5000/tcp
firewall-cmd --zone=public --add-port=4990-5000/tcp --permanent
```

**Thay đổi zone cho interface**

- Để quản lý tốt server cần gán thêm interface tương ứng vào các zone trên firewall cho phù hợp với mục đích sử dụng.

**Thêm interface vào zone**

- Cho phép SSH vào interface zone

``` 
firewall-cmd --zone=internal --add-interface=ens160 -permanent 
firewall-cmd --zone=internal --add-port=22/tcp --permanent
```

- Cho phép http vào external zone

```
firewall-cmd --zone=external --add-interface=ens192 --permanent
firewall-cmd --zone=external --add-service=http --permanent
```

- Apply cấu hình:

```
firewall-cmd --reload
firewall-cmd --zone=internal --list-all
firewall-cmd --zone=external --list-all
```

- Xóa interface khỏi zone

```
firewall-cmd --zone=internal --remove-interfaces=ens160
firewall-cmd --reload
firewall-cmd --zone=internal --list-interfaces
```

**Cấu hình Rich-Rules**

- Trong một số trường hợp để hạn chế truy cập, ta cần định nghĩa ra các Rich rules

- Cho phép một dải IP hoặc nhiều dải ip truy cập dịch vụ

	- Tạo list danh sách IP đặt tên là white-list

```
sudo firewall-cmd --perman --new-ipset=white-list --type=hash:ip/net
 
 ```

 - Thêm các IP hoặc dải mạng vào trong list `whitelist`

```
# ADD IP
sudo firewall-cmd --perman --ipset=white-list --add-entry=10.0.0.22/32

# ADD SUBNET
sudo firewall-cmd --perman --ipset=white-list --add-entry=10.0.0.0/24

```

- Hoặc ta có thể tạo một file text chứa list danh sách và nhập vào như sau 

```
# Creat List IP
cat > iplist.txt <<EOL
192.168.0.2
192.168.0.3
192.168.1.0/24
192.168.2.254
EOL
# Import to FirewallD
firewall-cmd --permanent --ipset=test --add-entries-from-file=iplist.txt
```

- Cấu hình rich rules:

```
sudo firewall-cmd --perman --add-rich-rule='rule source ipset=white-list port protocol="tcp" port="11211" accept'
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
 
# Show all entry IP range in list
sudo firewall-cmd --ipset=white-list --get-entries
```

- Xóa bỏ rules đã cấu hình 

```
# Delete list 
sudo firewall-cmd --perman --del-ipset=white-list --type=hash:ip
 
# Delete an entry inlist
sudo firewall-cmd --perman --ipset=white-list --remove-entry=10.0.0.22
 
# Delete multi entry in list
firewall-cmd --permanent --ipset=test --remove-entries-from-file=iplist.txt
 
# Remove rules
sudo firewall-cmd --perman --remove-rich-rule='rule source ipset=white-list port protocol="tcp" port="2022" accept'
 
# Check
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```




