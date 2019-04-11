## **Linux Security**

- Mặc định, Linux có nhiều tài khoản để phân chia các process và workloads:

  1. root
  2. system
  3. normal
  4. network 

- Với môi trường làm việc an toàn, nên giới hạn các quyền ở mức tối thiểu cho các tài khoản và các tài khoản không hoạt động. Command `last` sẽ show ra lịch sử người dùng đăng nhập vào hệ thống, xác định các tài khoản ít và đã lâu rồi không sử dụng để loại bỏ.

 ```
 [root@localhost ~]# last
root     pts/1        192.168.220.1    Mon Feb 18 13:43   still logged in
root     tty1                          Mon Feb 18 13:37   still logged in
root     pts/1        192.168.220.1    Mon Feb 18 10:42 - 10:42  (00:00)
root     pts/0        192.168.220.1    Mon Feb 18 09:51 - 14:02  (04:11)
reboot   system boot  3.10.0-957.el7.x Mon Feb 18 09:50 - 14:15  (04:25)
root     pts/0        192.168.220.1    Mon Feb 18 09:34 - down   (00:15)
root     tty1                          Mon Feb 18 09:30 - 09:49  (00:19)
reboot   system boot  3.10.0-957.el7.x Mon Feb 18 09:28 - 09:50  (00:21)
root     tty1                          Thu Feb 14 17:32 - 17:32  (00:00)
reboot   system boot  3.10.0-957.el7.x Thu Feb 14 16:23 - 17:32  (01:08)
root     pts/0        192.168.220.1    Thu Feb 14 16:06 - crash  (00:16)
root     tty1                          Thu Feb 14 16:00 - crash  (00:23)
reboot   system boot  3.10.0-957.el7.x Thu Feb 14 15:57 - 17:32  (01:35)
root     pts/0        192.168.220.1    Thu Feb 14 15:42 - crash  (00:14)
root     pts/0        192.168.220.1    Thu Feb 14 09:35 - 14:45  (05:10)
root     tty1                          Thu Feb 14 09:20 - 15:53  (06:32)
reboot   system boot  3.10.0-957.el7.x Thu Feb 14 09:12 - 17:32  (08:19)
root     pts/0        192.168.220.1    Wed Feb 13 15:45 - crash  (17:27)
root     tty1                          Wed Feb 13 15:43 - crash  (17:28)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 15:29 - 17:32 (1+02:03)
root     tty1                          Wed Feb 13 11:16 - 12:45  (01:29)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 11:15 - 17:32 (1+06:16)
root     tty1                          Wed Feb 13 11:14 - 11:15  (00:01)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 11:12 - 11:15  (00:02)
root     tty1                          Wed Feb 13 10:42 - 11:11  (00:29)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 10:40 - 11:11  (00:31)
root     tty1                          Wed Feb 13 10:17 - 10:39  (00:22)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 10:15 - 10:39  (00:24)
root     tty1                          Wed Feb 13 10:10 - 10:12  (00:02)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 10:06 - 10:12  (00:06)
root     pts/0        192.168.220.1    Wed Feb 13 09:41 - down   (00:24)
root     tty1                          Wed Feb 13 09:40 - 10:06  (00:25)
reboot   system boot  3.10.0-957.el7.x Wed Feb 13 09:33 - 10:06  (00:33)

```
Trong đó :
- pts/0: Nghĩa là user này đang kết nối thông qua các chương trinh remote connection như SSH hoặc telnet
- tty: user này đang được kết nối thông qua local terminal
- shutdown/reboot: thể hiện thông tin hệ thống về hostname hoặc địa chỉ IP của máy tính kết nối tới. Nếu bạn thấy "0.0" hoặc không có thông tin  gì chứng tỏ user đó được kết nối terminal như console. 
- cột 4 trở đi: thể hiện thời gian đăng nhập vào/ thời gian thoát ra khỏi hệ thống và khoảng thời gian hoạt động của terminal session đó.

- user`root` là tài khoản có quyền hạn cao nhất trong hệ thống. Nó có quyền quản trị hệ thống, tạo hay xóa, hay thay đổi mật khẩu tài khoản, kiểm tra log, cài đặt phần mềm... 
- Một tài khoản người dùng thường có thể thực hiện những hoạt động yêu cầu sự cấp quyền ; tuy nhiên nên cấu hình cho phép những hoạt động đó được thực thi. Chạy một network client hoặc chia sẻ file qua mạng là những hành động không yêu cầu tài khoản root để được thực thi.

## **Sudo và Su Command** 
- Mặc định, `sudo` sẽ kích hoạt cho mỗi người dùng, tuy nhiên với một số các distro như Ubuntu thì chỉ kích hoạt cho ít nhất một người dùng chính.

