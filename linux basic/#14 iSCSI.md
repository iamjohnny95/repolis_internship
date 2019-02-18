# **Chia sẻ bộ nhớ qua mạng với iSCSI**

## **1. iSCSI là gì**
- `iSCSI`  là internet Small Computer System Interface: dựa trên giao thức mạng internet (IP) để kết nối các cơ sở dữ liệu. Nói một cách đơn giản nhất, iSCSI sẽ giúp tạo 1 ổ cứng Local trong máy tính của bạn với mọi chức năng y như 1 ổ cứng gắn trong máy tính vậy. Chỉ khác ở chỗ dung lượng thực tế nằm trên NAS và do NAS(Network Attached Storage) quản lý.

- **iSCSI có nhiều điểm nổi bật như:**
  - Chi phí rẻ hơn nhiều so với Fiber Channel SAN
  - Tạo và quản lý được nhiều ổ cứng cho nhiều máy tính nội-ngoại mạng(VPN).
  - Gián tiếp mở rộng dung lượng lưu trữ cho các máy tính nội-ngoại mạng(VPN).
  - Cài VMware trên ổ cứng iSCSI hoặc cài phần mềm từ xa.
  - Hiển thị y hệt ổ cứng trong máy, thân thiện với người dùng phổ thông.
  - Bảo mật cao bằng mật khẩu.
  - Kết nối rất nhanh, không cần qua nhiều bước.
  - Thích hợp cho doanh nghiệp quản lý dữ liệu của máy nhân viên.

 ## **2. Các thành phần của iSCSI**
 - Gồm 2 thành phần chính:
  - **iSCSI Target**
  - **iSCSI Initator**

 - **iSCSI_Target:**  Server iSCSI Target thường sẽ là một máy chủ lưu trữ (storage) có thể là hệ thống NAS chẳng hạn. Từ máy chủ iSCSI Target sẽ tiếp nhận các request gửi từ iSCSI Initiator gửi đến và gửi trả dữ liệu trở về. Trên được dùng để chia sẻ ổ đĩa lưu trữ iSCSI với phía iSCSI Client.

 - **iSCSI Initiator:** là thiết bị client trong kiến trúc hệ thống lưu trữ qua mạng. iSCSI Initiator sẽ kết nối đến máy chủ iSCSI Target và truyền tải các lệnh SCSI thông qua đường truyền mạng TCP/IP . iSCSI Initiator có thể được khởi chạy từ chương trình phần mềm trên OS hoặc phần cứng thiết bị hỗ trợ iSCSI.

 ## **3 Cấu hình iSCSI Target & Initiator trên Centos 7**

 - Chuẩn bị :

  - Máy server: 192.168.220.13
  - Máy client: 192.168.220.14

Cả 2 máy sử dụng hệ điều hành CentOS 7

**1. Tạo LVM cho máy server**
- Add thêm ổ đĩa 10G. 
- Ở đây, chúng tôi sẽ tạo 5GB đĩa LVM trên máy chủ đích để sử dụng làm bộ nhớ chia sẻ cho khách hàng. Hãy liệt kê các đĩa có sẵn được gắn vào máy chủ đích bằng cách sử dụng lệnh dưới đây. Nếu bạn muốn sử dụng toàn bộ đĩa cho LVM, sau đó bỏ qua bước phân vùng đĩa.

**2. Tạo Partition mới bằng công cụ fdisk và chọn kiểu phân vùng LVM**

- Chúng ta đứng ở máy Server:

```
[root@localhost ~]# fdisk -l

Disk /dev/sdh: 10.7 GB, 10737418240 bytes, 20971520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

- Từ đầu ra ở trên, bạn có thể thấy rằng hệ thống của tôi có 10GB đĩa (/dev/sdh). Chúng ta sẽ tạo một phân vùng 5GB trên đĩa và sẽ sử dụng nó cho LVM 

```
[root@target ~]#fdisk /dev/sdh
Welcome to fdisk (util-linux 2.23.2).
 
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.
 
Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0xd0165926.
 
Command (m for help): n ----> Phân vùng mới
Partition type:
p primary (0 primary, 0 extended, 4 free)
e extended
Select (default p): p ----> Phân vùng primary
Partition number (1-4, default 1): 1 ----> Số phân vùng
First sector (2048-20971519, default 2048): Enter
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519): <strong>+5G Nhập vào size</strong>
Partition 1 of type Linux and of size 5 GiB is set
 
