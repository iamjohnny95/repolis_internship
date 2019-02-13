# **Init process là gì**

Init process là một tiến trình được khởi động lên đầu tiên trong hệ thống Linux. Tức là sau khi bạn chọn hệ điều hành trong menu của Boot Loader. Hệ điều hành bắt đầu được khởi động và tiến trình đầu tiên khởi động lên là init. Nhiệm vụ của init là start và stop các process, services… cần thiết khác.

Vì init là tiến trình được khởi động đầu tiên của hệ thống Linux nên:

Init process luôn có PID (Process ID) là 1.
Tiến trình init là tiến trình cha (hoặc ông nội =)) ) của các tiến trình khác.
Có ba kiểu triển khai init system chính trong hệ thống Linux là:

System V (đọc là System Five – V là số 5 la mã đó): là phiên bản truyền thống của init system trên nhiều hệ thống Linux.
Upstart: Được phát triển bởi Canonical vào khoảng năm 2009 và sử dụng trong các phiên bản Ubuntu cũ hơn bản 15.04.
Systemd: Là một init system được phát triển khoảng năm 2010 và được nhiều Linux distributions sử dụng để thay thế các init system cũ. Ubuntu từ phiên bản 15.04 và Centos từ phiên bản 7 đã sử dụng systemd làm init system mặc định.

# **Systemd**
- `Systemd` là một `init system` mới đang dần thay thế các `init system` cũ vì nhiều lý do. Hiện nay Centos 7 và Ubuntu 16.04 đã sử dụng systemd làm init system mặc định của hệ thống.
- `Systemd` không chỉ dừng lại ở việc start hoặc stop các services nó còn có thể mount filesystems, quản lý network sockets… Và để thực hiện được những công việc đó nó phân chia ra các đơn vị units:
   - **Service units (.service)** – để start và stop các service.
   - **Mount units (.mount)** – Để quản lý các mount point.
   - **Target units (.target)** – Để điều khiển các “runlevels” (khái niệm runlevels chỉ sử dụng trong **SysV init**).

 - Systemd là sự khác biệt giữa 2 phiên bản CentOS 6 và CentOS 7:

    - init – là process đầu tiên được load và sẽ nằm ở đó cho đến khi hệ thống (họ nhà Red Hat, Centos ) shutdown. Múc đích của nó là sử dụng các run levels để quyết định daemons nào được start và tương tác để điều khiển chúng. Tuy nhiên điểm cố hữu ” chết người” của init là ở chỗ nó khởi động các process theo thứ tự lần lượt, các tác vụ chỉ được khởi động khi tác vụ trước đó đã hoàn thành. Vì thế sẽ mất nhiều thời gian hơn và nếu một tác vụ bị failed, quá trình khởi động sẽ dừng lại ở đó cho đến khi nó tìm được cách xử lý.

    - Upstart – là sự thay thế cho init, chủ yếu sử dụng trên Ubuntu và dành cho mục đích khởi động các process không đồng thời, điều này làm tăng tốc độ boot và mức ổn định của hệ thống.

 - Ở Centos 7 systemd cũng làm nhiệm vụ tương tự init và là tiến trình đầu tiên khi khởi động, có pid =1. systemd không phải là một process đơn thuần mà nó còn chứa các gói, các thư viện và các công cụ trong đó. 

 - Khác hoàn toàn với init, systemd khởi động các process song song, không còn phụ thuộc vào nhau nên giảm thiểu thời gian khởi động và tăng tính ổn định khi một process failed sẽ không ảnh hưởng đến toàn bộ quá trình khởi động. Không chỉ khởi động các chương trình core, systemd còn khởi động các hoạt động khác trên hệ thống như network stack, bộ cron job scheduler, user login….

 “Runlevels” trong systemd.
Trong SysV init system (nếu bạn đã biết Linux từ trước) có các runlevels:

0: halt
1: single-user
2: multi-user
3: multi-user with networking
4: undefined (user defined)
5: multi-user with display manager (graphical login)
6: reboot
Trong systemd khái niệm “runlevels” được thay thế bằng các targets để boot vào như:

