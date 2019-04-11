## Sử dụng RSYNC để đồng bộ dữ liệu trên linux
- RSYNC là một công cụ mạnh mẽ để copy file và đồng bộ dữ liệu giữa linux với linux.
## Các tính năng nổi bật của RSYNC 
- Sao chép cả sysbolic link, user, group, permission giúp bảo toàn dữ liệu.
- rsync nhanh hơn SCP, nó dùng thuật toán thông minh chỉ sao lưu những dữ liệu thay đổi.
- rsync nén dữ liệu trên server trước khi gửi đi.
- Tự xóa dữ liệu nếu dữ liệu đó không tồn tại trên source giúp đồng bộ dữ liệu giữa hai máy chủ linux từ xa.
- rsync kết hợp SSH bảo mật dữ liệu truyền trên internet.

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/rsync.png)]


## Cài đặt RSYNC
-`Rsync` không chỉ đảm bảo một hoặc nhiều tập tin giống nhau ở thư mục nguồn và thư mục đích, nó sử dụng một thuật toán phức tạp để so sánh các phần của mỗi tập tin, do đó làm giảm đáng kể thời gian cần thiết để đồng bộ hóa. Ngoài ra, RSYNC nén dữ liệu để giảm băng thông và sử dụng `ssh` trên hệ thống để bảo mật.

 `yum install rsync`

## Cách sử dụng RSYNC

- Cú pháp sử dụng:

`#rsync option source destination`

Trong đó:

**Source**: thư mục chứa dữ liệu gốc muốn đồng bộ, nơi truyền dữ liệu.

**Destination**: nơi sẽ chứa dữ liệu đồng bộ đến, nơi nhận dữ liệu.

**Option**: các tham số để tùy biến rsync khi đồng bộ dữ liệu.

-`a`: option này sẽ bảo toàn user, group, permission,symbolic link của dữ liệu

-`v`: show trạng thái truyền tải file ra màn hình để bạn theo dõi.

-`h`: kết hợp với -v để định dạng dữ liệu show ra dễ nhìn hơn.

-`z`: nén dữ liệu trước khi truyền đi giúp tăng tốc quá trình đồng bộ file.

-`e`: sử dụng giao thức SSH để mã hóa dữ liệu.

-`P`: Option này dùng khi đường truyền không ổn định, nó sẽ gửi tiếp các file chưa được gửi đi khi có kết nối trở lại.

--`delete`: xóa dữ liệu ở destination nếu source không tồn tại dữ liệu đó.

--`exclude`: loại trừ ra những dữ liệu không muốn truyền đi, nếu bạn cần loại ra nhiều file hoặc folder ở nhiều đường dẫn khác nhau thì mỗi

cái bạn phải thêm –exclude tương ứng.

***VÍ DỤ***:

- Đồng bộ hai thư mục local 

```
rsync -azv --progress /root/son/ /tmp/test/
```
Đồng bộ dữ liệu từ thư mục `/root/son` đến thư mục `/tmp/test`

- Đồng bộ hai thư mục từ xa
Server:/root/son => Client:/root/test
Thực hiện rsync trên Client

```
rsync -avzP --delete -e ssh root@192.168.220.13:/root/son /root/test

```

**Chứng thực RSA**

Gen cặp khóa rsa độ dài 2048 bit trên client

```
# ssh-keygen -t rsa -b 2048
```

Copy public key id_rsa.pub lên server

```
# ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.220.13
```
## Dịch vụ crontab
- Là dịch vụ chạy ở chế độ background cho phép thực hiện các tác vụ một cách tự động lặp đi lặp lại theo định kỳ 
```
# yum install crontabs
# service crond status
```
**crontab** là file chứa bảng biểu (schedule) của các entries được chạy 
mỗi người dùng sẽ có một cron schedule riêng trong /var/spool/cron. File này không cho phép tạo hoặc chỉnh sửa trực tiếp với bất kỳ soạn thảo nào ngoài lệnh crontab
**Cấu trúc của crontab** 
Một crontab có 5 trường xác định thời gian mà lệnh sẽ được chạy định kỳ 

