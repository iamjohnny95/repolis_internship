# **Một số hiểu biết cơ bản về log**

## **Khái niệm về log**

Log là gì? Log để làm gì?

Trước hết Bạn là người quản trị mạng của một doanh nghiệp, trong hệ thống mạng của bạn có một máy chủ chứa dữ liệu rất quan trọng. Một buổi

 tối bạn để máy chủ đó chạy suốt đêm nhưng khi về đến nhà bạn truy cập vào máy chủ thì báo lỗi từ chối dịch vụ do không thể kết nối, buổi 

 sáng bạn vội vã đến xem xét tình hình thì thấy một số dữ liệu đã bị mất và vấn đề lúc này là xem ai đã gây ra vấn đề trên. Vậy phải làm thế 

 nào để điều tra xử lý, hay đơn giản là tìm nguyên nhân để khắc phục hậu quả vừa xảy ra. Log sẽ giúp bạn làm việc này.


Vậy nên tác dụng của log là:

- Log ghi lại liên tục các thông báo về hoạt động của cả hệ thống hoặc của các dịch vụ được triển khai trên hệ thống và file tương ứng. Log file thường là các file văn bản thông thường dưới dạng “clear text” tức là bạn có thể dễ dàng đọc được nó, vì thế có thể sử dụng các trình soạn thảo văn bản (vi, vim, nano...) hoặc các trình xem văn bản thông thường (cat, tailf, head...) là có thể xem được file log.

- Các file log có thể nói cho bạn bất cứ thứ gì bạn cần biết, để giải quyết các rắc rối mà bạn gặp phải miễn là bạn biết ứng dụng nào, tiến trình nào được ghi vào log nào cụ thể.

- Trong hầu hết hệ thống Linux thì `/var/log` là nơi lưu lại tất cả các log.

Như đã nói ở trên, tác dụng của log là vô cùng to lớn, nó có thể giúp quản trị viên theo dõi hệ thống của mình tôt hơn, hoặc giải quyết các vấn đề gặp phải với hệ thống hoặc service. Điều này đặc biệt quan trọng với các hệ thống cần phải online 24/24 để phục vụ nhu cầu của mọi người dùng.

Hướng dẫn chung logfile

- Như một tiêu chuẩn chung trong hệ thống linux, các tệp tin log được đặt trong thư mục /var/log. Bất kỳ ứng dụng khác mà sau này bạn có thể

cài đặt trên hệ thống của bạn có thể sẽ tạo tập tin log của chúng ta tại /var/log. Dùng lệnh `ls -l /var/log` để xem nội dung của thư mục này.

- `/var/log/messages` - Chứa dữ liệu log của hầu hết các thông báo hệ thống nói chung, bao gồm cả các hệ thống trong quá trình khởi động hệ 

thống.

- `/var/log/cron` - Chứa dữ liệu log của cron daemon. Bắt đầu và dừng cron cũng như cronjob thất bại 

- `/var/log/maillog hoặc /var/log/mail.log` – Thông tin log từ các máy chủ mail chạy trên máy chủ.

- `/var/log/wtmp` - Chứa tất cả các đăng nhập và đăng xuất lịch sử.

- `/var/log/btmp` – Thông tin đăng nhập không thành công

- /var/run/utmp – Thông tin log trạng thái đăng nhập hiện tại của mỗi người dùng.

- /var/log/dmesg – Thư mục này có chứa thông điệp rất quan trọng về kernel ring buffer. Lệnh dmesg có thể được sử dụng để xem các tin nhắn của tập tin này.

- /var/log/secure – Thông điệp an ninh liên quan sẽ được lưu trữ ở đây. Điều này bao gồm thông điệp từ SSH daemon, mật khẩu thất bại, người dùng không tồn tại, vv

- /var/log/mariadb – Nếu MariaDB được cài đặt trên hệ thống thì đây là vị trí tập tin log sẽ được lưu lại.



## **2. Syslog và Rsyslog**

**2.1 Giới thiệu về Syslog**

Syslog là một giao thức client/server là giao thức dùng để chuyển log và thông điệp đến máy nhận log. Máy nhận log thường được gọi là

syslogd, syslog daemon hoặc syslog server. Syslog có thể gửi qua UDP hoặc TCP. Các dữ liệu được gửi dạng cleartext. Syslog dùng cổng 514.


Syslog là một giao thức client/server là giao thức dùng để chuyển log và thông điệp đến máy nhận log. Máy nhận log thường được gọi là

