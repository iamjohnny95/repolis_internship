## **Một số câu lệnh**

### **Câu lệnh xem dụng lượng máy chủ Linux**

**1. Sử dụng bằng lệnh df**

```
[root@matbao ~]# df
```

```
Filesystem           1K-blocks      Used Available Use% Mounted on
 /dev/cciss/c0d0p2     78361192  23185840  51130588  32% /
 /dev/cciss/c0d0p5     24797380  22273432   1243972  95% /home
 /dev/cciss/c0d0p3     29753588  25503792   2713984  91% /data
 /dev/cciss/c0d0p1       295561     21531    258770   8% /boot
 ```

 ```
 [root@matbao ~]# df -a
 ```

 ```
 Filesystem           1K-blocks      Used Available Use% Mounted on
 /dev/cciss/c0d0p2     78361192  23186116  51130312  32% /
 proc                         0         0         0   -  /proc
 sysfs                        0         0         0   -  /sys
 devpts                       0         0         0   -  /dev/pts
 /dev/cciss/c0d0p5     24797380  22273432   1243972  95% /home
 /dev/cciss/c0d0p3     29753588  25503792   2713984  91% /data
 /dev/cciss/c0d0p1       295561     21531    258770   8% /boot
 tmpfs                   257476         0    257476   0% /dev/shm
 none                         0         0         0   -  /proc/sys/fs/binfmt_misc
 sunrpc                       0         0         0   -  /var/lib/nfs/rpc_pipefs
 ```

```
 [root@matbao ~]# df -h
```

```
Filesystem            Size  Used Avail Use% Mounted on
 /dev/cciss/c0d0p2      75G   23G   49G  32% /
 /dev/cciss/c0d0p5      24G   22G  1.2G  95% /home
 /dev/cciss/c0d0p3      29G   25G  2.6G  91% /data
 /dev/cciss/c0d0p1     289M   22M  253M   8% /boot
 tmpfs                 252M     0  252M   0% /dev/shmof /home
 ```

 ```
 [root@matbao ~]# df -hT /home
 ```

 ```
 Filesystem      Type    Size  Used Avail Use% Mounted on
 /dev/cciss/c0d0p5   ext3     24G   22G  1.2G  95% /home
 View all Disk Partitions in Linux
 ```

 ```
[root@matbao ~]# fdisk –l
```

```
Disk /dev/sda: 637.8 GB, 637802643456 bytes
 255 heads, 63 sectors/track, 77541 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 ```

 **2. Sử dụng lệnh du**

 Ví dụ: chúng ta sử dụng command sau để bắt đầu tìm 10 file/thư mục chiếm nhiều dung lượng nhất

```
[root@matbao ~]#du -a /var | sort -n -r | head -n 10
```

```
1008372 /var
 313236 /var/www
 253964 /var/log
 192544 /var/lib
 152628 /var/spool
 152508 /var/spool/squid
 136524 /var/spool/squid/00
 95736 /var/log/mrtg.log
 74688 /var/log/squid
 62544 /var/cache
 ```

 - `du`: Tính dung lượng ổ cứng mà file/thư mục đang chiếm dụng.

 - `sort`: Sắp xếp các dòng của một file text hoặc của dữ liệu truyền vào.

 - `output`: Hiển thị phần đầu nội dung một file văn bản, ví dụ 10 dòng đầu tiên của kết quả sau sắp xếp sẽ là 10 file/thư mục chiếm nhiều dung lượng nhất.

 Nếu bạn muốn một kết quả tốt hơn, dễ hiểu hơn thì có thể thử nhiều phương án sau:

 ```
 $ cd /path/to/some/where
 $ du -hsx * | sort -rh | head -10
 ```

 Trong đó:

- cd /path/to/some/where: là lệnh di chuyển tới đường dẫn của thư mục cần kiểm tra dung lượng.

- Tham số -h (du -h): Hiện kết quả với định dạng quen thuộc với người dùng (ví dụ: 1K, 234M, 2G).

- Tham số -s (du -s): Chỉ hiện thống kê chung kết quả kiểm tra của lệnh du.

- Tham số -x (du -x): Bỏ qua thư mục khác định dạng file hệ thống của hệ điều hành.

- Tham số -r (sort -r): Đảo ngược kết quả so sánh.

- Tham số -h (sort -h): So sánh bằng tham số điều chỉnh đơn vị đo lường quen thuộc (K, M, G). Chỉ áp dụng cho lệnh sort cài thêm theo giấy phép phần mềm GNU.

- Tham số -10 hoặc -n 10 (head -10 hoặc head -n 10): Hiển thị 10 dòng đầu tiên của kết quả tìm kiếm.

**3.Sử dụng câu lệnh `lsblk`**