poweroff.target – shutdown system
rescue.target – single user mode
multi-user.target – multiuser with networking
graphical.target – multiuser with networking and GUI
reboot.target – restart

- Ta sẽ xem các ví dụ về việc sử dụng systemd như sau:

- File cấu hình chung của systemd nằm trong thư mục /etc/systemd

- File cấu hình các service thì nằm trong /usr/lib/systemd

- Các file custome config thì đặt trong /etc/systemd/system, đặc biệt đôi khi thư mục /run/systemd/system cũng đc sử dụng

- Để xem phiên bản của systemd hiện tại, sử dụng lệnh:
 
 ```
 # systemd-analyze blame
7.029s network.service
2.241s plymouth-start.service
1.293s kdump.service
1.156s plymouth-quit-wait.service
1.048s firewalld.service
632ms postfix.service
621ms tuned.service
460ms iprupdate.service
446ms iprinit.service
344ms accounts-daemon.service
...
7ms systemd-update-utmp-runlevel.service
5ms systemd-random-seed.service
5ms sys-kernel-config.mount
```

 ```
  # systemctl --version
  systemd 208
  +PAM +LIBWRAP +AUDIT +SELINUX +IMA +SYSVINIT +LIBCRYPTSETUP +GCRYPT +ACL +XZ
```
- Nhiệm vụ chính của systemd là quản lý các boot process và cung cấp thông tin về nó

- Để xem các service trong quá trình boot của nó, ta sử dụng lệnh như sau

```
# systemd-analyze blame
7.029s network.service
2.241s plymouth-start.service
1.293s kdump.service
1.156s plymouth-quit-wait.service
1.048s firewalld.service
632ms postfix.service
621ms tuned.service
460ms iprupdate.service
446ms iprinit.service
344ms accounts-daemon.service
...
7ms systemd-update-utmp-runlevel.service
5ms systemd-random-seed.service
5ms sys-kernel-config.mount
```
# **CÁC THÀNH PHẦN CƠ BẢN VÀ QUAN TRỌNG TRONG systemd**

**Service Management – Quản lý các services**
- Để quản lý các services, systemd sử dụng systemctl thay thế cho các lệnh chkconfig và service trước đây của Centos 6.

- Ví dụ để active ntp services lúc khởi động thay cho chkconfig

```
# systemctl enable ntpd (thay vì chkconfig ntpd on)
```

- Chú ý 1: Cú pháp chuẩn phải là ntpd.service nhưng mặc định .service sẽ tự động được thêm vào.
- Chú ý 2: nếu là đường dẫn, .mount sẽ được thêm vào.
- Chú ý 3: Nếu là thiết bị,  .device sẽ được thêm vào.

- Để deactivate, start, stop một services:
```
# systemctl disable ntpd (thay vì chkconfig ntpd off)
# systemctl start ntpd (thay vì services ntpd start)
# systemctl stop ntpd (thay vì services ntpd stop)
```
- Kiểm tra NTP service có được active lúc khởi động:
```
# systemctl is-enabled ntpd
enabled
```

- Kiểm tra NTP service có hoạt động:

```
# systemctl is-active ntpd
inactive
```

# **3. Targets/Run Levels** 
- Systemd sử dụng các targets. Một target là một kỹ thuật ghép nhóm cho phép nhiều services khởi động cùng lúc. Các services này được kết hợp với một target cụ thể và được lưu trong thư mục cùng tên với tên target. Hiểu theo một cách nào đó, target thay thế các run levels (level 3 chế độ dòng lệnh hay level 5 chế độ đồ họa). File /etc/inittab sẽ không còn được sử dụng để set default run level nữa và vì thế việc thay đổi nó sẽ không còn tác dụng trong Centos 7.
 
- Để chuyển sang level 3:
```
# systemctl isolate runlevel3.target
```
hay 

```
# systemctl isolate multi-user.target
```
Để chuyển sang chế độ đồ họa 

```
# systemctl isolate graphical.target
```

Kiểm tra run level đang chạy của hệ thống

```
# systemctl get-default
graphical.target
```