syslogd, syslog daemon hoặc syslog server. Syslog có thể gửi qua UDP hoặc TCP. Các dữ liệu được gửi dạng cleartext. Syslog dùng cổng 514.


Syslog ban đầu sử dụng UDP, điều này là không đảm bảo cho việc truyền tin. Tuy nhiên sau đó IETF đã ban hành RFC 3195 (Đảm bảo tin cậy cho 

syslog) và RFC 6587 (Truyền tải thông báo syslog qua TCP). Điều này có nghĩa là ngoài UDP thì giờ đây syslog cũng đã sử dụng TCP để đảm bảo 

an toàn cho quá trình truyền tin.


Trong chuẩn syslog, mỗi thông báo đều được dán nhãn và được gán các mức độ nghiêm trọng khác nhau. Các loại phần mềm sau có thể sinh ra 

thông báo: auth, authPriv, daemon, cron, ftp, dhcp, kern, mail, syslog, user,... Với các mức độ nghiêm trọng từ cao nhất trở xuống 

Emergency, Alert, Critical, Error, Warning, Notice, Info, and Debug.

**MỨC ĐỘ CẢNH BÁO**

|**Mức cảnh báo**|**Ý nghĩa**|
|emerg|Thông báo tình trạng khẩn cấp|
|alert|Hệ thống cần can thiệp ngay|
|crit|Tình trạng nguy kịch|
|error|Thông báo lỗi đối với hệ thống|
|warn|Mức cảnh báo đối với hệ thống|
|notice|Chú ý đối với hệ thống|
|info|Thông tin của hệ thống|
|debug|Quá trình kiểm tra hệ thống|

**Định dạng chung của một gói tin syslog.**

Định dạng hoàn chỉnh của một thông báo syslog gồm có 3 phần chính như sau, và độ dài một thông báo không được vượt quá 1024 bytes:

```
<PRI> HEADER MSG
```

Phần `PRI` hay `Priority` là một số được đặt trong ngoặc nhọn, thể hiện cơ sở sinh ra log hoặc mức độ nghiêm trọng, là một số gồm 8 bit:

- 3 bit đầu tiên thể hiện cho tính nghiêm trọng của thông báo.

- 5 bit còn lại đại diện cho sơ sở sinh ra thông báo.

Giá trị Priority được tính như sau: Cơ sở sinh ra log x 8 + Mức độ nghiêm trọng.

Ví dụ, thông báo từ kernel (Facility = 0) với mức độ nghiêm trọng (Severity =0) thì giá trị Priority = 0x8 +0 = 0.

Trường hợp khác, với "local use 4" (Facility =20) mức độ nghiêm trọng (Severity =5) thì số Priority là 20 x 8 + 5 = 165.

Vậy biết một số Priority thì làm thế nào để biết nguồn sinh log và mức độ nghiêm trọng của nó. Ta xét 1 ví dụ sau:

Priority = 191 Lấy 191:8 = 23.875 -> Facility = 23 ("local 7") -> Severity = 191 - (23 * 8 ) = 7 (debug)

`HEADER`

Phần `HEADER` thì gồm các phần chính sau:

- Time stamp - Thời gian mà thông báo được tạo ra. Thời gian này được lấy từ thời gian hệ thống ( Chú ý nếu như thời gian của server và thời gian của client khác nhau thì thông báo ghi trên log được gửi lên server là thời gian của máy client)

- Hostname hoặc IP

`MSG`

Phần `Message` hay `MSG` chứa một số thông tin về quá trình tạo ra thông điệp đó. Gồm 2 phần chính:

- Tag field

- Content field

Tag field là tên chương trình tạo ra thông báo. Content field chứa các chi tiết của thông báo

## **2.2 Rsyslog**

Rsyslog - "The rocket-fast system for log processing" được bắt đầu phát triển từ năm 2004 bởi Rainer Gerhards rsyslog là một phần mềm mã nguồn mở sử dụng trên Linux dùng để chuyển tiếp các log message đến một địa chỉ trên mạng (log receiver, log server) Nó thực hiện giao thức syslog cơ bản, đặc biệt là sử dụng TCP cho việc truyền tải log từ client tới server. Hiện nay rsyslog là phần mềm được cài đặt sẵn trên hầu hết hệ thống Unix và các bản phân phối của Linux như : Fedora, openSUSE, Debian, Ubuntu, Red Hat Enterprise Linux, FreeBSD…






