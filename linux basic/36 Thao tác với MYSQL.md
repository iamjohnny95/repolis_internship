## **MYSQL CƠ BẢN**

**1.Truy cập vào MYSQL SHELL**

`mysql -u root -p` trong đó 

	- `-u root`: đăng nhập tài khoản root

	- `-p`: hiển thị prompt password

**2.Tạo và xóa các DB**

- Liệt kê database show databases

```
MariaDB [(none)] > show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
```

- Tạo một database mới `create database db_name;`

Ví dụ: Tạo một database mới có tên là `mydb`;

```
MariaDB [(none)]> create database db_mydb;
Query OK, 1 row affected (0.00 sec)
```

- Xóa một database `drop database db_name;`

```
MariaDB [(none)]> drop database db_mydb;
Query OK, 0 rows affected (0.00 sec)
```

**3. Làm việc với các DB**

1. Chọn DB cần làm việc với `use db_name`

```
MariaDB [(none)]> use db_mydb;
Database changed
MariaDB [db_2018]> 
```

2. Liệt kê các table trong DB được chỉ định `show tables`

```
MariaDB [db_mydb]> show tables;
Empty set (0.00 sec)
```

3. Tạo một table trong DB

```
MariaDB [db_mydb]> Create table user ( id INT AUTO_INCREMENT KEY , name varchar(20), full_name varchar(50), bd date );
Query OK, 0 rows affected (0.02 sec)
```
Lệnh này bao gồm:

- Tạo một table: user, gồm 4 trường 

- Trường id: tự tăng, và ID cho cách row

- name: giới hạn không quá 20 ký tự 

- full-name: giới hạn không quá 50 ký tự 

- bd: được lưu dưới dạng `yyyy-mm-dd`

Sử dụng `describe user;` để xem các trường được tạo trong table 

4. Them row vào table 

```
INSERT  INTO shop tale_name  (val_feild11,'val_feild2, 'val_feild3'),(val_feild1,'val_feild2',val_feild3);
```

Ví dụ:

```
MariaDB [db_mydb]> INSERT INTO `user` (`id` , `name`, `full_name` , `bd`) VALUE ( "","johnny", "johnny nguyen", '1998-12-30'); 
Query OK, 1 row affected, 1 warning (0.00 sec)
```
5. Hiển thị các row trong một table

```
MariaDB [db_2018]> select * from user;
+----+------+-----------+------------+
| id | name | full_name | bd         |
+----+------+-----------+------------+
|  1 | johnny  | johnny nguyen | 1998-12-30 |
|  2 | mike | mike tyson | 1998-12-30 |
+----+------+-----------+------------+
```

6. Update giá trị một row trong table

```
update `table_name` set `field1` = "val_field1", `field2`= "val_field_2" where `table_name`.`name`='nam2';
```

ví dụ:

```
MariaDB [db_2018]> update `user` set `name` = "son", `full_name`= "nguyen ha son" where `user`.`name`='johnny';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

```
MariaDB [db_2018]> select * from user;
+----+------+-----------+------------+
| id | name | full_name | bd         |
+----+------+-----------+------------+
|  1 | son  | nguyen ha son | 1998-12-30 |
|  2 | mike | mike tyson | 1998-12-30 |
+----+------+-----------+------------+
2 rows in set (0.00 sec)
```

- Xóa Row 

```
DELETE from [table name] where [column name]=[field text];
```

7. Thêm, xóa column

- `ALTER TABLE table_name.n_field_name ADD email VARCHAR(40) afer field_name;` # thêm một column mới 

- `ALTER TABLE table_name DROP field_name;`  # xóa column

ví dụ 

```
MariaDB [db_2018]> alter table user add email varchar(30) after full_name;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

