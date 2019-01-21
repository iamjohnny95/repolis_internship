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