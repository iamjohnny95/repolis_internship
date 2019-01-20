# Lý thuyết về VMware(update bổ sung thêm 1 số các yêu cầu)
## Tìm hiểu 3 chế độ card mạng 
** Chế độ Bridge: **
- Ở chế độ này, card mạng trên máy ảo được gắn vào VMnet0, VMnet0 này liên kết trực tiếp với card mạng vật lý trên máy thật, máy ảo lúc này sẽ kết nối internet thông qua  card mạng vật lý và có chung lớp mạng với card mạng vật lý.
** Chế độ Nat: **
- Áp dụng cơ chế Nat địa chỉ Ip cho phép nhiều máy tính kết nối mạng qua 1 địa chỉ publish. Ở chế độ này máy ảo có khả năng kết nối mạng nhưng dải địa chỉ khác với máy thật
** Chế độ Host- Only: **
- Cho phép tạo ra các máy ảo với địa chỉ tự tạo có thể kết nối với nhau. Sử dụng trong trường hợp tạo một mạng riêng. Có thể kết nối mạng nếu cài đặt DNS

## Gateway của 3 kiểu mạng
** Chế độ Bridge **
- Gateway sẽ trỏ đến địa chỉ mạng vật lý của router hay wifi
** Chế độ Nat ** 
- Gateway sẽ trỏ đến địa chỉ inside local
** Chế độ Host-Only:**
- Gateway sẽ trỏ đến dải mạng vật lý mình tạo ra

## Khái niệm về LAN Segment 
- Các card mạng của máy ảo có thể gắn kết với nhau thành từng LAN Segment. Không giống như VMnet, LAN Segment chỉ kết nối các máy ảo được gán trong một LAN Segment lại với nhau mà không có những tính năng như DHCP và LAN Segment không thể kết nối ra máy thật như các Virtual Switch VMnet. 

## Phân vùng ổ cứng cho Ubuntu Ở đây có 4 sự lựa chọn
- Guided - use entire disk: Sử dụng cho ổ cứng chưa từng được phân vùng, máy tính sẽ tự động format lại toàn bộ ổ cứng và định dạng cho từng vùng đã chia.
- Guided - use entire disk and with set up LVM: Tự động phân vùng bằng LVM, là một phương pháp cho phép ấn định không gian đĩa cứng thành những logical volume, khiến cho việc thay đổi kích thước các ổ đĩa dễ dàng hơn mà không phải sửa lại table của OS. Trong trường hợp bạn đã sử dụng hết phần bộ nhớ còn trống của partition và muốn mở rộng dung lượng thì LVM là một sự lựa chọn tốt.
- Guided - use entire disk and with set encrypted up LVM: Giống với lựa chọn 2 nhưng sẽ cài đặt mã hóa ổ cứng để tăng tính bảo mật.
- Manual: Phân vùng thủ công.
## Nat Advance 
- Khi một máy ảo trong VMWare sử dụng card mạng NAT thì sẽ được NAT ra ngoài mạng qua địa chỉ của máy thật, và các máy từ mạng ngoài sẽ không thể truy cập vào các máy trong dải NAT đó. Nếu muốn truy cập vào được (ví dụ ssh vào một máy ảo bên trong đang sử dụng NAT) thì cần tạo đường và cho phép máy bên ngoài truy câp vào.
- Ví dụ:
  - Một máy Ubuntu có ip 192.168.220.10
  - Ip máy thật có địa chỉ : 192.168.100.11
  - Vào VMWare -> Chọn Edit -> Virtual Network Editor

  ![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/1.png)

  - Thay đổi cài đặt -> Change Setting làm theo hình

  ![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/2.png)

  - Chọn cổng nằm trong dải khả dụng mà máy thật của bạn chưa sử dụng

  ![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/3.png)

  - Lưu lại, và ssh vào máy ảo bằng địa chỉ máy thật qua port 1111. Ở đây tôi sử dụng Xshell. Sau đó đăng nhập mật khẩu

  ![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/2.png)


