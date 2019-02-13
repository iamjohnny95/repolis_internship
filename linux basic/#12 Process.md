# **Linux processes**

## **Tiến trình là gì**

Hệ thống sẽ không thực sự quản lý toàn bộ các chương trình, mà chỉ quản lý khi nó được thực thi. Một chương trình để có thể thực thi được trên bất cứ một hệ điều hành nào thì nó đều phải ở dạng mã máy, mỗi chương trình chưa rất nhiều các đoạn mã máy (hay mã chỉ dẫn) giúp cho máy tính có thể biết được chương trình sẽ làm gì. Các đoạn mã này sẽ được nạp vào bộ nhớ khi thực thi, được cấp phát vùng hoạt động, thời gian thực thi .... Và khi điều này xảy ra, thay vì gọi là chương trình, ta có một thuật ngữ khác là tiến trình. Và chính xác thì các tiến trình này là những thứ được quản lý bởi một hệ thống/hệ điều hành Linux (hoặc Windows hay OSX)

## **Những tiến trình đang hoạt động**

Khi một hệ thống đã vận hành, có rất nhiều chương trình đã và đang hoạt động cùng nhau, cùng phối hợp để khiến cho hệ thống có thể giúp người dùng xử lý các công việc. Các bản phân phối Linux cũng giống như các hệ điều hành hiện đại ngày nay, hoạt động theo cơ chế đa nhiệm, tức là trong cùng 1 thời điểm có thể có nhiều chương trình cùng (có vẻ) thực thi tại 1 thời điểm. Tất nhiên thực tế điều này không bao giờ xảy ra, các chương trình đã được phân chia thời gian hoạt động và hệ điều hành điều phối hoạt động tốt đến mức ta không nhận ra được các chương trình thực tế đang chạy tuần tự mà nghĩ rằng nó đang chạy song song.

Ngoài sự đa nhiệm, Linux còn hỗ trợ cơ chế đa người dùng, tức là tại 1 thời điểm, có thể có nhiều chương trình được hoạt động với người dùng là những người khác nhau. Hệ điều hành quản lý tất cả các tiến trình này và vẫn đảm bảo trải nghiệm là đồng đều giữa các người dùng cũng như giữa các chương trình. Một chương trình đặc biệt là top có thể giúp ta biết được hệ thống hiện tại có các chương trình nào đang hoạt động.

```
top - 09:42:02 up 9 min,  2 users,  load average: 0.02, 0.15, 0.13
Tasks:  99 total,   2 running,  97 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  1015296 total,   771288 free,   111924 used,   132084 buff/cache
KiB Swap:  3145720 total,  3145720 free,        0 used.   748776 avail Mem
```

Lệnh `top` cho ta biết khá nhiều thông tin của các tiến trình

- Dòng thứ nhất cho biết thời gian `uptime` (từ lúc khởi động) cũng như số người dùng thực tế đang hoạt động.

- Dòng thứ hai là thống kê về số lượng tiến trình, bao gồm tổng số tiến trình (total), số đang hoạt động (running), số đang ngủ/chờ (sleeping), số đã dừng (stopped) và số không thể dừng hẳn (zombie).

- Dòng thứ 3-5 lần lượt cho biết thông tin về CPU, RAM và bộ nhớ Swap

- Các dòng còn lại liệt kê chi tiết về các tiến trình như định danh (PID), người dùng thực thi (USER), độ ưu tiên (PR), dòng lệnh thực thi (COMMAND) .....

Một lệnh khác là `ps` cũng giúp ta liệt kê được chi tiết về các tiến trình tuy nhiên có một vài điểm khác với `top` 

- Chỉ hiển thị từ dòng thứ 6 của lệnh `top`

- Nếu `top` hiển thị một cách realtime các tiến trình thì `ps` chỉ hiện thị thông tin tại thời điểm khởi chạy lệnh.

- `top` và `ps` đều có thể dùng kết hợp với piping tuy nhiên như vậy thì tính realtime của `top` sẽ không có ý nghĩa.

## **Kết thúc một tiến trình đang hoạt động** 

Một ngày nào đó, hệ thống đang vận hành bình thường, bạn đang làm những công việc thường ngày vẫn làm. Tuy nhiên, cái trình duyệt bạn đang dùng tự nhiên bị treo (not responding), bạn thử tắt nó nhưng không có gì thay đổi. Và lúc này để xử lý cái trình duyệt khó chịu đó bạn có thể sử dụng các công cụ dòng lệnh, bao gồm ps và kill. Lệnh kill được dùng để kết thúc một tiến trình dựa trên định danh của tiến trình PID, và để biết được PID của tiến trình cần buộc kết thúc, ta có thể dùng ps kết hợp với redirection bằng grep. Ta sử dụng lệnh sau: ps aux | grep 'opera' (VD với trình duyệt Opera bị treo)

Trình duyệt Opera chạy rất nhiều tiến trình, vậy ta thử tắt chúng đi, sử dụng lệnh kill -9 PID, ở trên hình ta sẽ thử tắt tiến trình có PID = 8768, như vậy command giờ sẽ là: kill -9 8768.

