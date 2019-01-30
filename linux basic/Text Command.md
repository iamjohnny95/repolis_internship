# **Text commands**
- Hiển thị nội dung sử dụng `cat`,`less` và `echo`
- Chỉnh sửa nội dung `sed` và `awk`
- Tìm kiếm nội dung `grep`

## **Hiển thị nội dung**
- `cat` và `less` sẽ in ra màn hình toàn bộ nội dung file. Nhưng lệnh `less` có thể hiển thị được nội dung dài và có thể cuộn lên và xuống được
- `echo chỉ đơn giản dùng để in ra màn hình`

## **Edit nội dung file**
##**Sed command**
- Command sed là một công cụ mạnh mẽ để làm việc với các đoạn text. Nó sẽ lọc và sắp xếp sự bổ sung trong các dòng liệu (data streams). Dữ liệu từ nguồn vào (hoặc stream) sẽ được nhận và đưa vào một khu vực xử lí riêng. Toàn bộ danh sách hoạt động, việc chỉnh sửa được áp dụng vào dữ liệu trong khu vực làm việc và nội dung cuối cùng sẽ được chuyển ra ngoài khu vực làm việc đến nơi xuất dữ liệu chuẩn (hoặc stream).

- Cú pháp của lệnh `Sed`

`sed [option] [command] [file]`

Trong trường hợp bạn muốn thực hiện edit đối với standard input thay vì file thì không cần phải để tham số [file] nữa.

## **Một số option**
`-i`
- Thực hiện việc edit text inplace, trực tiếp vào input stream thay vì chỉ in kết quả sau khi edit text ra standard output. Điều này có nghĩa là bạn có thể trực tiếp thay đổi nội dung file thay vì chỉ in kết quả sau khi edit text ra màn hình console.

Ví dụ ta có 1 file test.txt với nội dung

```
hello
world
```
- Nếu bạn muốn thay đổi chữ l thường thành L hoa thì có thể dùng lệnh sau. (cú pháp s/original_text/substitute_text/g) chuyên dùng để thay thế text.

```
$ sed "s/l/L/g" test.txt
```

- Kết quả sẽ được hiện ra màn hình 
```
heLLo
worLd
```

- Tuy nhiên nội dung file test.txt không thay đổi. Trong trường hợp bạn muốn thay đổi nội trong file đó đồng thời muốn giữ lại nội dung file cũ vào 1 file khác để đề phòng bất trắc thì có thể làm như sau

```
$ sed -i .bak "s/l/L/g" test.txt
```
- Khi đó nội dung file test.txt sẽ bị thay đổi, các chữ l sẽ bị đổi thành L, còn nội dung cũ sẽ được lưu lại trong 1 file backup tên là test.txt.bak. Nếu bạn tự tin vào câu lệnh biến đổi text của mình thì có thể không cần file backup bằng cách chỉ định tham số của option -i là 1 string rỗng

```
$ sed -i "" "s/l/L/g" test.txt
```

`-e`

- Bổ sung thêm command cho list command.

Bạn có thể thực hiện nhiều phép thay thế text trên 1 câu lệnh sed như ví dụ sau:

```
$ echo "abcdefgh" | sed -e "s/b/B/g" -e "s/f/F/g"
aBcdeFgh
```

## **Sed script command**

- Đây là phần cốt lõi của lệnh sed. Dựa theo các chỉ thị trong phần command này mà lệnh sed thực hiện các thao tác tương ứng.
Cấu trúc của 1 sed script command như sau:

```
[addr]X[options]
```
`[addr]` là phần địa chỉ đánh dấu phạm vi mà câu lệnh `sed` tác động tới. Phần [addr] có thể là một dòng , hoặc 1 phạm vi bao gồm nhiều dòng hoặc biểu thức regex.`X` là câu lệnh sẽ được thực hiện trên phạm vi chỉ định bởi `[addr]` `[options]` được sử dụng trong 1 số trường hợp. Bạn có thể thực hiện nhiều sed script command bằng cách liên kết chúng qua dấu `;` 
```
# delete content from line 2 to line 4
$ printf "12\n34\n56\n78\n90\n" | sed "2,4d"
12
90

# print content until found string "HERE"
$ printf "12\n34\n56\nHERE\n78\n90\n" | sed "/^HERE/q"
12
34
56
HERE
```
## **Xóa dòng**

```
$ printf "12\n34\n56\n78\n90\n" | sed \'3,4d\'
12
34
90
```

## **Thay thế regax**

```
printf "foo\nfont\nhello foo\nhello\n" | sed "/hello/ s/foo/baz/"
foo
font
hello baz
hello
```

## **awk command**

- `awk`dùng để giải nén và in ra nội dung cụ thể của một file , thường được sử dụng để xây dựng các bản báo cáo. Nó là một công cụ mạnh mẽ và là một trình thông dịch ngôn ngữ lập trình. Làm việc tốt với các dữ liệu theo dạng field (một mẩu dữ liệu riêng lẻ, đặc biệt là các cột ) và các ghi chép ( tập hợp các fields, đặc biệt là các dòng trong file ).

```
[root@localhost ~]# awk '{print $0}' test.txt
hello world
i from Viet Nam
my home is very beautiful
[root@localhost ~]# awk '{print $2}' test.txt
world
from
home
```
## **Grep command**

- Lệnh `grep`để tìm kiếm các từ khóa. Ví dụ tìm trong file tất cả các dòng bắt đầu bằng ký tự `o`

```
grep ^o test.txt
```










