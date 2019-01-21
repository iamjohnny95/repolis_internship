## Cấu trúc file hệ thống 
- Trên nhiều hệ thống , bao gồm hệ thống Linux, file hệ thống đã được cấu trúc giống 1 nhánh cây. 
## Các định dạng filesystem trong linux
Ext – Extended file system: là định dạng file hệ thống đầu tiên được thiết kế dành riêng cho Linux. Có tổng cộng 4 phiên bản Ext1, Ext2, Ext3, Ext4. Hiện nay đa phần người dùng sử dụng định dạng Ext4 vì nó có thể giảm bớt hiện tượng phân mảnh dữ liệu trong ổ cứng, hỗ trợ các file và phân vùng có dung lượng lớn…
XFS: Khá tương đồng với Ext4 về một số mặt nào đó, chẳng hạn như hạn chế được tình trạng phân mảnh dữ liệu, không cho phép các snapshot tự động kết hợp với nhau, hỗ trợ nhiều file dung lượng lớn, có thể thay đổi kích thước file dữ liệu…
JFS: Điểm mạnh của JFS là tiêu tốn ít tài nguyên hệ thống, đạt hiệu suất hoạt động tốt với nhiều file dung lượng lớn và nhỏ khác nhau. Tốc độ kiểm tra ổ đĩa nhanh hơn so với các phiên bản Ext.
Và nhiều định dạng khác….
## Tìm hiểu về mount và umount:
- Mount để "gắn" thiết bị và thư mục. Khi cài đặt bạn được yêu cầu tạo ra ít nhất hai phân vùng. Một để "gắn" thư mục root vào (/) và một choswap. Linux coi toàn bộ hệ thống là một FileSystem duy nhất và bạn có thể "gắn" ổ đĩa cũng như thiết bị lên bất kỳ thư mục thông thường nào trên đó. Một số bản phân phối Linux dành riêng một số thư mục để ta gắn các ổ đĩa lên đó. Ở Ubuntu đó là thư mục /media dành để gắn các ổ đĩa tự động và /mnt dùng với mục đích chung.

`$ mount /dev/sda5 /mnt`

Đó sẽ gắn các file hệ thống đã được bao gồm trong đĩa partition đã được liên kết với `/dev/sda5`, vào cây hệ thống tại thư mục `/mnt`. Chú ý rằng trừ khi hệ thống khác còn chỉ duy nhất user root có quyền chạy lệnh `mount`. Nếu bạn muốn được chạy sẵn khi khởi động hệ điều hành thì phải cần chỉnh sửa file `/etc/fstab`. Khi mở file etc/fstab sẽ chỉ cho bạn thấy được những file đã được cấu hình trước đó.
- Câu lệnh `umount` được sử dụng để gỡ file hệ thống từ mount point

`$ umount /mnt`

