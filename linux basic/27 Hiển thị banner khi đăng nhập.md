## **Hiển thì banner mod khi đăng nhập**

**Để hiển thị một thông điệp trước khi đăng nhập**

**Đăng nhập root user. Open 1 file**

```
# vi /etc/issue
```

**Thêm 1 text mới**

```
Welcome to nixCraft Labs!
Today is \d \t @ \n
```
**Thủ tục để thay đổi OpenSSH trước khi đăng nhập banner**

- Đăng nhập root user, tạo file banner

```
# vi /etc/ssh/sshd-banner
```

- Thêm vào file text

```
Hello everybody!
```

- Mở file cấu hình sshd ` /etc/sshd_config`

```
# vi /etc/sshd/sshd_config
```

- Thêm/ Sửa dòng 

```
Banner /etc/ssh/sshd-banner
```

- Lưu và restart sshd server:

```
systemctl restart sshd
```