- Khi sử dụng `sudo<command>` lệnh được thực hiện với quyền root, sau khi thực hiện xong sẽ trở về quyền người dùng bình thường.
- File cấu hình `/etc/sudoers` và `/etc/sudoers.d`. Có thể sửa file `/etc/sudoers` bằng lệnh `visudo` 
- khi `sudo` được thực hiện, sẽ có một tiến trình trỏ tới `/etc/sudoers` các file trong `etc/sudoer.d` để xác định người dùng đó có được cấp quyền `sudo` không, nếu được cấp thì có những quyền gì. Nếu không được phép thực hiện lệnh đó thì sẽ ghi lại log về thông tin đăng nhập.

## **Tiến trình riêng biệt**
- Linux bảo mật hơn các hệ điều hành khác là do các tiến trình hoạt động độc lập với nhau. Một tiến trình không thể truy cập tài nguyên của các tiến trình khác kể cả khi nó đang chạy phiên bản của một người dùng.

- Một cơ chế đã được bổ sung vào để bảo mật và hạn chế tối thiểu các mối nguy hại đã được giới thiệu gần đây: 
 
 - `Control Groups`: Cho phép người quản trị phân nhóm các tiến trình và cấp tài nguyên hữu hạn cho mỗi người nhóm (cgroup).
 - `Linux Containers`: Cho phép chạy nhiều phiên bản Linux trên cùng một hệ thống.
 - `Virtualization`: Phần cứng được tính toán sao cho không chỉ tách biệt các tiến trình, đồng thời cũng phải tách biệt với phần cứng mà các máy ảo sử dụng trên cùng một host vật lý.

## **Mã hóa mật khẩu**

- Hầu hết các phiên bản linux đều sử dụng một thuật toán mã hóa là SHA-512, được phát triển bởi NSA để mã hóa mật khẩu. SHA-512 được sử dụng rộng rãi để bảo vệ các ứng dụng và giao thức như TLS, SSL, PHP, S/MINE và IPSec.

## **Password aging**
- Password aging  là một phương thức nhắc nhở người dùng tạo password mới sau một thời gian sử dụng, nhằm nâng cao tính bảo mật. Điều này có thể củng cố cho việc bảo mật, nếu hệ thống bị xâm nhập thì cũng chỉ sử dụng được trong một thời gian nhất định.
 
 - Sử dụng command `change` để điều chỉnh mật khẩu 
 ``` Options:
  -d, --lastday LAST_DAY        set date of last password change to LAST_DAY
  -E, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
  -h, --help                    display this help message and exit
  -I, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -l, --list                    show account aging information
  -m, --mindays MIN_DAYS        set minimum number of days before password
                                change to MIN_DAYS
  -M, --maxdays MAX_DAYS        set maximim number of days before password
                                change to MAX_DAYS
  -R, --root CHROOT_DIR         directory to chroot into
  -W, --warndays WARN_DAYS      set expiration warning days to WARN_DAYS
```
:

## **Selinux**
- Selinux là một tiện ích bảo vệ ở tầng kernel, có thể được sử dụng để bảo vệ chống lại việc cấu hình chương trình sai. Nó đi kèm với hệ thống MAC dùng để cải các mô hình truyền thống Unix/ Linux DAC. Selinux có ba trạng thái như sau:
  - **Enforcing**: chế độ mặc định cho phép và thực thi chính sách bảo mật SElinux trên hệ thống, từ chối các hàng động và ghi truy cập 
  - **Permissive**: Trong chế độ Permissive, SElinux được kích hoạt nhưng sẽ không thực thi chính sách bảo mật, chỉ cảnh báo và ghi lại các hành động. Chế độ Permissive hữu ích trong việc khắc phục sự cố SElinux 
  - **Disabled** Selinux bị vô hiệu hóa hoặc tắt đi

 - Tuy nhiên có trường hợp nó lại gây phiền phức khi bạn muốn cài một phần mềm mà phần mềm đó lại muốn can thiệp sâu vào linux, lúc đó ta nên disable SElinux. Để tắt SElinux ta vào 
 ```
 vi /etc/selinux/config
 ```
 Sau đó thay giá trị `enforcing` bằng `disabled`

## **Cài đặt SSH key trên CentOS 7**
### **Tạo cặp khóa RSA**
- Bước đầu tiên tạo một cặp khóa trên máy khách. `keygen` sẽ sinh ra khóa công khai và gửi đến máy client
```
ssh-keygen
```
- Theo mặc định, `ssh-keygen` sẽ tạo ra một cặp khóa RSA 2048-bit, đủ an toàn cho hầu hết các trường hợp sử dụng (bạn có thể tùy ý vượt qua cờ `-b 4096` để tạo ra một khóa 4096 lớn hơn).

