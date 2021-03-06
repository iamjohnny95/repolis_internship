**LVM là gì:**
**1.1 Khái niệm, Tổng quan**

LVM (Logical Volume Manager) là một kỹ thuật cho phép tạo ra các không gian ổ đĩa ảo từ ổ đĩa cứng để có thể thay đổi kích thước dễ dàng hơn

- Một số ứng dụng của LVM:

	- Quản lý một lượng lớn ổ đĩa một cách dễ dàng.

	- Điều chỉnh phân vùng ổ cứng một cách linh động 

	- Backup hệ thống bằng cách snapshot các phân vùng ổ cứng (real-time)

	- Migrate dữ liệu dễ dàng.


**1.2 Vai trò của LVM**

LVM là kỹ thuật quản lý việc thay đổi kích thước lưu trữ của ổ cứng 
  - Không để hệ thống bị gián đoạn hoạt động 
  - Không làm hỏng dịch vụ 
  - Có thể kết hợp Hot Swapping (phương pháp thay thế nóng bên trong máy tính)

**1.3 Các thành phần trong LVM**

**Mô hình các thành phần trong LVM**


 [[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/1.png)



**Hard drives -Drives**
Thiết bị lưu trữ dữ liệu, ví dụ như trong linux là `/dev/sda/`

**Partition**
Partitions là các phân vùng của Hard drivers, mỗi Hard drivers có 4 partition, trong đó partition bao gồm 2 loại là primary partition và extended partition

	- **Primary partition:**

	- Phân vùng chính, có thể khởi động

	- Mỗi đĩa cứng có thể có tối đa 4 phân vùng này 

	- **Extended partition:**

	- Phân vùng mở rộng có thể tạo ra bộ nhớ luân lý 

**Physical Volume**
- Là một cách gọi khác của partition trong kỹ thuật LVM, nó là những thành phần cơ bản được sử dụng bởi LVM. Một Physical Volume không thể mở rộng ra ngoài phạm vi một ổ đĩa. 

- Chúng ta có thể kết hợp nhiều Physical Volume thành Volume Groups

**Volume Groups**
- Nhiều Physical Volume trên những ổ đĩa khác nhau được kết hợp lại thành một Volume Group

- Volume Group được sử dụng để tạo ra các Logical Volume, trong đó người dùng có thể tạo, thay đổi kích thước, lưu trữ, gỡ bỏ và sử dụng.

- Một điểm cần lưu ý là boot loader không thể đọc /boot khi nó nằm trên Logical Volume Group. Do đó không thể sử dụng kỹ thuật LVM với /boot mount point

**Logical Volume**

- Volume Group được chia nhỏ thành nhiều Logical Volume, mỗi Logical Volume có ý nghĩa tương tự như partition. Nó được dùng cho các mount point và được format với những định dạng khác nhau như ext2, ext3, ext4,...

- Khi dung lượng của Logical Volume được sử dụng hết ta có thể đưa thêm ổ đĩa mới bổ sung cho Volume Group và do đó tăng được dung lượng của Logical Volume

- Ví dụ bạn có 4 ổ đĩa mỗi ổ 5GB khi bạn kết hợp nó lại thành 1 volume group 20GB, và bạn có thể tạo ra 2 logical volumes mỗi disk 10GB

**File Systems**

	-Tổ chức và kiểm soát các tập tin

	- Được lưu trữ trên ổ đĩa cho phép truy cập nhanh chóng và an toàn

	- Sắp xếp dữ liệu trên đĩa cứng mọi máy tính

	- Quản lý vị trí vật lý của mọi thành phần dữ liệu

**Một số tính năng cơ bản của Logical Volume**

- Di chuyển LV giữa các PV khác nhau 

- Thay đổi kích thước của VG online bằng cách gắn thêm hoặc tháo bớt PV.

- Thay đổi kích thước của LV bằng cách thay đổi số lượng extent của PV này.

- Tạo snapshot của các LV (giữ nguyên toàn bộ trạng thái của LV vào thời điểm đó).



## **Hướng dẫn sử dụng LVM**

**2.1 Chuẩn bị**

	- Tạo máy ảo trên vmware Workstation trên hệ điều hành CentOS 6

	- Add thêm một số ổ cứng vào máy ảo 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/2.png)


**2.2 Tạo Logical Volume trên LVM**

