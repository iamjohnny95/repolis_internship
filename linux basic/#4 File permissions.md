# File permissions
- Trong linux và những hệ điều hành Unix khác, mỗi file được liên kết với 1 người dùng người sở hữu file đó. Mỗi file cũng được liên kết với 1 group, các quyền hạn được thực thi lên file hay thư mục: read, write và excute.
  - chown: sử dụng để thay đổi người dùng của file hay đường dẫn
  - chgrp: sử dụng để thay đổi group của file sở hữu
  - chmod: sử dụng để thay đổi quyền trên file

- file có 3 quyền là: read(r),write(w),excute(x). Những quyền này ảnh hưởng đén 3 nhóm của sở hữu: user(u), group(g), other(o). mỗi nhóm có tối đa 3 quyền hạn
- Có một số cách khác để sử dụng lệnh `chmod`. Cho ví dụ, để thêm quyền excute cho user sở hữu file đó
```
$ ls -l test1
-rw-rw-r-- 1 joy caldera 1601 Mar 9 15:04 test1
$ chmod u+x test1
$ ls -l test1
-rwxrw-r-- 1 joy caldera 1601 Mar 9 15:04 test1
```
- Ngoài các thể hiện quyền bằng chữ t cũng có các quy ước phân quyền bằng số
  - 4 là quyền read(r)
  - 2 là quyền write(w)
  - 1 là quyền excute(x)
 - Như vậy 7 là read + write + excute, 6 là read +write, và 5 nghĩa là read +excute
 ```
$ chmod 755 test1
$ ls -l test1
-rwxr-xr-x 1 joy caldera 1601 Mar 9 15:04 test1
```
## Một số quyền nâng cao và đặc biệt:
- **SUID** (Set User ID): Nếu **SUID** bit được thiết lập cho một ứng dụng, những file có thể thực thi nào đó điều này có nghĩa là một người dùng khác không phải chủ sở hữu của ứng dụng cũng có thể chạy như chính chủ sở hữu. Ví dụ:
```
$ ls /usr/bin/passwd
-rwsr-xr-x 1 root root 31640 Сен 15 00:51 /usr/bin/passwd
```
**rws**: nghĩa là câu lệnh thay đổi passwd đã được thiết lập SUID bit. Tuy **passwd** thuộc **root** nhưng vì đã được thiết lập SUID bit nên người dùng khác cũng có thể thực hiện **passwd** 
- **SGID** : Giống như SUID nhưng dành cho nhóm 
- Để thiết lập **SUID** và **SGID** sử dụng lệnh:
`$ chmod u+s yourfile`
và
`$ chmod g+s yourfile`
- **Sticky Bit**: người dùng chỉ có thể xóa những file mà chính họ tạo ra trong thư mục được thiết lập **Sticky bit**. Để bật **Sticky bit** cho một thư mục chúng ta thực hiện:
`$ chmod +t stickyfolder`

- Ngoài ra người ta sử dụng thêm một bit thứ 4 để biểu diễn suid, sgid và sticky bit

|**Permision**|**Number**|
|suid|4000|
|sgid|2000|
|sticky|1000|

## **Giá trị umask**

- Trong Linux, khi một file hay một thư mục được tạo ra thì các quyền hạn truy cập đối với chúng là (read, write, execute) cho các chủ thể (owner, group, other) sẽ được xác định dựa trên hai giá trị là quyền truy nhập cơ sở (base permission) và mặt nạ (mask).

  -  Base Permission là giá trị được thiết lập sẵn từ trước, và ta không thể thay đổi được

- Đối với file thông thườnggiá trị base perm là 666 (rw-rw-rw-)

- Đối với thư mục (file đặc biệt) giá trị base perm là 777 (rwxrwxrwx)

   - Mask là giá trị đựợc thiết lập bởi người dùng bằng lệnh `umask`

 - Vậy các quyền được tạo ra này được thiết lập như thế nào? Có thể sửa được không? Tất nhiên là có thể. Hãy sử dụng umask (tạm dịch là mặt nạ).Quyền truy cập cho phép là kết quả giữa phép toán sau:
```
 Quyền truy cập cho phép = "quyền truy cập mặc định" AND {NOT (Giá trị umask)}
 ```

- Chú ý:
  - Bạn có thể đặt umask=000 sau đó tạo thử file và thư mục để biết được quyền truy cập mặc định.

  - Giá trị mặc định của umask thường được đặt trong file .bashrc hay .bash_profile trong thư mụcHOME và giá trị thường là 022. Nếu vậy nó sẽ loại bỏ quyền ghi dành cho nhóm và other từ quyền mặc định. Ở ví dụ trên thì kết quả là 644.

  - Nếu bạn chỉ định các quyền khi tạo thì umask sẽ không có tác dụng gì cả:

  ```
  mkdir -m 744 demo # sẽ có quyền rwx r-- r--​
  ```
  
