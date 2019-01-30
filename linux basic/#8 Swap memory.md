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


| |total|used|free|shared|buff/cache|available|
|---|---|---|---|---|---|---|
|Mem:|991|115|747|7|128|725|
|swap:|5119|0|5119|

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

### **Tìm hiểu lệnh dd**
- Câu lệnh dd trong linux là một trong những câu lệnh thường xuyên được sử dụng. Câu lệnh dd dùng để sử dụng trong các trường hợp sau:

   - Sao lưu và phục hồi toàn bộ dữ liệu ổ cứng hoặc một partition
   - Chuyển đổi định dạng dữ liệu từ ASCII sang EBCDIC hoặc ngược lại
   - Sao lưu lại MBR trong máy (MBR là một file dữ liệu rất quan trong nó chứa các lệnh để LILO hoặc GRUB nạp hệ điều hanh)
   - Chuyển đổi chữ thường sang chữ hoa và ngược lại
   - Tạo một file với kích cỡ cố định
   - Tạo một file ISO
- Cú pháp:
`#dd if=<địa chỉ đầu vào> of=<địa chỉ đầu ra> option`

- Trong đó
  - if= địa chỉ nguồn của dữ liệu nó sẽ bắt đầu đọc
  - of= viết đầu ra của file
  - option : các tùy chọn cho câu lệnh

 - Các tùy chọn 

 |**Tùy chọn**|**Ý nghĩa**|
 |-----------|----------|
 |bs=Bytes|Quá trình đọc (ghi) bao nhiêu byte một lần đọc (ghi)|
 |cbs=Bytes|Chuyển đổi bao nhiêu byte một lần|
 |count=Blocks|thực hiện bao nhiêu Block trong quá trình thực thi câu lệnh|
 |if|Chỉ đường dẫn đọc đầu vào|
 |of|Chỉ đường dẫn ghi đầu ra|
 |ibs=bytes|Chỉ ra số byte một lần đọc|
 |obs=bytes|Chỉ ra số byte một lần ghi|
 |skip=blocks|Bỏ qua bao nhiêu block đầu vào|
 |conv=Convs|Chỉ ra tác vụ cụ thể của câu lệnh, các tùy chọn được ghi dưới bảng sau đây|

 - Các tùy chọn của conv
 
 |**Tùy chọn**|**Ý nghĩa**|
 |------------|-----------|
 |nocreat|Không tạo ra file đầu ra|
 |noerror|Tiếp tục sao chép dữ liệu khi đầu vào bị lỗi|
 |sync|Đồng bộ dữ liệu với ổ đang sao chép sang|

 - Khi định dạng số lượng byte mỗi lần đọc. Mặc định nó được tính theo đơn vị là kb. Bạn có thể thêm một số trường sau để báo định dạng khác:
  - c = 1 byte
  - w = 2 byte
  - b = 512 byte
  - kB = 1000 byte
  - K = 1024 byte
  - MB = 1000000 byte
  - M = (1024 * 1024) byte
  - GB = (1000 * 1000 * 1000) byte
  - G = (1024 * 1024 * 1024) byte

### ***Các ví dụ của lệnh dd trong thực tế***
- **Sao lưu- phục hồi toàn bộ ổ cứng hoặc phân vùng trong ổ cứng**
  - Sao lưu toàn bộ dữ liệu ổ cứng sao ổ cứng khác

`#dd if=/dev/sda of=/dev/sdb conv=noerror,sync`

Câu lệnh này dùng dể sao lưu toàn bộ dữ liệu của ổ sda sang ổ sdb với tùy chọn trong trường conv=noerrom.sync với ý ngĩa vẫn tiếp tục sao lưu nếu dữ liệu đầu vào bị lỗi và tự động đồng bộ với dữ liệu sdb

  - Tạo một file image cho ổ sda1. Các này sẽ nhanh hơn là viêc chuyển dữ liệu sao ổ khác

`dd if=/dev/sda1 of=/root/sda1.img `

  - Sao lưu dữ liệu từ một phân vùng này đến một phân vùng khác

 `dd if=/dev/sda2 of=/dev/sdb2 bs=512 conv=noerror,sync`

 Đối với câu lệnh này bs=512 có ý nghĩa mỗi lần đọc ghi nó đọc và ghi 512 byte

  - Phục hồi dữ liệu

`dd if=/root/sda1.img of=/dev/sda1`

  - Sao lưu từ đĩa CDroom

`dd if=/dev/cdrom of=/root/cdrom.img conv=noerror`

  -  Tạo một file có dung lượng cố định

Tạo ra một file có kích thước 100M

`dd if=/dev/zero of=/root/file1 bs=100M count=1`

   - Sử dụng câu lệnh dd để tạo một phân vùng trống có kích cỡ 1G

`dd if=/dev/zero of=/root/swap bs=1024M count=1`
  
   - Backup và nén dữ liệu

` dd if=/dev/da0 conv=sync,noerror bs=128K | gzip -c > centos-core-7.gz `

   - Giải nén dữ liệu 

` gunzip -c centos-core-7.gz | dd of=/dev/da0 `