**B1.Kiểm tra các Hard Drives có trên hệ thống**

Bạn có thể kiểm tra xem có những Hard Drives nào trên hệ thống bằng cách sử dụng câu lệnh `lsblk`

`#lsblk`

 [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/3.png)


Trong đó sdj, sdk, sdh,là các Hard Drives mà mình mới thêm vào

**B2.Tạo partition**

- Từ các Hard Drivers trên hệ thống, bạn tạo các partition. Ở đây, Ở đây, từ sdh, mình tạo các partition bằng cách sử dụng lệnh sau 

`fdisk /dev/sdh`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/4.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/4.png)

	- Trong đó bạn chọn `n` để bắt đầu tạo partition

	- Bạn chọn `p` để tạo partition primary

	- Bạn chọn `1` để tạo partition primary 1

	- Tại `First sector (2048-20971519, default 2048)` bạn để mặc định

	- Tại `Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519)` bạn chọn `+1G` để partition bạn tạo ra có dung lượng 1 G

	- Bạn chọn `w` để lưu lại và thoát

- Tiếp theo thay đổi định dạng của partition vừa mới tạo thành LVM

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/5.png)


	- Bạn vào `fdisk /dev/sdh`

	- Bạn chọn `t` để thay đổi định dạng partition

	- Bạn chọn `8e` để đổi thành LVM

- Tương tự tạo thêm các partition primary từ sdh


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/6.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/6.png)


Tạo các partition primary từ `sdj` bằng lệnh `fdisk /dev/sdj`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/7.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/7.png)

**B3. Tạo Physical Volume**

Tạo các Physical Volume là `/dev/sdh1` và `/dev/sdj1` bằng các lệnh sau:

`# pvcreate /dev/sdh1`

`# pvcreate /dev/sdj1`

Bạn có thể kiểm tra các Physical Volume bằng câu lệnh `pvs`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/8.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/8.png)


**B4. Tạo Volume Group**

- Tiếp theo, mình sẽ nhóm các Physical Volume thành 1 Volume Group bằng cách sử dụng câu lệnh sau:

`# vgcreate vg-demo1 /dev/sdh1 /dev/sdj1`

Trong đó `vg-demo1` là tên của Volume Group

Có thể sử dụng câu lệnh sau để kiểm tra lại các Volume Group đã tạo

`# vgs`

`# vgdisplay`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/9.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/9.png)


**B5. Tạo Logical Volume**

- Từ một Volume Group, chúng ta có thể tạo ra các Logical Volume bằng cách sử dụng lệnh sau:

`# lvcreate -L 1G -n lv-demo1 vg-demo1`

-L: Chỉ ra dung lượng của logical volume

-n: Chỉ ra tên của logical volume

Trong đó `lv-demo1` là tên Logical Volume, `vg-demo1` là Volume Group mà mình vừa tạo ở bước trước

Lưu ý là chúng ta có thể tạo nhiều Logical Volume từ 1 Volume Group

Có thể sử dụng câu lệnh sau để kiểm tra lại các Logical Volume đã tạo

`# lvs`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/10.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/10.png)


**B6. Định dạng Logical Volume**

- Để format các Logical Volume thành các định dạng như ext2, ext3, ext4, ta có thể làm như sau:

` mkfs.ext4 /dev/vg-demo1/lv-demo1`

**B7. Mount và sử dụng**

- Trong bài lab này, mình sẽ tạo ra một thư mục để mount Logical Volume đã tạo vào thư mục đó

`# mkdir demo1`

Tiến hành mount logical volume `lv-demo1` vào thư mục `demo1` như sau:

`# mount /dev/vg-demo1/lv-demo1 demo1`

Kiểm tra lại dung lượng của thư mục đã được mount:

`# df -h`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/11.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/11.png)


## **2.3 Thay đổi dung lượng Logical Volume trên LVM**

- Ở phần trước, mình đã tiến hành tạo Logical Volume trong LVM. Ở phần này, chúng ta sẽ tìm hiểu làm thế nào để có thể thay đổi dung lượng của 1 Logical Volume đã được tạo ở phần trước.

Trước khi thay đổi dung lượng, các bạn cần phải kiểm tra các thông tin hiện có:

`# vgs`

`# lvs`

`# pvs`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/12.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/12.png)


Ở đây, mình đã tạo được Logical Volume là lv-demo1, và giả sử Logical Volume này dung lượng đã đầy và chúng ta cần tăng kích thước của nó.