- Câu lệnh `df-Th` để hiển thị thông tin về file hệ thống đã được mount bao gồm kiểu thông kê đã sử dụng và khoảng dung lượng còn lại.
```
# df -Th
Filesystem                 Type      Size  Used Avail Use% Mounted on
/dev/mapper/os-root        xfs        50G  2.0G   48G   4% /
devtmpfs                   devtmpfs  1.8G     0  1.8G   0% /dev
tmpfs                      tmpfs     1.9G  4.0K  1.9G   1% /dev/shm
tmpfs                      tmpfs     1.9G  8.6M  1.8G   1% /run
tmpfs                      tmpfs     1.9G     0  1.9G   0% /sys/fs/cgroup
/dev/mapper/swift01-zone01 xfs        49G   33M   49G   1% /srv/node/z1d1
/dev/mapper/swift02-zone02 xfs        49G   33M   49G   1% /srv/node/z2d1
/dev/sda1                  xfs       497M  167M  331M  34% /boot
/dev/mapper/os-data        xfs        20G  261M   20G   2% /data
```
- Các thư mục trong filesystem:
1. / – Root
Đây là thư mục ở mức cao nhất như đã nói ở trên. Tất cả các tệp tin và thư mục đều nằm trong thư mục này.
2. /sbin – System Binaries
Chứa đựng các file thực thi dạng binary (nhị phân) của các chương trình cơ bản giúp hệ thống có thể hoạt động. Các lệnh bên trong /sbin thường được sử dụng dùng cho các mục đích là duy trì quản trị hệ thống. Các lệnh này yêu cầu phải có quyền root.
Một số lệnh trong đây ví dụ: lilo, fdisk, init, ifconfig v.v.. Để liệt kê, bạn dùng lệnh “ls /sbin/”.
Còn một thư mục mà nó chứa các tệp tin thi hành cho hệ thống là /usr/sbin/. Nhưng các chương trình ở đây không được sử dụng để bảo trì hệ thống.
3. /bin – User Binaries
Đối lập với /sbin/ thư mục này chứa rất nhiều ứng dụng khác nhau dùng được cả cho việc bảo trì hệ thống của root, cũng như các lệnh cho người dùng thông thường. Thư mục này thông thường chứa hệ vỏ (Shell), cũng như rất nhiều lệnh hữu dụng như cp (sao chép), mv (di chuyển), cat, ls. Cũng giống như sbin, thư mục /usr/bin cũng chứa các tệp tin có chức năng tương tự như /bin.
4. /boot – Boot Loader Files
Nó chứa các tệp tin khởi động và cả nhân kernel là vmlinuz. Trong các bản phân phối gần đây, nó cũng chứa cả dữ liệu cho grub. Phần mềm khởi động Grub (viết tắt của GRand Unified Boot loader) ngày nay được sử dụng khá phổ biến.
5. /dev – Device Files
Đây là một thư mục thú vị nhất, nó thể hiện một cách rõ ràng là hệ điều hành Linux coi mọi thứ đều là các tệp tin và thư mục.
Trong thư mục này bạn có thể thấy rất nhiều tệp tin đại diện cho các thiết bị như ổ đĩa SATA, cổng COM v.v.. Bạn liệt kê chúng ra bằng lệnh “ls /dev/”. Bạn sẽ thấy rất nhiều nhưng không phải chúng đều có thật trên máy tính của bạn đâu nhé. Chẳng hạn bạn chỉ có một cổng COM nhưng ở đây bạn sẽ thấy không chỉ có một.
Ví dụ:
/dev/sda : đây là ổ đĩa SATA thứ nhất
/dev/cdrom : ổ CD
/dev/ttyS0 : cổng COM1
6. /etc – Configuration Files
Chứa file cấu hình cho các chương trình hoạt động. Chúng thường là các tệp tin dạng text thường. Chức năng của nó gần giống với “Control Panel” trong Windows. Ví dụ:
/etc/resolv.conf (cấu hình dns-server )
/etc/network dùng để quản lý dịch vụ network
Ở /etc có một thư mục quan trọng đó là /etc/rc.d. Nơi đây thường chứa các scripts dùng để start, stop, kiểm tra status cho các chương trình.
7. /home – Home Directories
Thư mục Home. Thư mục này chứa thông tin, dữ liệu , cấu hình riêng cho từng user. Nó giống như thư mục “C:\Documents and Settings” trong Windows XP.
8. /lib – System Libraries
Chứa các file library hỗ trợ cho các file thực binary. Tên của các file library thường là ld* or lib*.so.* . Ví dụ như libc.so.* (Thư viện C).
9. /lost+found
Vì một lý do bất ngờ nào đó như lỗi phần mềm, mất điện v..v, hệ thống có thể đổ vỡ. Khi khởi động lại, hệ thống sẽ kiểm tra lại hệ thống filesystem bằng lệnh fchk và cố gắng phục hồi lại các lỗi mà nó tìm thấy. Kết quả của việc này sẽ được lưu giữ trong thư mục /lost+found.
10. /mnt – Mount Directory
Chứa các thư mục dùng để system admin thực hiện quá trình mount. Như đã nói, hệ điều hành Linux coi tất cả là các file và lưu giữ trên một cây chung. Đây chính nơi tạo ra các thư mục để ‘gắn’ các phân vùng ổ đĩa cứng cũng như các thiết bị khác vào. Sau khi được mount vào đây, các thiết bị hay ổ cứng được truy cập từ đây như là một thư mục. Trong một số hệ điều hành, các ổ đĩa chưa được gắn sẵn vào hệ thống bởi fstab sẽ được gắn ở đây. Về cách gắn và tháo, có lẽ cần một bài viết riêng.
11. /opt – Optional add-on Applications
Chứa các phần mềm và phần mở rộng không nằm trong phần cài đặt mặc định, thường là của hãng thứ ba.
12. /proc – Process Information
Chứa đựng thông tin về quá trình xử lý của hệ thống
Đây là một pseudo filesystem chứa đựng các thông tin về các process đang chạy
Đây là một virtual filesystem chứa đựng các thông tin tài nguyên hệ thống. Ví dụ:/proc/cpuinfo cung cấp cho ta thông số kỹ thuật của CPU. Để xem bạn dùng lệnh ‘cat’:

`$cat /proc/cpuinfo`

13. /tmp – Temporary Files
Thư mục này chứa các file được tạo với mục đích dùng tạm thời bởi hệ thống cũng như user. Các file bên dưới thư mục này được xóa đi khi hệ thống reboot hay shutdown.
14. /usr – User Programs
Chứa các file binary, library, tài liệu, source-code cho các chương trình

/usr/bin chứa file binary cho các chương trình của user. Nếu như một user trong quá trình thực thi một lệnh ban đầu sẽ tìm kiếm trong /bin, nếu như không có thì sẽ tiếp tục nhìn vào /usr/bin. Ví dụ một số lệnh như at. awk, cc…
/usr/sbin chứa các file binary cho system administrator. Nếu như ta không tìm thấy các file system binary bên dưới /sbin thì ta có thể tìm ở trong /usr/sbin. Ví dụ một số lệnh nhưcron, sshd, useradd, userdel
/usr/lib chứa các file libraries cho /usr/bin và /usr/sbin
/usr/local dùng để chứa chương trình của các user, các chương trình này được cài đặt từ source. Ví dụ khi ta install apache từ source thì nó sẽ nằm ở vị trí là/usr/local/apache2
15. /media – Removable Media Devices
Chứa thư mục dùng để mount cho các thiết bị removable. Ví dụ như CDROM, Floppy v.v..
16. /var – Variable Files
Chứa đựng các file có sự thay đổi trong quá trình hoạt động của hệ điều hành cũng như các ứng dụng. Ví dụ:
+ Nhật ký của hệ thống /var/log
+ database file /var/lib
+ email /var/mail
+ Các hàng đợi in ấn: /var/spool
+ lock file: /var/lock
+ Các file tạm thời cần cho quá trình reboot: /var/tmp
+ Dữ liệu cho trang web: /var/www