- Câu lệnh để hiện thị thông tin Block device như sau:

```
$ lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda       8:0    0 931.5G  0 disk
├─sda1    8:1    0  1000M  0 part
├─sda2    8:2    0   260M  0 part /boot/efi
├─sda3    8:3    0  1000M  0 part
├─sda4    8:4    0   128M  0 part
├─sda5    8:5    0 557.1G  0 part
├─sda6    8:6    0    25G  0 part
├─sda7    8:7    0  14.7G  0 part
├─sda8    8:8    0     1M  0 part
├─sda9    8:9    0 324.5G  0 part /
└─sda10   8:10   0   7.9G  0 part [SWAP]
sr0      11:0    1  1024M  0 rom
```

- Nếu bạn muốn hiển thị toàn bộ Block Device trên hệ thống của mình thì sử dụng thêm tùy chọn -a

```
$ lsblk -a
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda       8:0    0 931.5G  0 disk
├─sda1    8:1    0  1000M  0 part
├─sda2    8:2    0   260M  0 part /boot/efi
├─sda3    8:3    0  1000M  0 part
├─sda4    8:4    0   128M  0 part
├─sda5    8:5    0 557.1G  0 part
├─sda6    8:6    0    25G  0 part
├─sda7    8:7    0  14.7G  0 part
├─sda8    8:8    0     1M  0 part
├─sda9    8:9    0 324.5G  0 part /
└─sda10   8:10   0   7.9G  0 part [SWAP]
sdb       8:16   1         0 disk
sr0      11:0    1  1024M  0 rom
ram0      1:0    0    64M  0 disk
ram1      1:1    0    64M  0 disk
ram2      1:2    0    64M  0 disk
ram3      1:3    0    64M  0 disk
ram4      1:4    0    64M  0 disk
ram5      1:5    0    64M  0 disk
ram6      1:6    0    64M  0 disk
ram7      1:7    0    64M  0 disk
ram8      1:8    0    64M  0 disk
ram9      1:9    0    64M  0 disk
loop0     7:0    0         0 loop
loop1     7:1    0         0 loop
loop2     7:2    0         0 loop
loop3     7:3    0         0 loop
loop4     7:4    0         0 loop
loop5     7:5    0         0 loop
loop6     7:6    0         0 loop
loop7     7:7    0         0 loop
ram10     1:10   0    64M  0 disk
ram11     1:11   0    64M  0 disk
ram12     1:12   0    64M  0 disk
ram13     1:13   0    64M  0 disk
ram14     1:14   0    64M  0 disk
ram15     1:15   0    64M  0 disk
```

**Câu lệnh egrep**

Linux cung cấp `grep` để lọc văn bản. Nhưng trong một vài tình huống chúng ta có lẽ cần công cụ mở rộng hơn. Công nghệ đó đã được gọi là egrep cung cấp thuộc tính mở rộng hơn công cụ phổ biến grep 

**Tìm kiếm thông thường**

Chúng ta có thể sử dụng `egrep` để tìm kiếm văn bản thông thường mà không cần cung cấp dấu hiệu thông thường. Chúng ta chỉ cần cung cấp điều

kiện chúng ta muốn tìm kiếm. Trong ví dụ chúng ta sẽ tìm kiếm `ismail` trong file có tên `/etc/passwd`

**Nối những dòng bao gồm các chữ trong bảng chữ cái**

- Chúng ta cũng có thể chỉ rõ các chữ cái với [a-z] và ký tự [A-Z] cho ký tự viết hoa. 

```
$ egrep '[A-Z]'/etc/passwd
```

**Câu lệnh AWK**

AWK có thể làm được gì?

- Quét tất các dòng trong file

- Chia mỗi dòng đầu vào vào field

- So sánh những dòng đầu vào và các field đến pattern

- Thực hiện những chức năng, hành động 

**Câu lệnh AWK hữu hiệu**

- Thay đổi file dữ liệu 

- Tạo mẫu báo cáo

**Để giải thích kỹ hơn về cách sử dụng AWK, chúng ta sẽ sử dụng file có tên là file.txt**

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/4.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/4.png)

1st column => Item,
2nd column => Model
3rd column => Country
4th column => Cost

## **Ví dụ về câu lệnh AWK**

Để in cột 2 và 3, thực thi câu lệnh phía dưới 

```
$ awk '{print $2 "\t" $3}' file.txt
```

**Output**

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/5.png)

## **In tất cả các dòng trong 1 file**

Nếu bạn muốn liệt kê tất cả các dòng và cột trong 1 file

```
$ awk ' {print $0}' file.txt
```

**Output**

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/6.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/6.png)

**In tất cả các dòng được nối 1 pattem cụ thể**