Logical Volume này thuộc Volume Group vg-demo1, để tăng kích thước, bước đầu tiên phải kiểm tra xem Volume Group còn dư dung lượng để kéo giãn Logical Volume không. Logical Volume thuộc 1 Volume Group nhất định, Volume Group đã cấp phát hết thì Logical Volume cũng không thể tăng dung lượng được. Để kiểm tra, ta dùng lệnh sau:

`# vgdisplay`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/13.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/13.png)


Volume Group ở đây vẫn còn dung lượng để cấp phát, ta có thể nhận thấy điều này qua 2 trường thông tin là VG Status resizable và Free PE / Size 510 / 1.99 GiB với dung lượng Free là 510\*4 = 2040 Mb

- Để tăng kích thước Logical Volume ta sử dụng câu lệnh sau:

`# lvextend -L +50M /dev/vg-demo1/lv-demo1`

Với `-L` là tùy chọn để tăng kích thước

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/14.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/14.png)


Kiểm tra lại bằng cách dùng lệnh `# lvs`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/15.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/15.png)


Sau khi tăng kích thước cho Logical Volume thì Logical Volume đã được tăng nhưng file system trên volume này vẫn chưa thay đổi, bạn phải sử dụng lệnh sau để thay đổi:

`# resize2fs /dev/vg-demo1/lv-demo1`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/16.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/16.png)


- Để giảm kích thước của Logical Volume, trước hết các bạn phải umount Logical Volume mà mình muốn giảm

`# umount /dev/vg-demo1/lv-demo1`

Tiến hành giảm kích thước của Logical Volume

`# lvreduce -L 20M /dev/vg-demo1/lv-demo1`

Sau đó tiến hành format lại Logical Volume

`# mkfs.ext4 /dev/vg-demo1/lv-demo1`

Cuối cùng là mount lại Logical Volume

`# mount /dev/vg-demo1/lv-demo1 demo1`

Kiểm tra kết quả ta được như sau:

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/17.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/17.png)


## **2.4 Thay đổi dung lượng Volume Group trên LVM**

- Ở phần trước mình có thể tăng kích thước của Logical Volume nhưng với điều kiện Volume Group của Logical Volume đó còn dung lượng. Phần này chúng ta sẽ tìm hiểu xem làm thế nào có thể mở rộng thêm kích thước của Volume Group cũng như thu hồi dung lượng của nó.

- Việc thay đổi kích thước của Volume Group chính là việc nhóm thêm Physical Volume hay thu hồi Physical Volume ra khỏi Volume Group

- Trước tiên, các bạn cần kiểm tra lại các partition và Volume Group

`# vgs`

`# lsblk`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/18.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/18.png)


- Tiếp theo, nhóm thêm 1 partition vào Volume Group như sau:

`# vgextend /dev/vg-demo1 /dev/sdh2`    


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/19.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/19.png)


- Ở đây, muốn nhóm vào Volume Group phải là Physical Volume nên hệ thống đã tự động tạo cho mình Physical Volume và nhóm vào Volume Group.

- Chúng ta có thể cắt 1 Physical Volume ra khỏi Volume Group như sau:

`# vgreduce /dev/vg-demo1 /dev/sdb3`


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/20.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/20.png)



## **2.5 Xóa Logical Volume, Volume Group, Physical Volume**

**Xóa Logical Volumes**

Trước tiên ta phải Umount Logical Volume

`# umount /dev/vg-demo1/lv-demo1`

Sau đó tiến hành xóa Logical Volume bằng câu lệnh sau:

`# lvremove /dev/vg-demo1/lv-demo1`

**Xóa Volume Group**

Trước khi xóa Volume Group, chúng ta phải xóa Logical Volume

Xóa Volume Group bằng cách sử dụng lệnh sau:

`# vgremove /dev/vg-demo1`

Xóa Physical Volume

Cuối cùng là xóa Physical Volume:

`# pvremove /dev/sdb3`

- Vậy là mình đã hoàn thành một bài lab đơn giản về LVM.

## **LVM Migrating**

- LVM là một tính năng của LVM cho phép tạo ra một bản sao dữ liệu từ một Logical Volume này đến một ổ đĩa mới mà không làm mất dữ liệu hay xảy ra tình trạng downtime.

