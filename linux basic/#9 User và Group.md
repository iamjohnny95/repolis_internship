# **User và Group**
- Linux là một hệ điều hành nhiều người dùng nơi mà hơn một người dùng có thể đăng nhập vào cùng một thời điểm. câu lệnh `who` sẽ liệt kê danh sách những người dùng đã đăng nhập hiện tại. Để nhận dạng người dùng hiện tại, sử dụng câu lệnh `whoami`
- Linux sử dụng group để tổ chức người dùng. Những group thu thập các tài khoản với ủy quyền chia sẻ. Thành viên điều khiểm group là quản trị viên thông qua file `etc/group`, file sẽ show ra danh sách các groups và thành viên của group. Mặc định, mọi thành viên phụ thuộc 1 default hay primary group. Khi một tài khoản đăng nhập vào, các thành viên được đặt cho họ primary group và tất cả các thành viên tham gia sẽ cùng level về truy cập và đặc quyền. Ủy quyền trên một vài file và thư mục có thể đã được sửa tại group level.

- Tất cả user Linux đang được gắn 1 user ID riêng - UID. GID có một định nghĩ tương tự như UID nhưng là mức nhóm. Về mặt lịch sử, RedHat dựa trên bản phân phối bắt đầu uid là 500. Những bản phân phối khác bắt đầu là 1000. Những con số đã được liên kết với tên thông qua file `/etc/passwd` và `/etc/group` .Group được sử dụng để thiết lập những user liên quan đến mục đích truy cập, quyền hạn và bảo mật. 

- chỉ user root có thể thêm và xóa các user và group. Thêm 1 user mới với `usseradd` và xóa user với command `userdel`. 
```
# useradd adriano
# cat /etc/passwd | grep adriano
adriano:x:1000:1000::/home/adriano:/bin/bash
# ls -lrta /home/adriano/
total 16
-rw-r--r--. 1 adriano adriano 231 Sep 26 03:53 .bashrc
-rw-r--r--. 1 adriano adriano 193 Sep 26 03:53 .bash_profile
-rw-r--r--. 1 adriano adriano  18 Sep 26 03:53 .bash_logout
drwxr-xr-x. 3 root    root     20 Feb 17 17:48 ..
-rw-------. 1 adriano adriano   9 Feb 17 17:49 .bash_history
drwx------. 2 adriano adriano  79 Feb 17 17:49 .
```
- Xóa user
```
# userdel adriano
# cat /etc/passwd | grep adriano
# ls -lrta /home/adriano/
total 16
-rw-r--r--. 1 1000 1000 231 Sep 26 03:53 .bashrc
-rw-r--r--. 1 1000 1000 193 Sep 26 03:53 .bash_profile
-rw-r--r--. 1 1000 1000  18 Sep 26 03:53 .bash_logout
drwxr-xr-x. 3 root root  20 Feb 17 17:48 ..
-rw-------. 1 1000 1000   9 Feb 17 17:49 .bash_history
drwx------. 2 1000 1000  79 Feb 17 17:49 .
```
- Câu lệnh `id` đưa ra thông tin về user hiện tại. Nếu thêm tên của 1 user khác, thông tin sẽ hiện ra của user đó.
```
# id
uid=0(root) gid=0(root) groups=0(root)
# id adriano
uid=1000(adriano) gid=1000(adriano) groups=1000(adriano)
```
- Sử dụng `passwd` để thay đổi mật khẩu

- Thêm group mới và xóa group

```
$ groupadd newgroup
$ groupdel newgroup
```
- Thêm user và group

```
$ useradd bo
$ groupadd newgroup
$ usermod -G newgroup bo
$ groups bo 
bo : bo newgroup
$ usermod -g newgroup bo
$ groups bo 
bo : newgroup
```
- Xóa user 
```
userdel [name]
```

## **Root User**

- Root là tài khoản có toàn quyền trên hệ thống. Các hệ thống khác thường gọi là administrator account; Linux thường gọi là superuser account. Phải thật cẩn thận khi cấp quyền truy cập root cho các user. Sử dụng `su` để chuyển đổi giữa các user.

## **Backup User Root**

- Để tạo ra user root thì phải chỉnh uid và gid bằng 0
 
 `Useradd -u 0 -g 0 -o admin`

 - Để đặt mật khẩu cho admin thì sử dụng lệnh 

 `Passwd admin `


## **Các file chứa thông tin và mật khẩu của các user**

- File chứa thông tin về tài khoản các user trên linux là file `/etc/passwd`

Các trường trong file `etc/passwd`


```
 root:x:0:0:root:/root:/bin/bash

```

- Trong đó root là tài khoản tên root. :x là đã mã hóa mật khẩu trong file `etc/<shadow>` . Tiếp theo là 2 giá trị uid và gid. Cuối cùng là 2 giá trị tên của user và group đã được lưu trong /bin/bash

- File chứa thông tin mật khẩu được mã hóa là `etc/shadow `

```
[root@localhost /]# cat /etc/shadow
root:$6$zRj5lAjC$yPyG5ETmtxZN3QfnsSIAPBW11Q2nQGLgXuilKQN1fVJuCLDSrGwy1XYKw0SboMGeaMta9NKJ8hM/yU9owbzQK1:17920:0:99999:7:::
```

