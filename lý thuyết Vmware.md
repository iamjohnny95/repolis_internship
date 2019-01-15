## Hướng dẫn cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu

### Sử dụng công cụ phân vùng Gparted

Đây là công cụ có giao diện giống với các phần mềm quản lý phân vùng ổ đĩa trên Windows. Nên việc sử dụng nó cũng tương đối đơn giản nên mình sẽ không hướng dẫn chi tiết.
![](https://secure.gravatar.com/avatar/dabbaf0d03c5a9beae02bd6b048a06a4?s=60&r=g)

[Tường Nguyễn](https://tuong.me/author/noido1nguoidangcho1nguoi/)

June 13, 2017

[NO COMMENTS](https://tuong.me/cach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet/#respond)

# Cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu chi tiết

[Facebook](https://www.facebook.com/share.php?m2w&s=100&p[url]=https%3A%2F%2Ftuong.me%2Fcach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet%2F&p[images][0]=h&p[title]=C%C3%A1ch+chia+%E1%BB%95+%C4%91%C4%A9a%2C+qu%E1%BA%A3n+l%C3%BD+ph%C3%A2n+v%C3%B9ng+tr%C3%AAn+Linux%2C+Ubuntu+chi+ti%E1%BA%BFt&u=https%3A%2F%2Ftuong.me%2Fcach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet%2F&t=C%C3%A1ch+chia+%E1%BB%95+%C4%91%C4%A9a%2C+qu%E1%BA%A3n+l%C3%BD+ph%C3%A2n+v%C3%B9ng+tr%C3%AAn+Linux%2C+Ubuntu+chi+ti%E1%BA%BFt)[Twitter](https://tuong.me/chuyen-huong/?url=https%3A%2F%2Ftwitter.com%2Fintent%2Ftweet%3Foriginal_referer%3Dhttps%253A%252F%252Ftuong.me%252Fcach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet%252F%26text%3DC%C3%A1ch+chia+%E1%BB%95+%C4%91%C4%A9a%2C+qu%E1%BA%A3n+l%C3%BD+ph%C3%A2n+v%C3%B9ng+tr%C3%AAn+Linux%2C+Ubuntu+chi+ti%E1%BA%BFt%26url%3Dhttps%253A%252F%252Ftuong.me%252Fcach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet%252F%26via%3Dtuongs2it)[Google+](https://tuong.me/chuyen-huong/?url=%2F%2Fplus.google.com%2Fshare%3Furl%3Dhttps%253A%252F%252Ftuong.me%252Fcach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet%252F)[Pinterest](https://tuong.me/chuyen-huong/?url=http%3A%2F%2Fpinterest.com%2Fpin%2Fcreate%2Fbutton%2F%3Furl%3Dhttps%253A%252F%252Ftuong.me%252Fcach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet%252F%26media%3Dhttps%3A%2F%2Fi2.wp.com%2Ftuong.me%2Fwp-content%2Fuploads%2F2017%2F06%2FC%C3%A1ch-chia-%E1%BB%95-%C4%91%C4%A9a-qu%E1%BA%A3n-l%C3%BD-ph%C3%A2n-v%C3%B9ng-tr%C3%AAn-Linux-Ubuntu.png%3Ffit%3D777%252C524%26ssl%3D1%26description%3DC%C3%A1ch+chia+%E1%BB%95+%C4%91%C4%A9a%2C+qu%E1%BA%A3n+l%C3%BD+ph%C3%A2n+v%C3%B9ng+tr%C3%AAn+Linux%2C+Ubuntu+chi+ti%E1%BA%BFt)

PROMOTED CONTENT

[![Mgid](https://cdn.mgid.com/images/by_mgid_adc_logo_mini.svg "Mgid")](https://mgid.com/advertisers?utm_source=widget&utm_medium=text&utm_campaign=add&utm_content=207363)

[](https://Ki%E1%BA%BFm_h%C3%A0ng_ch%E1%BB%A5c_tri%E1%BB%87u_m%E1%BB%97i_%C4%91%C3%AAm_ch%E1%BB%89_b%E1%BA%B1ng_m%E1%BA%B9o_%C4%91%C6%A1n_gi%E1%BA%A3n_n%C3%A0y/)

![](https://imgg-cdn.mgid.com/3141/3141682_200x150.jpg?t=1544189083)

[Kiếm hàng chục triệu mỗi đêm chỉ bằng mẹo đơn giản này](https://Ki%E1%BA%BFm_h%C3%A0ng_ch%E1%BB%A5c_tri%E1%BB%87u_m%E1%BB%97i_%C4%91%C3%AAm_ch%E1%BB%89_b%E1%BA%B1ng_m%E1%BA%B9o_%C4%91%C6%A1n_gi%E1%BA%A3n_n%C3%A0y/)

[](https://engbreaking.com/Ti%E1%BA%BFng_Anh_h%E1%BB%8Dc_tr%C6%B0%E1%BB%9Bc_qu%C3%AAn_sau_K%C3%A9m_t%E1%BB%AB_v%E1%BB%B1ng_%C3%81p_d%E1%BB%A5ng_c%C3%A1ch_n%C3%A0y_ngay)

![](https://imgg-cdn.mgid.com/3155/3155793_200x150.jpg?t=1544756792)

[Tiếng Anh học trước quên sau? Kém từ vựng? Áp dụng cách này ngay!](https://engbreaking.com/Ti%E1%BA%BFng_Anh_h%E1%BB%8Dc_tr%C6%B0%E1%BB%9Bc_qu%C3%AAn_sau_K%C3%A9m_t%E1%BB%AB_v%E1%BB%B1ng_%C3%81p_d%E1%BB%A5ng_c%C3%A1ch_n%C3%A0y_ngay)

[engbreaking.com](https://engbreaking.com/Ti%E1%BA%BFng_Anh_h%E1%BB%8Dc_tr%C6%B0%E1%BB%9Bc_qu%C3%AAn_sau_K%C3%A9m_t%E1%BB%AB_v%E1%BB%B1ng_%C3%81p_d%E1%BB%A5ng_c%C3%A1ch_n%C3%A0y_ngay)

[](https://xn--kim_1000_trong_mt_ngy_nh_th_thut_ny-l3co21010agta46a7exq/)

![](https://imgg-cdn.mgid.com/3141/3141630_200x150.jpg?t=1544188276)

[Kiếm 1000$ trong một ngày nhờ thủ thuật này](https://xn--kim_1000_trong_mt_ngy_nh_th_thut_ny-l3co21010agta46a7exq/)

[](https://Gi%E1%BA%A3m_90_ch%E1%BB%89_trong_1_ng%C3%A0y_cho_chi%E1%BA%BFc_%C4%91%E1%BB%93ng_h%E1%BB%93_g%C3%A2y_s%E1%BB%91t_nh%E1%BA%A5t_n%C4%83m_2019/)

![](https://imgg-cdn.mgid.com/3155/3155867_200x150.jpg?t=1544767903)

[Giảm 90% chỉ trong 1 ngày cho chiếc đồng hồ gây sốt nhất năm 2019](https://Gi%E1%BA%A3m_90_ch%E1%BB%89_trong_1_ng%C3%A0y_cho_chi%E1%BA%BFc_%C4%91%E1%BB%93ng_h%E1%BB%93_g%C3%A2y_s%E1%BB%91t_nh%E1%BA%A5t_n%C4%83m_2019/)

Nhiều khi sử dụng máy tính chúng ta cũng cần  **chia ổ đĩa, tạo một phân vùng partition**  để lưu trữ hoặc cài đặt một hệ điều hành mới. Nhưng bạn tự hỏi trên  **Linux, Ubuntu**  có  **công cụ quản lý phân vùng ổ đĩa**  giống như trên Windows? Câu trả lời là có, trên Ubuntu, Linux cũng tích hợp một số công cụ để bạn có thể phân chia ổ đĩa, quản lý phân vùng và định dạng phân vùng. Dưới đây chúng ta sẽ cùng tìm hiểu cách để phân chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu bằng công cụ **Gparted, gdisk hoặc fdisk**.

Mục Lục

-   [Tìm hiểu các định dạng File System trong Linux, Ubuntu](https://tuong.me/cach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet/#Tim_hieu_cac_dinh_dang_File_System_trong_Linux_Ubuntu "Tìm hiểu các định dạng File System trong Linux, Ubuntu")
-   [Hướng dẫn cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu](https://tuong.me/cach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet/#Huong_dan_cach_chia_o_dia_quan_ly_phan_vung_tren_Linux_Ubuntu "Hướng dẫn cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu")
    -   [Sử dụng công cụ phân vùng Gparted](https://tuong.me/cach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet/#Su_dung_cong_cu_phan_vung_Gparted "Sử dụng công cụ phân vùng Gparted")
    -   [Sử dụng công cụ fdisk và gdisk](https://tuong.me/cach-chia-dia-quan-phan-vung-tren-linux-ubuntu-chi-tiet/#Su_dung_cong_cu_fdisk_va_gdisk "Sử dụng công cụ fdisk và gdisk")

## Tìm hiểu các định dạng File System trong Linux, Ubuntu

Chúng ta đã quá quen thuộc với những định dạng như NTFS, Fat, Fat32 nhưng các định dạng như Ext1, Ext2, Ext3, Ext4, XFS, JFS thì chắc nhiều bạn còn chưa nắm vững. Dưới đây chúng ta sẽ cùng tìm hiểu chúng để có thể quản lý phân vùng trong ubuntu hiệu quả hơn.

-   **Ext – Extended file system**: là định dạng file hệ thống đầu tiên được thiết kế dành riêng cho Linux. Có tổng cộng 4 phiên bản Ext1, Ext2, Ext3, Ext4. Hiện nay đa phần người dùng sử dụng định dạng Ext4 vì nó có thể giảm bớt hiện tượng phân mảnh dữ liệu trong ổ cứng, hỗ trợ các file và phân vùng có dung lượng lớn…
-   **XFS**: Khá tương đồng với Ext4 về một số mặt nào đó, chẳng hạn như hạn chế được tình trạng phân mảnh dữ liệu, không cho phép các snapshot tự động kết hợp với nhau, hỗ trợ nhiều file dung lượng lớn, có thể thay đổi kích thước file dữ liệu…
-   **JFS**: Điểm mạnh của JFS là tiêu tốn ít tài nguyên hệ thống, đạt hiệu suất hoạt động tốt với nhiều file dung lượng lớn và nhỏ khác nhau. Tốc độ kiểm tra ổ đĩa nhanh hơn so với các phiên bản Ext.
-   ….

## Hướng dẫn cách chia ổ đĩa, quản lý phân vùng trên Linux, Ubuntu

### Sử dụng công cụ phân vùng Gparted

Đây là công cụ có giao diện giống với các phần mềm quản lý phân vùng ổ đĩa trên Windows. Nên việc sử dụng nó cũng tương đối đơn giản nên mình sẽ không hướng dẫn chi tiết.

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
eyJoaXN0b3J5IjpbMTM1NTE4MDU2MCwxNTg4OTMzMDYsLTEzOD
U3ODIxNTQsLTExOTIyNDU3NDcsLTI4NTg5MTA1NSw4ODk0NDYx
MTMsLTYxNzg0NzA4Miw0ODgzMTI2NzcsMTk4NzU3MjA1NSwyOT
kxMDI4MTMsMTE2NzU1NTE0NywtMTM1NzQ1NzU5MywtMTQwMDQ3
MTU3XX0=
-->