- User case: Khi có một ổ cứng cũ bị lỗi, bạn muốn thêm một ổ cứng mới gắn và di chuyển dữ liệu ổ cũ sang ổ này thì migrating là một lựa chọn tốt của LVM.

**Thực hành**

- Tạo một mirror volume với câu lệnh 

`lvcreate -L 1G -m 1 -n lv-mirror vg-demo1`

Lệnh này sẽ tạo ra một logical volume `lv-mirror` và một bản mirror của nó với tùy chọn `-m 1`

Tiếp theo tạo một thư mục để mount vào logical volume này và kiểm tra tính năng này:

```
mkfs.ext4 /dev/vg-demo1/lv-mirror 
mkdir demo2
mount /dev/vg-demo1/lv-mirror demo2
```

- Tạo một file trong thư mục mới tạo

```
cd demo2
echo "Hello World." >> greet.txt
```

- Kiểm tra thông tin về Logical Volume bằng lệnh sau:

```
[root@ipmac demo2]# lvs -a -o +devices
  Couldn't find device with uuid YP0Uh8-oHu4-a7Nv-Sz6J-mSOE-SqmL-Pfi0dK.
  Couldn't find device for segment belonging to VG3/LV1 while checking used and assumed devices.
  Couldn't find device with uuid Xzpm0g-NWTN-03XD-XmyV-KnXt-bDWW-DeBaQz.
  LV                   VG        Attr       LSize  Pool Origin Data%  Meta%  Move Log              Cpy%Sync Convert Devices
  LV1                  VG1       -wi-ao----  5.00g                                                                  /dev/sde(0)
  LV1                  VG2       -wi-ao----  5.00g                                                                  /dev/sdd(0)
  LV2                  VG2       -wi-ao----  3.00g                                                                  /dev/sdd(1280)
  LV1                  VG3       -wi-a---p- 10.00g                                                                  /dev/sdg(0)
  LV1                  VG3       -wi-a---p- 10.00g                                                                  unknown device(0)
  lv-demo1             vg-demo1  -wi-ao---- 20.00m                                                                  /dev/sdh1(0)
  lv-mirror            vg-demo1  mwi-aom---  1.00g                                [lv-mirror_mlog] 100.00           lv-mirror_mimage_0(0),lv-mirror_mimage_1(0)
  [lv-mirror_mimage_0] vg-demo1  iwi-aom---  1.00g                                                                  /dev/sdj1(0)
  [lv-mirror_mimage_1] vg-demo1  iwi-aom---  1.00g                                                                  /dev/sdh2(0)
  [lv-mirror_mlog]     vg-demo1  lwi-aom---  4.00m                                                                  /dev/sdh1(5)
  lv_root              vg_centos -wi-ao---- 37.57g                                                                  /dev/sda2(0)
  lv_swap              vg_centos -wi-ao----  1.94g                                                                  /dev/sda2(9618)
```
- Ta thấy được `lv-mirror` đang gắn với lv-mirror_rimage_0(0) và lv-mirror_rimage_1(0), mà lv-mirror_rimage_0(0) đang gắn với `/dev/sdb1`, lv-mirror_rimage_1(0) đang gắn với `/dev/sdb2`. Như vậy ta có thể thấy dữ liệu lưu trên Mirror Volume được lưu ở hai chỗ.

- Nếu muốn xóa một bản đi, ta sử dụng lệnh sau:

```
lvconvert -m 0 /dev/vg-demo1/lv-mirror /dev/sdh1
```

Kết quả:

```

[root@ipmac demo2]# lvs -a -o +devices
  Couldn't find device with uuid YP0Uh8-oHu4-a7Nv-Sz6J-mSOE-SqmL-Pfi0dK.
  Couldn't find device for segment belonging to VG3/LV1 while checking used and assumed devices.
  Couldn't find device with uuid Xzpm0g-NWTN-03XD-XmyV-KnXt-bDWW-DeBaQz.
  LV        VG        Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert Devi                                                                        ces
  LV1       VG1       -wi-ao----  5.00g                                                     /dev                                                                        /sde(0)
  LV1       VG2       -wi-ao----  5.00g                                                     /dev                                                                        /sdd(0)
  LV2       VG2       -wi-ao----  3.00g                                                     /dev                                                                        /sdd(1280)
  LV1       VG3       -wi-a---p- 10.00g                                                     /dev                                                                        /sdg(0)
  LV1       VG3       -wi-a---p- 10.00g                                                     unkn                                                                        own device(0)
  lv-demo1  vg-demo1  -wi-ao---- 20.00m                                                     /dev                                                                        /sdh1(0)
  lv-mirror vg-demo1  -wi-ao----  1.00g                                                     /dev                                                                        /sdj1(0)
  lv_root   vg_centos -wi-ao---- 37.57g                                                     /dev                                                                        /sda2(0)
  lv_swap   vg_centos -wi-ao----  1.94g                                                     /dev                                                                        /sda2(9618)
```

