# Bộ nhớ swap:
## Swap là gì
- Swap là một vùng trên ổ đĩa mà nó có thể được sử dụng lưu trữ các dữ liệu mà không được sử dụng bộ nhớ vật lý trên RAM. Đây là nơi chứa tài nguyên tạm thời đang hoạt động trong bộ nhớ.
- Swap được sử dụng khi hệ thống của bạn quyết định rằng nó cần thêm bộ nhớ RAM cho quá trình hoạt động và bộ nhớ RAM không còn dư để sử dụng. Nếu điều đó xảy ra, các tài nguyên và dữ liệu tạm thời không hoạt động trên bộ nhớ RAM sẽ được di chuyển để lưu trữ vào không gian Swap để giải phóng bộ nhớ RAM và sử dụng cho việc khác.
- Lưu ý rằng thời gian truy cập vào vùng Swap là chậm hơn nhiều, do đó không nên sử dụng Swap là một phương pháp thay thế hoàn hảo cho bộ nhớ vật lý (RAM). Swap có thể là một phân vùng dành riêng cho Swap (khuyến nghị), một tập tin Swap hoặc một sự kết hợp của phân vùng và tập tin Swap. 

## Tại sao cần Swap
- Cũng có thể nói rằng sử dụng Swap là lấy ổ cứng làm RAM, tuy nó là chậm nhưng nó vẫn tốt hơn là không sử dụng nếu máy tính không có đủ lượng RAM. Bạn vẫn có thể chỉ định rằng khi nào hệ thống sẽ được phép sử dụng Swap. Vì vậy nên sử dụng Swap cho máy tính, mặc dù bạn có ít hoặc nhiều bộ nhớ RAM.

- **Chế độ ngủ đông (Hibernation)** :Trong Ubuntu, nếu bạn muốn sử dụng tính năng ngủ đông (suspend-to-disk) thì bạn cần phải có phân vùng Swap.
- **Tối ưu hóa bộ nhớ** :Hệ thống sẽ di chuyển các tài nguyên và dữ liệu hiện không được sử dụng trong bộ nhớ RAM đến Swap, điều này giúp cho hệ thống phục vụ với các mục đích khác tốt hơn. 
- **Tránh các trường hợp không lường trước** :Trong một số trường hợp, bạn không dự tính được bộ nhớ dành cho các chương trình mà bạn chuẩn bị thử nghiệm, hoặc một chương trình bất kỳ nào đó nổi điên lên, hoặc bất cứ điều gì đó bất thường. Trong trường hợp này, Swap sẽ được sử dụng để hệ thống có thể được duy trì để tiếp tục chạy (mặc dù nó là chậm) thay vì hệ thống đột ngột dừng lại vì thiếu bộ nhớ.

## Kích thước Swap là bao nhiêu
- Đối với dung lượng RAM lớn hơn 1GB, nếu muốn sử dụng chế độ ngủ đông thì kích thước tối thiểu Swap là bằng với lượng RAM. Nếu không sử dụng chế độ ngủ đông thì kích thước tối thiểu của Swap là gấp đôi lượng RAM. Có một nhược điểm khi bạn thiết lập kích thước của Swap quá lớn, đó là bạn đang lãng phí dung lượng ổ đĩa mặc dù Swap không được sử dụng.

## Tạo swap
### **Kiểm tra thông tin Swap trên hệ thống**
- Trước khi tạo swap, chúng ta kiểm tra xem swap đã chạy chưa bằng câu lệnh 
`free -m`
- Các thông số sẽ ra như bảng dưới. Máy đã sử dụng 5G cho bộ nhớ swap

```
| |total|used|free|shared|buff/cache|available|
|---|---|---|---|---|---|---|
|Mem:|991|115|747|7|128|725|
|swap:|5119|0|5119|
```
- Bây giờ sử dụng lệnh `df-h` để kiểm tra dụng lượng trong ổ đĩa còn trống bao nhiêu. Từ đó tính toán dung lượng để khởi tạo swap

### **Tạo Swap file**
- Tạo file dùng cho hoạt động swap. Swap file sẽ có dung lượng 512M (1024*512 = 524288)
```
 [root@localhost ~]# dd if=/dev/zero of=/swapfile bs=1024 count=524288
524288+0 records in
524288+0 records out
536870912 bytes (537 MB) copied, 12.6459 s, 42.5 MB/s
```
- Phân quyền cho file /swapfile với quyền chỉ user root mới được phép thao tác trên đây
`[root@localhost ~]# chmod 600 /swapfile`

- Tiến hành tạo file swap
`[root@localhost ~]# mkswap /swapfile`

- Bật swap lên
` swapon /swapfile`

- Sau đó kiểm tra bằng câu lệnh 
`swap -s` hay `free -m`

- Cấu hình fstab, để khi hệ thống khởi động lại vẫn nhận diện swap file này là sử dụng cho bộ nhớ ảo RAM SWAP
```
# vi /etc/fstab
/swapfile swap swap defaults 0 0
```

### **Xóa file Swap**
- Xóa trên file fstab sau đó reboot lại hệ thống






