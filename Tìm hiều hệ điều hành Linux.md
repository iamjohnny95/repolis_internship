## Cấu trúc phân lớp 
- Trên nhiều  hệ điều hành, bao gồm  cả linux , file system thường có dạng cây. Linux  filesystem sẽ thường được bắt đầu từ thư mục root. Tất cả các thư mục khác là con của thư mục này. Các định dạng file system mà linux sp là: ext2, ext3, ext4, XFS, JFS, btrfs
- 1./ (root): thư mục gốc, thư mục cha toàn bộ hệ thống
- 2./ bin: chứa các tệp binary, chứa các lệnh của người dùng và toàn hệ thống
- 3./ boot: chứa các thư mục và tệp tin trong bootloader
- 4./dev: chứa các thiết bị ngoại vi, thiết bị đầu cuối gắn vào hệ thống 
- 5./etc: chứa các câu hình của package, và system
- 6./home: chứa các tập tin, thư mục người dùng trên hệ thống 
- 7./lib: chứa các thư viện cho các chương trình trong /bin và /sbin
- 8./media: là các điểm gắn kết system với các thiết bị bên ngoài 
- 9./mnt: điểm  gắn kết cho phép  gắn trực tiếp filesystem
- 10./opt: chứa các gói phần mềm từ các package đã cài đặt 
- 11./tmp: chứa các file tạm thời, của các package đang chạy, sẽ mất đi khi root
## Thư mục  home:
- Trong những hệ thống UNIX, mỗi người dùng có đường dẫn sở hữu của họ. Thông thường được đặt /home.  Thư mục /home thường được mount 1 filesystem riêng biệt trên partition 

## thư mục variable ( thư mục biến động )

-   Thư mục / var chứa các tệp sẽ thay đổi về kích thước và nội dung khi hệ thống đang chạy

```
- System log files: /var/log
- Packages files: /var/lib
- Print queues: /var/spool
- Temp files: /var/tmp
- FTP home directory: /var/ftp
- Web Server directory: /var/www

```

##File System Table

`etc/fstab`  là file dạng văn bản (plain text) cho biết các điểm mount vào filesystem


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM1NTQyNTg2MywtMTI1MTkwNjU2NSwtMT
c4MTMyNDI0Niw0Nzk2MDcwNDIsMTA3Mjk4ODg5NCwtMTg4MDc3
NDMzLDE0OTkxNzE0NDgsMTkzMDE2ODAxMCwtMzIxNTYzMzQ4LD
E3MzQ0MDQ0MjgsMTU2NzA1NjIyMCwtMTIyMzUyOTIwMywtNjE0
MTY1MzYyLC0xNTU3MjIzODk2LDEwOTc5OTc4ODUsNDQxNjkzMD
UyLDE4NTY4NzEyODNdfQ==
-->