## Sử dụng RSYNC để đồng bộ dữ liệu trên linux
- RSYNC là một công cụ mạnh mẽ để copy file và đồng bộ dữ liệu giữa linux với linux.
## Các tính năng nổi bật của RSYNC 
- Sao chép cả sysbolic link, user, group, permission giúp bảo toàn dữ liệu.
- rsync nhanh hơn SCP, nó dùng thuật toán thông minh chỉ sao lưu những dữ liệu thay đổi.
- rsync nén dữ liệu trên server trước khi gửi đi.
- Tự xóa dữ liệu nếu dữ liệu đó không tồn tại trên source giúp đồng bộ dữ liệu giữa hai máy chủ linux từ xa.
- rsync kết hợp SSH bảo mật dữ liệu truyền trên internet.

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/rsync.png)]
(https://github.com/iamjohnny95/repolis_internship/blob/master/img/rsync.png)

## Cài đặt RSYNC
- Bên trên là một số tính năng quan trọng của rsync, để bắt đầu chúng ta phải cài rsync cho máy chủ của mình trước, nếu chưa có chạy lệnh.
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
--`exclude`: loại trừ ra những dữ liệu không muốn truyền đi, nếu bạn cần loại ra nhiều file hoặc folder ở nhiều đường dẫn khác nhau thì mỗi cái bạn phải thêm –exclude tương ứng.
***VÍ DỤ***:
- Sử dụng `rsync` để copy dữ liệu các file trong 1 máy chủ linux. Cụ thể là máy chủ centOS7. tạo thư mục /root/sondz. Bên trong thư mục sondz tạo file johnny. Tiếp theo đó backup vào thư mục tmp phòng trường hợp mất mát dữ liệu 
`# rsync -azvhPE ssh --delete /root/sondz/ /tmp/`
## Nén dữ liệu:
- file dữ liệu thông thường được nén để tiết kiệm dung lượng của ổ đĩa và giảm thời gian truyền file trên mạng. Linux sử dụng 1 số phương pháp để thực hiện nén. 2 kiểu nén file là gzip và bzip2
 - Gzip:**Nén** 1 file dưới định dạng .gz `Gzip -c abc.txt > abc.txt.gz`
        **Giải nén** `Gzip -dv abc.txt.gz` 
 - Bzip2:**Nén** `Bzip2 -c abc.txt > abc.txt.gz`
 		 **Giải nén** `Bzip2 -dv abc.txt.bz`
 - Nén cả file thư mục thì ta sử dụng lệnh tar
   - **Nén** `tar -cvf /root/sondz.tar /root/sondz` , còn muốn nén theo chuẩn gz thì sử dụng câu lệnh `tar -czvf /root/sondz.tar.gz /root/sondz`, nén sang chuẩn bz thì sử dụng câu lệnh `tar -cjvf /root/sondz.tar.bz /root/sondz`
   - **Giải nén** `tar -xvf sondz.tar.gz` 
   



