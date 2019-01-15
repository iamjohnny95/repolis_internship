
## Câu lệnh mở đầu với Linux
### 1. ls - List

**ls** liệt kê nội dung (file và thư mục) trong thư mục hiện hành. Nó cũng tương tự với việc bạn mở một thư mục và xem nội dung trong đó trên giao diện người dùng.
-   `-a`: xem cả các file và thư mục ẩn
-   `-l`: xem thông tin chi tiết bao gồm ACL (access control list), kích cỡ, ngày tháng cập nhật, chủ sở hữu ....
-   `-p`: thêm slash (`/`) để đánh dấu các thư mục
-   `-R`: xem cả cây thư mục

### 2. mkdir - Make Directory

**mkdir <tên thư mục mới>** tạo một thư mục mới. Nó cũng tương tự với việc bạn chọn new/create directory để tạo một thư mục mới trên giao diện người dùng.

### 3. pwd - Print Working Directory

**pwd** in ra đường dẫn đầy đủ đến thư mục hiện hành.

### 4. cd - Change Directory

**cd <thư mục>** chuyển một thư mục thành thư mục hiện hành cho phiên làm việc hiện tại. Nó cũng tương tự với việc bạn mở một thư mục và thao tác với các file và thư mục bên trong đó trên giao diện người dùng.

### 5. rmdir - Remove Directory

**rmdir <thư mục>** xóa một thư mục.

## 6. rm - Remove

**rm <tên file>** xóa file. Bạn cũng có thể sử dụng  **rm -r <tên thư mục>** để xóa thư mục và toàn bộ dữ liệu trong thư mục đó.

## 7. cp - Copy

**cp <file nguồn> <file đích>** sao chép file từ vị trí nguồn đến vị trí đích.  
Bạn cũng có thể sử dụng **cp -r <thư mục nguồn> <thư mục đích>** để sao chép thư mục và toàn bộ dữ liệu bên trong.

## 8. mv - Move

**mv <nguồn> <đích>** di chuyển một file hoặc thư mục từ vị trí này sang vị trí khác. Lệnh này cũng dùng để đổi tên file hoặc thư mục nếu như  **<nguồn>** và  **<đích>** là cùng một thư mục.

## 9. cat – concatenate and print files

**cat <tên file>** đọc và in ra nội dung của file ra màn hình.

## 10. tail – print TAIL

**tail <tên file>** đọc và in ra nội dung 10 dòng cuối cùng của file (mặc định).  
Bạn có thể sử dụng  **tail -n N <tên file>** để chỉ định in  **N** dòng ra màn hình.
## 11. head – print HEAD

**head <tên file>** đọc và in ra nội dung 10 dòng đầu tiên của file (mặc định).  
Bạn có thể sử dụng  **head -n N <tên file>** để chỉ định in  **N** dòng ra màn hình.

## 12. less – print LESS

**less <tên file>** in ra nội dung của một file theo từng trang trong trường hợp nội dung của file quá lớn và phải đọc theo trang. Bạn có thể dùng  **Ctrl+F**  để chuyển trang tiếp theo và  **Ctrl+B**  để chuyển về trang trước

## 13. grep

**grep <chuỗi> <tên file>** tìm kiếm nội dung của file theo chuỗi cung cấp.  
Bạn có thể dùng  **grep -i <chuỗi> <tên file>** để tìm kiếm không phân biệt hoa thường hoặc  **grep -r <chuỗi> <tên thư mục>** để tìm kiếm trong toàn thư mục

## 14. find

**find <thư mục> -name <tên file>** tìm kiếm file trong  **<thư mục>** theo  **<tên file>** .  
Bạn cũng có thể dùng  **find <thư mục> -iname <tên file>** để tìm kiếm không phân biệt hoa thường.
## 15. tar

**tar -cvf <tên-file-nén.tar> <file1 hoặc file2 ...>** tạo file nén (.tar) từ các file có sẵn.

**tar -tvf <tên-file-nén.tar>** xem nội dung file nén (.tar).

**tar -xvf <tên-file-nén.tar>** giải nén (file .tar).

## 16. gzip

**gzip <tên file>** tạo file nén (.gz). Sử dụng **gzip -d <tên file>** để giải nén (file .gz).

## 17. unzip

**unzip <file-nén.zip>** giải nén một file nén (.zip). Sử dụng  **unzip -l <file-nén.zip>** để xem nội dung file zip mà không cần giải nén.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxNjI5MjQ0NiwtMTI1MTkwNjU2NSwtMT
c4MTMyNDI0Niw0Nzk2MDcwNDIsMTA3Mjk4ODg5NCwtMTg4MDc3
NDMzLDE0OTkxNzE0NDgsMTkzMDE2ODAxMCwtMzIxNTYzMzQ4LD
E3MzQ0MDQ0MjgsMTU2NzA1NjIyMCwtMTIyMzUyOTIwMywtNjE0
MTY1MzYyLC0xNTU3MjIzODk2LDEwOTc5OTc4ODUsNDQxNjkzMD
UyLDE4NTY4NzEyODMsOTYyNzI0OTY3LC0yMDg4NzQ2NjEyLDE1
ODg5MzMwNl19
-->