Command (m for help): t  --->Thay đổi label
Selected partition 1
Hex code (type L to list all codes): 8e ---> Thay đổi thành LVN label
Changed type of partition 'Linux' to 'Linux LVM'
 
Command (m for help): w ---> Lưu lại
The partition table has been altered!
 
Calling ioctl() to re-read partition table.
Syncing disks.
```

- Tạo một phân vùng với LVM /dev/sdh1 (thay thế /dev/sdh1 bằng tên đĩa của bạn)

```
[root@target ~]# pvcreate /dev/sdh1
  Physical volume "/dev/sdh1" successfully created
[root@target ~]# vgcreate vg_iscsi /dev/sdh1
  Volume group "vg_iscsi" successfully created
[root@target ~]# lvcreate -l 100%FREE -n lv_iscsi vg_iscsi
  Logical volume "lv_iscsi" created
 ```
**3. Cấu hình iSCSI Target**

- Ở đây, mình sẽ cấu hình iSCSI mà không cần xác thực CHAP. Cài đặt gói targetcli trên máy chủ.

```
[root@target ~]# yum install targetcli -y
```

Khi bạn đã cài đặt xong, hãy nhập lệnh dưới đây để CLI iSCSI cho một dấu nhắc tương tác.

```
[root@localhost ~]# targetcli
```

- Bây giờ sử dụng một khối lượng hợp lý hiện có (/dev/vg_iscsi/lv_iscsi) như là một kho lưu trữ kiểu khối cho đối tượng lưu trữ scsi_disk1_server

```
/> cd backstores/
 /backstores> block/ create scsi_disk1_server /dev/vg_iscsi/lv_iscsi
Created block storage object scsi_disk1_server using /dev/vg_iscsi/lv_iscsi.
```
- Tạo target

```
/backstores> block/ cd /iscsi
/iscsi>
/iscsi> create iqn.2016-02.local.cloudzone.target:disk1
Created target iqn.2016-02.local.cloudzone.target:disk1.
Created TPG 1.
Global pref auto_add_default_portal=true
Created default portal listening on all IPs (0.0.0.0), port 3260.
/iscsi>

```

Tạo ACL cho máy khách (Đó là IQN mà Initiator sử dụng để kết nối).

```
/iscsi> cd /iscsi/iqn.2016-02.local.cloudzone.target:disk1/tpg1/acls
/iscsi/iqn.20...sk1/tpg1/acls>
/iscsi/iqn.20...sk1/tpg1/acls>  create iqn.2016-02.local.cloudzone.target:initiator1initiator2
Created Node ACL for iqn.2016-02.local.cloudzone.target:initiator1initiator2
```

Tạo LUN dưới target. LUN nên sử dụng đối tượng lưu trữ sao lưu được đề cập trước đây có tên “scsi_disk1_server“.

```
/iscsi/iqn.20...sk1/tpg1/acls>cd /iscsi/iqn.2016-02.local.cloudzone.target:disk1/tpg1/luns
/iscsi/iqn.20...sk1/tpg1/luns> create /backstores/block/scsi_disk1_server
Created LUN 0.
Created LUN 0->0 mapping in node ACL iqn.2016-02.local.cloudzone.target:initiator1initiator2
/iscsi/iqn.20...sk1/tpg1/luns>
```
- Xác minh cấu hình máy chủ đích 

```
/>  ls
o- / ..................................................................... [...]
  o- backstores .......................................................... [...]
  | o- block .............................................. [Storage Objects: 1]
  | | o- scsi_disk1_server  [/dev/vg_iscsi/lv_iscsi (5.0GiB) write-thru activated]
  | |   o- alua ............................................... [ALUA Groups: 1]
  | |     o- default_tg_pt_gp ................... [ALUA state: Active/optimized]
  | o- fileio ............................................. [Storage Objects: 0]
  | o- pscsi .............................................. [Storage Objects: 0]
  | o- ramdisk ............................................ [Storage Objects: 0]
  o- iscsi ........................................................ [Targets: 1]
  | o- iqn.2016-02.local.cloudzone.target:disk1 ...................... [TPGs: 1]
  |   o- tpg1 ........................................... [no-gen-acls, no-auth]
  |     o- acls ...................................................... [ACLs: 1]
  |     | o- iqn.2016-02.local.cloudzone.target:initiator1initiator2  [Mapped LUNs: 1]
  |     |   o- mapped_lun0 ................. [lun0 block/scsi_disk1_server (rw)]
  |     o- luns ...................................................... [LUNs: 1]
  |     | o- lun0  [block/scsi_disk1_server (/dev/vg_iscsi/lv_iscsi) (default_tg_pt_gp)]
  |     o- portals ................................................ [Portals: 1]
  |       o- 0.0.0.0:3260 ................................................. [OK]
  o- loopback ..................................................... [Targets: 0]
