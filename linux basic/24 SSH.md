## **SSH**

### **Cài đặt SSH key trên Centos 7**

### **Tạo cặp khóa RSA** 

**Bước một tạo một cặp khóa trên máy khách. `keygen` sẽ sinh ra khóa công khai và gửi đến máy client.**

```
ssh-keygen
```

- Theo mặc định, `ssh-keygen` sẽ tạo ra một cặp khóa RSA 2048-bit, đủ an toàn cho hầu hết các trường hợp sử dụng (bạn có thể tùy ý vượt qua cờ -b 4096 để tạo ra một khóa 4096 lớn hơn).

- Sau khi nhập lệnh, bạn sẽ thấy dấu nhắc sau:

```
Output
Enter file in which to save the key (/your_home/.ssh/id_rsa):
```

- Nhấn `Enter` để lưu cặp khóa vào thư mục con .ssh/ trong thư mục chính của bạn, hoặc chỉ định một đường dẫn thay thế.

- Sau đó, bạn sẽ thấy dấu nhắc sau:

```
Output
Enter passphrase (empty for no passphrase):
```

- Tại đây bạn tùy ý có thể nhập cụm từ mật khẩu bảo mật, được đánh giá cao. Cụm từ mật khẩu thêm một lớp bảo mật bổ sung để ngăn người dùng trái phép đăng nhập.

- Bạn sẽ thấy kết quả sau:

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

**Bước 2: Sao chép Public Key tới máy chủ CentOS**

- Cách nhanh nhất để sao chép khóa công khai của bạn đến máy chủ CentOS là sử dụng một tiện ích được gọi là `ssh-copy-id`. Do tính đơn giản của nó nên phương pháp này được đánh giá cao nếu có. Nếu bạn không có `ssh-copy-id` có sẵn trên máy khách, bạn có thể sử dụng một trong hai phương pháp thay thế được cung cấp trong phần này (sao chép qua SSH dựa trên mật khẩu hoặc tự sao chép khóa.

**Sao chép Public Key của bạn sử dụng `ssh-copy-id`**

- Công cụ `ssh-copy-id` được bao gồm theo mặc định trong nhiều hệ điều hành, vì vậy bạn có thể có nó trên hệ thống cục bộ . Để phương pháp này hoạt động, bạn phải có quyền truy cập SSH dựa trên mật khẩu vào máy chủ của mình. Để sử dụng tiện ích này, bạn chỉ cần chỉ định máy chủ từ xa mà bạn muốn kết nối và tài khoản người dùng mà bạn có mật khẩu truy cập vào SSH. Đây là tài khoản mà SSH Key công khai của bạn sẽ được sao chép.

- Cú pháp là:

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