- Sau khi nhập lệnh, bạn sẽ thấy dấu nhắc sau:
```
Output
Enter file in which to save the key (/your_home/.ssh/id_rsa):
```
- Nhấn ENTERđể lưu cặp khóa vào thư mục con .ssh/ trong thư mục chính của bạn, hoặc chỉ định một đường dẫn thay thế.
- Sau đó, bạn sẽ thấy dấu nhắc sau:

```
Output
Enter passphrase (empty for no passphrase):
```
- Tại đây bạn tùy ý có thể nhập cụm từ mật khẩu bảo mật, được đánh giá cao. Cụm từ mật khẩu thêm một lớp bảo mật bổ sung để ngăn người dùng trái phép đăng nhập.  
- Bạn  sẽ thấy kết quả sau:
```
Output
Your identification has been saved in /your_home/.ssh/id_rsa. 
Your public key has been saved in /your_home/.ssh/id_rsa.pub.
The key fingerprint is: 
a9:49:2e:2a:5e:33:3e:a9:de:4e:77:11:58:b6:90:26 username@remote_host 
The key's randomart image is:
+--[ RSA 2048]----+
| ..o |
| E o= . |
| o. o |
| .. | 
| ..S | 
| o o. |
| =o.+. |
| . =++.. |
| o=++. |
+-----------------+
```
- Bây giờ bạn có một khóa công khai và riêng tư mà bạn có thể sử dụng để xác thực. Bước tiếp theo là đặt khóa công khai trên máy chủ của bạn để bạn có thể sử dụng chứng thực dựa trên SSH Key để đăng nhập.

**Bước 2- Sao chép Public Key tới máy chủ CentOS**
- Cách nhanh nhất để sao chép khóa công khai của bạn đến máy chủ CentOS là sử dụng một tiện ích được gọi là `ssh-copy-id`.Do tính đơn giản của nó nên phương pháp này được đánh giá cao nếu có. Nếu bạn không có `ssh-copy-id` có sẵn trên máy khách, bạn có thể sử dụng một trong hai phương pháp thay thế được cung cấp trong phần này (sao chép qua SSH dựa trên mật khẩu hoặc tự sao chép khóa

**Sao chép Public Key của bạn sử dụng `ssh-copy-id`**
- Công cụ `ssh-copy-id` được bao gồm theo mặc định trong nhiều hệ điều hành, vì vậy bạn có thể có nó trên hệ thống cục bộ . Để phương pháp này hoạt động, bạn phải có quyền truy cập SSH dựa trên mật khẩu vào máy chủ của mình.

Để sử dụng tiện ích này, bạn chỉ cần chỉ định máy chủ từ xa mà bạn muốn kết nối và tài khoản người dùng mà bạn có mật khẩu truy cập vào SSH. Đây là tài khoản mà SSH Key công khai của bạn sẽ được sao chép.

Cú pháp là:
```
ssh-copy-id -i /root/.ssh/id_rsa.pub 192.168.220.15
```
Kết nối ssh được thiết lập. Bây giờ ssh đến máy chủ 
```
ssh 192.168.220.15
```
Sau đó thử cp đến máy client
```
scp -r /testssh/ root@192.168.220.15:/root
```

**Chú ý:** file /etc/ssh/sshd.conf** chứa các file để chỉnh sửa cấu hình đăng nhập kể cả root
## **Cấm truy cập SSH đến tài khoản root**
- Để vô hiệu hóa đăng nhập root, mở tập tin cấu hình ssh/etc/ssh/sshd_config, sau đó tìm đến dòng:

`#PermitRootLogin no`

- Bỏ kí tự # trước dòng đó:

`PermitRootLogin no`

Restart lại SSH:

`#/etc/init.d/sshd restart`

Bây giờ, bạn sẽ không truy cập trực tiếp tài khoản root từ ssh được nữa. Muốn truy cập được tài khoản root phải vào 1 tài khoản khác rồi su đến user root

## **Giới hạn user SSH đăng nhập**

- Nếu bạn có số lượng lớn các tài khoản người dùng trên hệ thống, bạn cần mở ssh cho những người dùng cần thiết. Mở file /etc/ssh/sshd_config
`# vi /etc/ssh/sshd_config`
- Thêm một dòng AllowUsers ở dưới cùng của tập tin với khoảng tách biệt bởi danh sách các username. Ví dụ, người dùng tecmint và Sheena cả hai đều có quyền truy cập vào ssh từ xa.
`AllowUsers tecmint sheena`

- Bây giờ restart lại ssh để có hiệu lực 





