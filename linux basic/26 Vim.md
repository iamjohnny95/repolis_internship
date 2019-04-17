## **Vim**

Vim là từ Vi cải tiến nên cơ bản chúng giống nhau 

## **Vi/Vim là gì**

- Vi/Vim chỉ là một text editor. Giống như các text editor quen thuộc khác như Notepad, Sublime Text, Atom,... Vim cũng chỉ là một chương trình cho phép người dùng soạn thảo và chỉnh sửa nó tùy ý.

Đều có 3 mode chính:

- Insert mode

- Normal mode

- Visual mode

## **Giữa Vi và Vim có một sự khác biệt cơ bản:**

- Portability: Vi chỉ có thể dùng trên Unix, thay vào đó thì Vim có làm việc trên cả MS-Windows, Macintosh, Amiga, OS/2, VMS, QNX và nhiều hệ thống khác. Tất nhiên Vim cũng có thể dùng trên tất cả các Unix system.

- Syntax highlighting: Vim được lập trình để làm nổi bật các thành phần với các color và style khác nhau dựa trên từng loại file đang được chỉnh sửa. Có hàng trăm các quy tắc syntax highlighting đi kèm với Vim trong khi Vi thì không

## **Cấu trúc câu lệnh của Vim**

```
[number][command][motion/ text object]
```

`number` là số lần thực hiện câu lệnh, mặc định là 1

`command` là một hành động thêm, sửa, xóa, thay thế...

`Motion / Text object` Vim coi các text trong file như một object, ví dụ như 1 từ, 1 câu,.. và có thể thao tác với mỗi object đó

Ví dụ như:

- Bạn muốn xóa 1 từ: daw (delete a word)

- Bạn muốn thay thế nội dung trong dấu "": ci" (change in "")

- Xóa từ vị trí con trỏ tới cuối file: dG (delete to G-eof)

- Copy nội dung cho tới lúc gặp dấu ".": yf. (yank (to) find .)

- Bạn muốn di chuyển con trỏ xuống dưới 10 dòng: 10j

**1. Mở file**

Cũng giống như các editor khác bạn cần sử dụng vi trước tên file

vi /duong_dan_den_file

ví dụ: vi /var/www/index.php sẽ mở file index.php trong editor

**2. Đóng file**

Khi đã làm việc với file xong, để đóng file bạn bấm "Esc" (phím Escape) rồi gõ

:q

để thoát và không lưu

:wq

lưu lại nội dung file và thoát

**3. Sửa file**

Trong vi có 2 chế độ là command mode và insert mode. Mặc định là command mode. Để chuyển sang chế độ sửa hoặc ghi vào file (insert mode) bạn sử dụng

:i

để chuyển sang chế độ insert mode (ký tự được ghi phía trước con trỏ)

:a

để chuyển sang chế độ insert mode (ký tự được ghi phía sau con trỏ)

Lưu ý : trong chế độ insert mode bạn không thể dùng các command (các lệnh của vi như tìm kiếm ....), để có thể dùng command bạn cần thoát chế độ insert trước (bằng cách gõ Esc trên bàn phím)

**4. Di chuyển con trỏ**

Để di chuyển con trỏ bạn sử dụng các phím h,j,k,l hoặc các phím mũi tên tương ứng trên bàn phím

**5. Xóa dòng**

Để xóa 1 dòng, bạn di chuyển con trỏ đến đầu dòng đó và gõ dd

**6. Copy và paste**

Để copy 1 dòng, bạn gõ 

yy

Để paste dòng đó, di chuyển đến nơi cần paste và gõ

p

**7. Tìm kiếm**

Để tìm kiếm bạn gõ / hoặc ?, phía sau là từ cần tìm kiếm

Ví dụ 

/ServerName

sẽ tìm kiếm từ ServerName trong file

Nếu vi nhảy đến kết quả đầu tiên chưa đúng ý bạn, để tiếp tục xem dòng khác gõ n

**8. Nhảy đến 1 dòng hoặc cột nào đó**

Gõ số dòng muốn nhảy đến và gõ G, nhảy đến cột nào đó gõ |

ví dụ : 

89G

sẽ nhảy đến dòng 89

21|

sẽ nhảy đến cột 21