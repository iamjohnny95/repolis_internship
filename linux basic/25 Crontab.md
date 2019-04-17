## **Crontab**

### **Dịch vụ Crontab**

- Là dịch vụ chạy ở chế độ background cho phép thực hiện các tác vụ một cách tự động lặp đi lặp lại theo định kỳ

```
# yum install crontabs
# service crond status
```

**Crontab** là file chứa bảng biểu (schedule) của các entries được chạy mỗi người dùng sẽ có một cron schedule riêng trong /var/spool/cron. File này không cho phép tạo hoặc chỉnh sửa trực tiếp với bất kỳ soạn thảo nào ngoài lệnh crontab

**Cấu trúc của crontab** Một crontab có 5 trường xác định thời gian mà lệnh sẽ được chạy định kỳ.

- Nếu cột thời gian được gán giá trị:

	- **Cột 1**: Định nghĩa theo phút. Ta có thể gán từ 0-59

	- **Cột 2**: Định nghĩa theo giờ. Ta có thể gán từ 0-23

	- **Cột 3**: Định nghĩa theo ngày. Ta có thể gán từ 0-31

	- **Cột 4**: Định nghĩa theo tháng. Ta có thể gán từ 1-12

	- **Cột 5**: Định nghĩa theo ngày trong tuần. Ta có thể gán là (Sun,Mon,Tue,Wed...)

	- **Cột 6**: User thực thi lệnh

	- **Cột 7**: Command được thực thi

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

`0 15 * * 1,4 /scripts/script.sh`

Đặt một cron để thực thi vào 12 giờ hằng ngày

`0 12 * * * /scripts/script.sh`

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

**Ví dụ**:

Đặt lịch đến khoảng thời gian bất kỳ ping đến địa chỉ 8.8.8.8

- Tạo 1 file ping.sh đuôi chứa câu lệnh 

- Trong file ping.sh sử dụng câu lệnh trong đó:

```
/bin/ping -c5 8.8.8.8 > /root/ping
```

- Sau đó dùng câu lệnh chmod để cho file quyền excute

- Bước tiếp theo đó vào `crontab -e` gõ

```
40 1 * * * /root/ping.sh 
```