1. Trường đầu tiên, đó chính là username root
2. Trường thứ 2 đó là trường password đã được mã hóa $6$zRj5lAjC$yPyG5ETmtxZN3QfnsSIAPBW11Q2nQGLgXuilKQN1fVJuCLDSrGwy1XYKw0SboMGeaMta9NKJ8hM/yU9owbzQK1:17920:0:99999:7:::
 - Được phân cách thành 3 trường bởi $.

  - Trường 1: Cho biết thuật toán mã hóa.

  ```
  $1 : MD5
  $2 : blowfish
  $2a : eksblowfish
  $5 : sha256
  $6 : sha512
  ```
  - Trường 2:Là một chuỗi dữ liệu ngẫu nhiên (salt) kết hợp với pass người dùng, tăng tính bảo mật trong hàm băm.

  - Trường 3: Giá trị băm của salt với password




Trong file này mật khẩu sử dụng thuật toán SHA 512 để băm giá trị khóa 

- 3 file bash trong /home/[user_name]
```
~/.bash_profile
       file khởi tạo thông tin cá nhân, đã được thực thi đến login shells
~/.bashrc
       chứa lịch sử hoạt động trên user đó
~/.bash_logout
       Shell đăng nhập cá nhân sẽ quét file ,thực thi khi shell đăng nhập tồn tại

```

## **Reset password**
**Trên centos**
Khi khởi động đến giao diện 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/RSP/1.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/RSP/1.png)

Chọn `e` ta sẽ thấy giao diện 


[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/RSP/2.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/RSP/2.png)

Di chuyển xuống gần cuối tìm dòng có hai từ `rhgb` và `quiet`, xóa chúng đi 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/RSP/3.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/RSP/3.png)

Và thêm vào cuối dòng đó đoạn sau: `rd.break enforcing=0`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/RSP/4.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/RSP/4.png)

Cuối cùng ấn `ctrl +x` để load system, sau đó sẽ vào được giao diện như dưới đây:

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/RSP/5.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/RSP/5.png)

mount lại:

`mount -o remount,rw /sysroot`

Chuyển file system của root bằng lệnh: chroot /sysroot

Sau đó đặt lại password bằng lệnh `passwd`

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/RSP/6.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/RSP/6.png)








## **Tạo group**

- Tạo 1 group về vận hành hệ thống 

```

[root@localhost /]# groupadd VHHT
```
- Sau đó tạo ra các user trong hệ thống thì sử dụng câu lệnh sau:
```
[root@localhost /]# useradd -G VHHT A
[root@localhost /]# useradd -G VHHT B
[root@localhost /]# useradd -G VHHT C
```

## **Chuyển tài khoản**
 - Sử dụng lệnh `su` . Command:

 ```
 su - [tên tài khoản]

```

## **Sudo**

- Sudo được dùng khi ta muốn thực thi một lệnh trên Linux với quyền của một user khác. Nếu được cho phép, ta sẽ thực thi một lệnh như là người quản trị hay một user nào khác. Các khai báo “ai được làm gì” đặc tả trong file `/etc/sudoers` 

- Sửa lệnh trong Sudo 

Cú pháp:

```
User ALL = [đường dẫn]
```

Thêm sau mục ` ## root to run any commands anywhere`

Muốn tạo 1 list các đường dẫn riêng của mình cho một nhóm thì ta làm các bước sau 

Ở trên thì chỉnh sửa câu lệnh
```
Cmnd _Alias ADMINCOMMAND = /bin/mound , /bin/umount,…
```

Ở cuối trang muốn cho group Abc thực thi mà k bị hỏi pass còn user sẽ không có %

```
%group ALL =NOPASSWD: ADMINCOMMAND
```
## **Biến môi trường** 
- Một số biến đáng chú ý là: 
   - SHELL: cho biết shell nào đang được thực thi. 
   - $echo $SHELL # thường là /bin/bash 
   - HOME: chỉ ra thư mục Home của bạn 
   - PATH:Biến môi trường PATH là một danh sách được sắp xếp theo thứ tự các thư mục được quét khi một lệnh được đưa ra để tìm chương trình hoặc tệp lệnh thích hợp để chạy. Mỗi thư mục trong đường dẫn được phân cách bằng dấu hai chấm. Tên thư mục trống cho biết thư mục hiện tại tại bất kỳ thời điểm nào.

   Ví dụ: 
   ```
   PATH='/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/X11R6/bin'​
   ```
   - Biến môi trường `PS` được sử dụng để tùy chọn các chuỗi ghi chú của bạn trên của sổ terminal để hiện thị ra thông tin bạn muốn. `PS` à biến prompt chính để điều khiển command line prompt trông như thế nào. Các ký tự đặc biệt trong PS1:

   |Ký tự|Sử dụng|
   |-----|-------|
   |\u|Username|
   |\h|Hostname|
   |\w0|Đường dẫn hiện tại|
   |!|lịch sử của câu lệnh|
   |\d|Ngày|

```
 [root@localhost ~]# export PS1='\d-\u@\h:\w$ '
 Wed Jan 30-root@localhost:~$ 
```


## **Alias Command**

- Bạn sử dụng những câu lệnh ấy lặp đi lặp lại nhiều lần trong một ngày. Khi đó rất có thể bạn sẽ cần đến alias để giảm bớt thời gian cho việc gõ đi gõ lại các câu lệnh đó.
- Hiểu một cách nôm na, alias được sử dụng trong chế độ dòng lệnh giống như việc bạn viết tắt khi ghi chép bằng giấy bút vậy. Với alias bạn có thể thay cả 1 câu lệnh hoặc 1 nhóm câu lệnh với chỉ 1 từ hay vài chữ cái, từ đó tiết kiệm cho bạn rất nhiều thời gian khi làm việc với chế độ dòng lệnh. Ví dụ bạn có thể chỉ cần gõ `update	` thay vì gõ cả câu lệnh `yum install mysql` 

- Cú pháp:
```
alias alias_name='aliased_command --options'
```
-Ví dụ:

```
alias e='echo'
```












