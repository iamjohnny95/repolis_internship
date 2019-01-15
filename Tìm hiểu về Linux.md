## Hướng dẫn cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu

### Sử dụng công cụ phân vùng Gparted

Đây là công cụ có giao diện giống với các phần mềm quản lý phân vùng ổ đĩa trên Windows. Nên việc sử dụng nó cũng tương đối đơn giản nên mình sẽ không hướng dẫn chi tiết.


# Cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu chi tiết

Nhiều khi sử dụng máy tính chúng ta cũng cần  **chia ổ đĩa, tạo một phân vùng partition**  để lưu trữ hoặc cài đặt một hệ điều hành mới. Nhưng bạn tự hỏi trên  **Linux, Ubuntu**  có  **công cụ quản lý phân vùng ổ đĩa**  giống như trên Windows? Câu trả lời là có, trên Ubuntu, Linux cũng tích hợp một số công cụ để bạn có thể phân chia ổ đĩa, quản lý phân vùng và định dạng phân vùng. Dưới đây chúng ta sẽ cùng tìm hiểu cách để phân chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu bằng công cụ **Gparted, gdisk hoặc fdisk**.


## Tìm hiểu các định dạng File System trong Linux, Ubuntu

Chúng ta đã quá quen thuộc với những định dạng như NTFS, Fat, Fat32 nhưng các định dạng như Ext1, Ext2, Ext3, Ext4, XFS, JFS thì chắc nhiều bạn còn chưa nắm vững. Dưới đây chúng ta sẽ cùng tìm hiểu chúng để có thể quản lý phân vùng trong ubuntu hiệu quả hơn.

-   **Ext – Extended file system**: là định dạng file hệ thống đầu tiên được thiết kế dành riêng cho Linux. Có tổng cộng 4 phiên bản Ext1, Ext2, Ext3, Ext4. Hiện nay đa phần người dùng sử dụng định dạng Ext4 vì nó có thể giảm bớt hiện tượng phân mảnh dữ liệu trong ổ cứng, hỗ trợ các file và phân vùng có dung lượng lớn…
-   **XFS**: Khá tương đồng với Ext4 về một số mặt nào đó, chẳng hạn như hạn chế được tình trạng phân mảnh dữ liệu, không cho phép các snapshot tự động kết hợp với nhau, hỗ trợ nhiều file dung lượng lớn, có thể thay đổi kích thước file dữ liệu…
-   **JFS**: Điểm mạnh của JFS là tiêu tốn ít tài nguyên hệ thống, đạt hiệu suất hoạt động tốt với nhiều file dung lượng lớn và nhỏ khác nhau. Tốc độ kiểm tra ổ đĩa nhanh hơn so với các phiên bản Ext.

## Hướng dẫn cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu

### Sử dụng công cụ phân vùng Gparted

Đây là công cụ có giao diện giống với các phần mềm quản lý phân vùng ổ đĩa trên Windows.

![Cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu](https://i2.wp.com/tuong.me/wp-content/uploads/2017/06/C%C3%A1ch-chia-%E1%BB%95-%C4%91%C4%A9a-qu%E1%BA%A3n-l%C3%BD-ph%C3%A2n-v%C3%B9ng-tr%C3%AAn-Linux-Ubuntu.png?resize=530%2C357&ssl=1)

Để cài đặt **GNOME Partition Editor**  bạn truy cập vào đường link  [tại đây](https://tuong.me/chuyen-huong/?url=http%3A%2F%2Fgparted.org%2Fdownload.php). Trang web sẽ hướng dẫn bạn cách cài đặt Gparted cho các phiên bản hệ điều hành linux. Sau khi cài đặt, đê mở công cụ Gparted bạn có thể truy cập vào Ubuntu Dash hoặc thiết bị đầu cuối.

### Sử dụng công cụ fdisk và gdisk

Đây là hai công cụ không có giao diện, bạn phải chạy nó hoàn toàn bằng dòng lệnh. fdisk được sử dụng để phân vùng ổ cứng chuẩn MBR, còn g**disk** được sử dụng để phân vùng ổ cứng chuẩn GPT. Hai công cụ này là anh em với nhau, cách sử dụng cũng y chang nhau. Còn thế nào là MBR và GPT, cách phân biệt giữa chúng thì bạn có thể xem qua  [bài viết này](https://tuong.me/su-khac-nhau-giua-mbr-voi-gpt-legacy-uefi/).

Để cài đặt Gdisk bạn chạy dòng lệnh bên dưới:

Đối với hệ điều hành Ubuntu

sudo apt–get  install gdisk

Đối với hệ điều hành Fedora/CentOS

su  –c  “yum install gparted”




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1Nzg1NDQ2NywxNTg4OTMzMDZdfQ==
-->