Nếu cột thời gian được gán giá trị:
- **Cột 1:** Định nghĩa theo phút. Ta có thể gán từ 0-59
- **Cột 2:** Định nghĩa theo giờ. Ta có thể gán từ 0-23
- **Cột 3:** Định nghĩa theo ngày. Ta có thể gán từ 0-31
- **Cột 4:** Định nghĩa theo tháng. Ta có thể gán từ 1-12
- **Cột 5:** Định nghĩa theo ngày trong tuần. Ta có thể gán là (Sun,Mon,Tue,Wed...)
- **Cột 6:** user thực thi lệnh
- **Cột 7:** Command được thực thi 

**Cấu hình Crontab hệ thống**
 - Crontab hệ thống gồm các thư mục có thể cài đặt chương trình định kỳ tương ứng :/etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, /etc/cron.monthly

 `# vi /etc/crontab`

 **Các lệnh thay đổi nội dung file crontab**

 `Crontab -u username -l: liệt kê crontab`

 `Crontab -u username -e: thêm mới crontab`

 `Crontab -l: liệt kê crontab user đang login`

 `Crontab -r: xóa crontab`

**Đặt lịch crontab**

`# crontab -e`

Đặt lịch 1 cron để thực thi vào	15 giờ thứ 2 và thứ 5 mỗi tuần 
```
0 15 * * 1,4 /scripts/script.sh
```

Đặt một cron để thực thi vào 12 giờ hằng ngày 
```
0 12 * * * /scripts/script.sh
```

Đặt một crontab để vào mỗi phút.
```
0-59 * * * * /scripts/script.sh

*/1 * * * * /scripts/script.sh
```

Đặt một crontab để vào mỗi năm phút
```
*/5 * * * * /scripts/script.sh
```

Đặt một crontab vào 5 tiếng 1 lần 
```
0 */5 * * * /scripts/script.sh
```

Đặt 1 crontab để thực thi vào 8h10, 10h10, 12h10, 14h10, 16h10
```
10 8,10,12,14,16 * * * /scripts/script.sh
```

Đặt 1 crontab để thực thi mỗi 30 phút 1 lần 
```
0,30 * * * * /scripts/script.sh
``` 

Đặt 1 crontab để thực thi mỗi 15 phút một lần 
```
0,15,30,45 * * * * /scripts/script.sh
```

Đặt 1 crontab để thực thi mỗi 30 giây
```
* * * * * sleep 30; /scripts/script.sh
```

Hiển thị crontab của các user trong /var/spool/cron

```
# ls -l /var/spool/cron
```

Có thể tạo file Crontab trong thư mục /etc/cron.d

```
# vi /etc/cron.d/test
```

## **Kết hợp RSYNC với CRONTAB**

Để hệ thống đồng bộ thường xuyên chúng ta sử dụng kết hợp giữa crontab với RSYNC

- Đầu tiên tạo một file .sh

```
vi RSYSNC.sh
```

- Trong file đó ta cấu hình bên trong file câu lệnh đồng bộ dữ liệu

```
rsync -avzP --delete -e ssh root@192.168.220.13:/root/son /root/test > RSYNC
```

Sau đó cho quyền thực thi 

```
chmod +x RSYNC.sh
```
Gõ câu lệnh để chạy script

```
sh ./RSYNC.sh
```

Cuối cùng gõ lệnh `crontab -e` để chạy để edit crontab. Tự động đồng bộ hệ thống 1 phút 1 lần

```
*/1 * * * * /root/RSYNC.sh
```











## Nén dữ liệu:

- file dữ liệu thông thường được nén để tiết kiệm dung lượng của ổ đĩa và giảm thời gian truyền file trên mạng. Linux sử dụng 1 số phương pháp để thực hiện nén. 2 kiểu nén file là gzip và bzip2

 - Gzip:**Nén** 1 file dưới định dạng .gz `Gzip -c abc.txt > abc.txt.gz`
        **Giải nén** `Gzip -dv abc.txt.gz` 

 - Bzip2:**Nén** `Bzip2 -c abc.txt > abc.txt.gz`
 		 **Giải nén** `Bzip2 -dv abc.txt.bz`

 - Nén cả file thư mục thì ta sử dụng lệnh tar

   - **Nén** `tar -cvf /root/sondz.tar /root/sondz` , còn muốn nén theo chuẩn gz thì sử dụng câu lệnh `tar -czvf /root/sondz.tar.gz /root/sondz`, nén sang chuẩn bz thì sử dụng câu lệnh `tar -cjvf /root/sondz.tar.bz /root/sondz`

   - **Giải nén** `tar -xvf sondz.tar.gz` 




