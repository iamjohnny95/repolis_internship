# Basic command
## Xác định các ứng dụng 
- Phụ thuộc vào sự phân phối cụ thể, chương trình và các gói phần mềm có thể được cài đặt trong các đường dẫn khác nhau. Thực thi các chương trình trong các đường dẫn
```
  -/bin
  -/usr/bin
  -/sbin
  -/usr/sbin
  -/opt
```
- Các để tra đường dẫn của 1 lệnh sử dụng câu lệnh which
```
$ which diff
/usr/bin/diff
```
- Truy cập thư mục

cd : di chuyển tới thư mục home

cd / : di chuyển tới thưc mục root

cd - : di chuyển tới thưc mục trước

cd .. : di chuyển tới thư mục cha

cd meditech : di chuyển tới thư mục con có tên "meditech"

cd /usr/bin/share : di chuyển tới thư mục /user/bín/share

- Hiển thị thông tin thư mục

ls : Liệt kê tất cả các tập tin và thư mục

ls -a : Liệt kê tất cả các tập tin bao gồm các tệp và thư mục ẩn

ls -l : Liệt kê quyền truy cập, người tạo, nhóm, kích cỡ ( size ) , thời gian chỉnh sửa gần nhất, tên của tất cả tập tin và thư mục

pwd : hiển thị thư mục hiện tại


## ommand history

- Bash sẽ lưu trữ tất cả các lệnh đã gõ trong bộ đệm history, bạn có thể gọi lại các lệnh trước đó bằng cách sử dụng phím `up` và `down`. Để xem tất cả các lệnh đó, bạn có thể sử dụng command `history` . Danh sách các lệnh được hiển thị với lệnh gần đây nhất sẽ xuất hiện từ cuối lên. Thông tin này lưu trữ trong file `~/.bash_history`. Một số biến môi trường có thể sử dụng để lấy thông tin này:

|Variable|Usage|
|----|----|
|HISTFILE|stores the location of the history file|
|HISTSIZE|stores the maximum number of lines in the history file for the current session|

- Một số cú pháp được sử dụng các lệnh trước đó 

|Syntax|Usage|
|----|----|
|!!|Execute the previous command|
|!|Start a history substitution|
|!$|Refer to the last argument in a line|
|!n|Refer to the n-th command line|
|!string|Refer to the most recent command starting with string|

- Để hiển thị cả ngày tháng gõ lệnh đó sử dụng 

```
HISTTIMEFORMAT="%d/%m/%y %T "
```

- Xóa history file

```
history -c
```

- Xóa dòng theo số dòng
```
history -d 121
```

- Hiển thị 5 dòng thôi

```
history 5
```

- Để lưu cả các lệnh lặp nhau liên tiếp sử dụng:

```
export HISTCONTROL=dups
```

- Nếu muôn bỏ các lệnh lặp đó thì đổi lại là:

```
export HISTCONTROL=ignoredups
```

- Với quyền root, có thể xem lịch sử của các user khác

```
grep -e "$pattern" /home/*/.bash_history

```
edit from origin main branch