Kiểm tra lại nội dung file `greet.txt` lúc đầu đã tạo ta thấy không có gì thay đổi, dữ liệu vẫn còn nguyên.

## **LVM Snapshot**

**Snapshot LVM là gì**

- Snapshot là một tính năng của LVM cho phép một bản sao lưu của thời điểm hiện tại để backup cho sau này, ta có thể khôi phục lại thời điểm đã backup trước đó nếu cần.

**Thực hành**

- Ở đây, tôi sẽ tạo một bản snapshot cho Logical Volume `lv-demo1`. Sử dụng lệnh:

```
lvcreate -l 50 --snapshot -n lv-demo1-snapshot /dev/vg-demo1/lv-demo1
```

- Kiểm tra bằng lệnh `lvs` sẽ có thể xem được lệnh snapshot tạo ra.

- Vì Snapshot LVM cũng là một Logical Volume nên có thể xóa, tăng giảm kích thước như Logical Volume. Ví dụ nếu muốn xóa snapshot đi:

`lvremove /dev/vg-demo1/lv_demo1-snapshot`

- Để phục hồi lại một snapshot, trước tiên cần unmount Logical Volume của của bản snapshot trước (không phải bản snapshot)

```
umount -v /dev/vg-demo1/lv-demo1
lvconvert --merge /dev/vg-demo1/lv-demo1-snapshot
```

## **Thin Provisioning trong LVM**

- Thin Provisioning là một tính năng nữa của LVM, nó cho phép tạo ra những ổ đĩa ảo từ storage pool giúp tận dụng tối đa tài nguyên của ổ đĩa. 

- Ví dụ một storage pool có dung lượng là 15 GB, cấp cho 3 người, mỗi người 5GB, tổng tất cả mới sử dụng hết 6GB, nếu có thêm một user nữa thì sẽ không thể mắc cấp phát mặc dù thừa rất nhiều dung lượng trống (Thick volume). Để giải quyết vấn đề đó, ta có thể sử dụng Thin Provisioning. Khi đó bạn có thể cấp phát thêm cho user thứ 4 5GB để sử dụng. Cái này có nghĩa dùng bao nhiêu cấp bấy nhiêu sẽ đỡ lãng phí tài nguyên.

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/LVM/21.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/LVM/21.png)


- Đầu tiên cần cài đặt gói:
```
yum install -y device-mapper-persistent-data
```

- Tạo một Volume Group
```
vgcreate -s 32M vg-thin /dev/sdj2
```

- Tạo một LV thin pool với kích thước 2GB 

```
lvcreate -L 2G --thinpool thin-meditech vg-thin
lvs
```

Tạo các Thin Volume
```
lvcreate -V 512M --thin -n thin-si1 vg-thin/thin-meditech
lvcreate -V 512M --thin -n thin-si2 vg-thin/thin-meditech
lvcreate -V 1G --thin -n thin-si3 vg-thin/thin-meditech
lvcreate -V 2G --thin -n thin-si4 vg-thin/thin-meditech
```
Tạo thư mục, format và mount để sử dụng

```
mkdir /mnt/si{1..4}
mkfs.ext3 /dev/vg-thin/thin-si1 && mkfs.ext3 /dev/vg-thin/thin-si2 && mkfs.ext3 /dev/vg-thin/thin-si3  mkfs.ext3 /dev/vg-thin/thin-si4
mount /dev/vg-thin/thin-si1 /mnt/si1
mount /dev/vg-thin/thin-si2 /mnt/si2
mount /dev/vg-thin/thin-si3 /mnt/si3
mount /dev/vg-thin/thin-si4 /mnt/si4
```
Tôi vừa tạo được 4 LV thin tổng 4G trên một pool chỉ có 2G mà vẫn được.




