/> saveconfig
Configuration saved to /etc/target/saveconfig.json
/>
```

Bật và khởi động lại dịch vụ target.

```
[root@target ~]# systemctl enable target.service
ln -s '/usr/lib/systemd/system/target.service' '/etc/systemd/system/multi-user.target.wants/target.service'
[root@target ~]# systemctl enable target.service
```
Cấu hình tường lửa để cho phép lưu lượng iSCSI.
```
[root@localhost ~]# firewall-cmd --permanent --add-port=3260/tcp
success
[root@localhost ~]# firewall-cmd --reload
success
```
**4. Cấu hình Initiator**

- Bây giờ cấu hình node để sử dụng target tạo làm bộ nhớ. Cài đặt gói dưới đây trên máy Initiator (node1).

```
yum install iscsi-initiator-utils -y
```
- Chỉnh sửa tệp  initiatorname.iscsi.

```
InitiatorName=iqn.2016-02.local.cloudzone.target:initiator1initiator2
```
Sử dụng lệnh để target

```
[root@localhost ~]# iscsiadm -m discovery -t st -p 192.168.220.13
192.168.220.13:3260,1 iqn.2016-02.local.cloudzone.target:disk1
```

Khởi động lại và kích hoạt dịch vụ khởi tạo.

```
iscsiadm -m node -T iqn.2016-02.local.cloudzone.target:disk1 -p 
iscsiadm -m node -T iqn.2016-02.local.cloudzone.target:disk1 -p 
```

Đăng nhập đến Target

```
[root@localhost ~]# iscsiadm -m node -T iqn.2016-02.local.cloudzone.target:disk1 -p 192.168.220.13 -l
Logging in to [iface: default, target: iqn.2016-02.local.cloudzone.target:disk1, portal: 192.168.220.13,3260] (multiple)
Login to [iface: default, target: iqn.2016-02.local.cloudzone.target:disk1, portal: 192.168.220.13,3260] successful.
```

**5. Tạo hệ thống tập tin trên đĩa ISCSI**

Định dạng đĩa mới 

```
[root@initiator ~]# mkfs.xfs /dev/sdb
meta-data=/dev/sdb               isize=256    agcount=8, agsize=163712 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=0
data     =                       bsize=4096   blocks=1309696, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=0
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```

Mount đĩa

```
[root@initiator ~]# mount /dev/sdb /mnt
```

Xác minh đĩa được gắn kết bằng cách sử dụng lệnh dưới đây.

```
[root@initiator ~]# df -hT
Filesystem              Type      Size  Used Avail Use% Mounted on
/dev/mapper/centos-root xfs        18G  851M   17G   5% /
devtmpfs                devtmpfs  908M     0  908M   0% /dev
tmpfs                   tmpfs     914M     0  914M   0% /dev/shm
tmpfs                   tmpfs     914M  8.6M  905M   1% /run
tmpfs                   tmpfs     914M     0  914M   0% /sys/fs/cgroup
/dev/sda1               xfs       497M   96M  401M  20% /boot
<strong>/dev/sdb                xfs       5.0G   33M  5.0G   1% /mnt
</strong>
```

**6. Lưu trữ iSCSI tự động**

```
[root@localhost ~]# blkid /dev/sdb
/dev/sdb: UUID="36c43dfc-d09b-4dfd-af11-07c92df5a0de" TYPE="xfs"
```
Sau đó lưu vào file /etc/fstab