Nếu bạn muốn in những dòng được nối 1 pattem, có cú pháp sau:

```
$ awk '/variable_to_be_matched/ {print $0}' file.txt
```

Cho ví dụ, để show ra danh sách có ký tự `o`, cú pháp sẽ là 

```
$ awk '/o/ {print $0}' file.txt
```

**OUT PUT**


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/8.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/8.png)

Để hiện ra màn hình tất cả danh sách có ký tự `e`

```
$ awk '/e/ {print $0}' file.txt
```

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/7.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/7.png)

**In cột 3 và 4 mà có ký tự a**

```
$ awk '/a/ {print $3 "\t" $4}' file.txt
```

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/9.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/9.png)

**Đếm và in kết quả ra**

Bạn có thể sử dụng AWK để đếm và in số dòng. Cho ví dụ, câu lệnh phía dưới đếm số xuất hiện. 

```
$ awk '/a/{++cnt} END {print "Count = ", cnt}' file.txt
```

**Output** 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/syslog/10.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/syslog/10.png)


## **Câu lệnh sed**

- Câu lệnh Sed trong UNIX là 1 tiêu chuẩn biên soạn và nó có thể thực hiện nhiều chức năng trên file, tìm kiếm, tìm và thay thế, chèn và xóa. Dù thông thường hầu hết sử dụng câu lệnh SED trong UNIX là để trong tình huống tìm và thay thế. Bởi sử dụng SED bạn có thể sửa files mà không cần mở nó, nó là cách nhanh hơn để tìm và thay thế một vài file, sau đó đầu tiên mở file trong VI EDITOR và sau đó thay đổi nó. 

- SED là một siêu công cụ biên soạn. Có thể chèn, xóa, tìm kiếm và thay thế

Cú pháp:

```
sed OPTIONS... [SCRIPT] [INPUTFILE...] 
```

**Ví dụ**

Cho một file văn bản

```
$cat > geekfile.txt
```

```
unix is great os. unix is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

**Thay thế chuỗi:** Câu lệnh Sed hầu như được sử dụng để thay thế văn bản trong file. Câu lệnh Sed đơn giả phía dưới được thay thế từ 

"unix" sang từ "linux" trong file.

```
$sed 's/unix/linux/' geekfile.txt
```

**OUT PUT**

```
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

Ký tự "s" chỉ rõ quá trình thay thế. Dấu "/" là để tách. "unix" là từ tìm kiếm, "linux" là từ để thay thế chuỗi.

**2.Thay thế trong trường hợp cùng 1 dòng**

- Sử dụng kết hợp /1,/2,... và /g để thay thế tất cả các ký tự xuất hiện trong cùng một dòng. Câu lệnh sed thay thế từ "unix" số 3,4,5 trở đi trong cùng một dòng. 

```
$sed 's/unix/linux/3g' geekfile.txt
```

**OUT PUT**

```
unix is great os. unix is opensource. linux is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn linux .linux is a powerful.
```

**Thay thế chuỗi trên một dòng cụ thế**

Bạn có thể hạn chế câu lệnh sed để thay thế chuỗi trên một dòng cụ thể. Ở đây thay thế trên dòng thứ 3

```
$sed '3 s/unix/linux/' geekfile.txt
```

**OUT PUT**

```
unix is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

Câu lệnh sed ở trên chỉ thay thế dòng thứ 3

**Bản sao dòng được thay thế với cờ /p**

cờ /p in thay thế lại dòng đó. Nếu không có từ thay thế trên dòng đó thì dòng đó chỉ được in 1 lần. 

```
$sed 's/unix/linux/p' geekfile.txt
```
**OUTPUT**

```
linux is great os. unix is opensource. unix is free os.
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

**Chỉ in dòng được thay thế**

```
$sed -n 's/unix/linux/p' geekfile.txt
```

**OUT PUT**

```
linux is great os. unix is opensource. unix is free os.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

**Thay thế từ dòng này đến dòng này**

```
$sed '1,3 s/unix/linux/' geekfile.txt
```

**OUT PUT**

```
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

**Xóa các dòng từ 1 file cụ thể:** 

Câu lệnh SED cũng có thể được sử dụng để xóa dòng từ một file cụ thể. Câu lệnh SED được sử dụng để thực hiện xóa hoạt động mà không cần mở 

file 

Ví dụ:

1. Để xóa một dòng cụ thể 

```
Syntax:
$ sed 'nd' filename.txt
Example:
$ sed '5d' filename.txt
```

2. Để xóa dòng cuối

```
Syntax:
$ sed '$d' filename.txt
```

3. Để xóa dòng thứ x đến y

```
Syntax:
$ sed 'x,yd' filename.txt
Example:
$ sed '3,6d' filename.txt
```





