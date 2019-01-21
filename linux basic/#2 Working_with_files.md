## Luồng file
- Khi dòng lệnh được thực thi, mặc định 3 tiêu chuẩn luồng hay ký hiệu luôn luôn mở để sử dụng
  - chuẩn đầu vào or stdin
  - chuẩn đầu ra or stdout
  - chuẩn báo lỗi or stderr
**Chuẩn stdin**
- Đây là nơi mà dữ liệu được nhập vào, và thường là thiết bị cuối (terminal).

  -Ví dụ: Bạn có thể chuyển nội dung của tệp tin cho lệnh "grep" như sau:

   `$grep root < /path/to/some/file ` # hiển thị các dòng chứa từ root trong tệp tin.​
**Chuẩn stdout**
- Đây là nơi chương trình xuất dữ liệu ra.

  -Ví dụ bạn muốn lệnh "echo" kết xuất dữ liệu ra một tệp tin, thế thì làm như sau:

   `$echo "Hello" > hello.txt ` # hello.txt sẽ có nội dung là "Hello".​
**Chuẩn stderr**
- Là nơi các chương trình báo lỗi

  - Ví dụ giả sử thư mục demo đã có rồi, mà bạn lại tạo sẽ gây lỗi. Bây giờ tôi xin hướng dẫn cách lấy lỗi của lệnh này và chuyển nội dung vào tệp tin log.txt.

   `$mkdir demo >> log.txt 2>&1​`

  ## Xác định vị trí file
  - Xác định vị trí thông qua cơ sở dữ liệu đã được dựng lên trước đó của file hay đường dẫn trên file hệ thống của bạn, nó nối toàn bộ bao gồm 1 chuỗi ký tự cụ thể. Xác định vị trí sử dụng database đã được tạo bởi chương trình khác. Hầu như các hệ thống linux chạy 1 cách tự động 1 lần 1 ngày. Tuy nhiên, bạn có thể update tại bất kỳ thời điểm chỉ với lệnh `updatedb` từ command như người dùng root.
 ```
# yum install -y mlocate
# updatedb
# locate zip
```
  - Kết quả của `locate` có thể xuất ra trong một thời gian dài. Để lấy ra một list ngắn hơn chúng ta có thể sử dụng `grep` chương trình như một bộ lọc.Nó sẽ chỉ in những dòng bao gồm một hay nhiều chuỗi cụ thể như ở dưới đây:
```
  $ locate zip | grep bin
/usr/bin/gpg-zip
/usr/bin/gunzip
/usr/bin/gzip
/usr/bin/zipdetails
```
- Thứ sẽ list tất cả các file và đường dẫn với cả "zip" và "bin" theo tên của chúng. Wildcard có thể được sử dụng trong tìm kiếm danh sách tên bao gồm những ký tự đặc biệt.
|Wildcard| Result|
|--------|:-------:|
|   *    |những chuỗi của ký tự|
|   ?    |những ký tự đơn|
- Câu lệnh `find` thực sự hữu ích và thường được sử dụng hằng ngày đối với các quản trị hệ thống linux. Nó đệ quy xuống các cây file hệ thống từ những đường dẫn cụ thể và xác định những file đó nối với điều kiện cụ thể. Ví dụ để tìm tất cả các file trong thư mục var có đuôi .log ta sử dụng câu lệnh:
```
$ find /var -name *.log
/var/log/audit/audit.log
/var/log/tuned/tuned.log
/var/log/anaconda/anaconda.log
/var/log/anaconda/anaconda.program.log
/var/log/anaconda/anaconda.packaging.log
/var/log/anaconda/anaconda.storage.log
```
- `find` sẽ list ra tất cả các file trong đường dẫn hiện tại và tất cả các đường dẫn nhỏ. Ví dụ tìm file và đường dẫn được đặt tên "sr"
`$ find /usr -name sr`
- Lệnh find cũng có thể tìm được các file dựa vào kích cỡ của find bằng câu lệnh
`$ find / -size +10M`
- Câu lệnh để tìm ra những file có dung lượng lớn hơn 10 MB
## Quản lý file:
- Sử dụng các câu lệnh ở bảng dưới.
|Câu lệnh|Sử dụng|
|--------|:-------:|
|  Cat   |Được sử dụng để xem những file không quá dài|
|  less  |Sử dụng để xem những file dài có thể cuộn lên và xuống được|
|  tail  |mặc định in ra 10 dòng của file. Bạn có thể thay đổi số của dòng đầu bằng -n 15 nếu muốn xem 15 dòng cuối thay vì 10 như mặc định |
|  head  |trái ngược với tail, head cho phép xem mặc định là 10 dòng đầu của file|

- Câu lệnh `touch` được sử dụng để tạo file. Câu lệnh có cú pháp sau:
` $ touch <filename>`
- Câu lệnh `mkdir` để tạo thư mục. Để xóa thư mục sử dụng câu lệnh `rmdir`
- Câu lệnh diff để so sánh giữa 2 file
```
$ cat file1.txt
Amor, ch'a nullo amato amar perdona,
Mi prese del costui piacer si forte,
Che, come vedi, ancor non m'abbandona.
$ 
$  cat file2.txt
amor, ch'a nullo amato amar perdona,
mi prese del costui piacer si forte,
che, come vedi, ancor non m'abbandona.
$ 
$ diff  file1.txt file2.txt
< Amor, ch'a nullo amato amar perdona,
< Mi prese del costui piacer si forte,
< Che, come vedi, ancor non m'abbandona.
---
> amor, ch'a nullo amato amar perdona,
> mi prese del costui piacer si forte,
> che, come vedi, ancor non m'abbandona.
$ 
$ diff -c file1.txt file2.txt
*** file1.txt   2015-02-17 16:10:03.781804799 +0100
--- file2.txt   2015-02-17 16:13:41.059088459 +0100
***************
! Amor, ch'a nullo amato amar perdona,
! Mi prese del costui piacer si forte,
! Che, come vedi, ancor non m'abbandona.
--- 1,3 ----
! amor, ch'a nullo amato amar perdona,
! mi prese del costui piacer si forte,
! che, come vedi, ancor non m'abbandona.
$ 
$  diff -i file1.txt file2.txt
$ 
```





