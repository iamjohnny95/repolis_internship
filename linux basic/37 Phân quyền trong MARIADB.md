## **Người dùng và phân quyền trong MARIADB**

**Phân quyền**

- Sau khi tạo người dùng mới, cần phải set quyền cho nó để kiểm soát hành vi của người dùng. 

- Cú pháp cấp quyền user như sau: `GRANT [loại quyền] ON [tên database].[tên table] TO 'username'@'localhost';`

- Cú pháp thu hồi quyền user như sau: `REVOKE [loại quyền] ON [tên database].[tên table] TO 'username'@'localhost';` trong đó.

	- Loại quyền - các quyền sẽ cấp cho user. Bạn có thể cung cấp nhiều loại quyền cho user, được ngăn cách bằng dấu phẩy. Một số quyền phổ 

	biến:

	ALL PRIVILEGES - cấp tất cả quyền cho user.

	CREATE - cho phép tạo database và table

	DROP - cho phép xóa database(DROP) và table

	DELETE - cho phép xóa các dòng trong table

	INSERT – cho phép thêm dòng vào table.

	SELECT – cho phép đọc (select) dữ liệu trong database.

	UPDATE – cho phép cập nhật dòng trong table.

	GRANT OPTION – cho phép cấp hoặc thu hồi quyền của user khác.

- Tên database – tên database sẽ cấp quyền cho user. Có thể dùng dấu * để cấp quyền cho tất cả database.

- Tên table - tên table sẽ cấp quyền cho user. Có thể dùng dấu * để cấp quyền cho database.

- Để quyền có tác dụng sau khi phân quyền cần thực hiện `FLUSH PRIVILEGES;`

**3.Ví dụ phân quyền**

- Cấp tất cả quyền cho user trên một db `GRANT ALL PRIVILEGES db.* to 'johnny'@'localhost'`

- Cấp quyền insert cho user trên một table cụ thể `GRANT INSERT db.table to "johnny"@localhost`

- Cấp tất cả quyền trên tất cả DB GRANT ALL PRIVILEGES *.* to "johnny"@'localhost'






