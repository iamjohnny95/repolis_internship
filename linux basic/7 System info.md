## Linux release and system info
- Quản trị hệ thống linux cần lấy thông tin từ hệ thống. Dưới đây là một vài câu lệnh hữu dụng 
- Để xem thông tin của bản phân phối linux

```
# cat /etc/*release
CentOS Linux release 7.0.1406 (Core)
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"
CentOS Linux release 7.0.1406 (Core)
```
- Để xem thông tin của bộ nhớ của máy 
```
# head /proc/meminfo
MemTotal:        3776748 kB
MemFree:         2230496 kB
MemAvailable:    2782088 kB
Buffers:            1452 kB
Cached:           652196 kB
SwapCached:            0 kB
Active:          1069616 kB
Inactive:         193056 kB
Active(anon):     609504 kB
Inactive(anon):     8304 kB
```
- Để xem file thông tin của file system
```
# df -h
Filesystem         Dimens. Usati Disp. Uso% Montato su
/dev/sda1          12G     6,2G  4,9G  56%      /
/dev/small-db02    5,9G    2,6G  3,0G  46%      /db02
/dev/small-db01    5,0G    3,6G  1,2G  77%      /db01
/dev/small-db05    7,8G    1,2G  6,2G  17%      /db05
/dev/small-db03    39G     5,4G   32G  15%      /db03                      
/dev/small-db04    30G     2,5G   26G   9%      /db04
```
- Để xem CPU máy 
```
# cat /proc/cpuinfo | grep model | uniq -c
      2 model name      : Intel(R) Core(TM)2 Duo CPU     E8500  @ 3.16GH
```
-File system proc
 file system `/proc` bao gồm các file hệ thống. file hệ thống bao gồm những file và đường dẫn giống với cấu trúc kernel và thông tin cấu hình. Nó không có các file thực sự nhưng chứa thông tin hệ thống (system memory, devices mounted, hardware configuration). Một vài file quan trọng trong file `/proc` là
 ```
 /proc/cpuinfo
/proc/interrupts
/proc/meminfo
/proc/mounts
/proc/partitions
/proc/version
/proc/<process-id-#>
/proc/sys
```


