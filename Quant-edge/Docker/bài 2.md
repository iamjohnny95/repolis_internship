# **BÀI 2**

## **Làm thế nào để chạy một Container**

**Nội dung**

- Làm thế nào để chạy một Container

- Chạy một Container (nginx web server)

- Điều gì xảy ra khi chạy một Container?

- Containerization (Docker vs VM)

- Vào trong Shell của Container

## **Container vs Virtual Machine**

- Đầu tiên Container không phải là mini- virtual machine, chỉ là những process. Container thay lớp Hypervisor bằng Container Engine

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/Docker/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/Docker/1.png)

Và trên Container Engine là lớp bash/shell. Nó coi Container như là một process chứ k phải 1 hệ điều hành. So với máy ảo thông thường thì t

tài nguyên trên Container bị hạn chế, tối giản đi nhiều chỉ bao gồm thư viện và file binary cấu hình lên app. Vì nó là 1 process nên nó sẽ 

tắt khi process tắt. Container không có kernel riêng, nó dùng kernel của OS

**Container và Image**

- **Docker Image** là tập hợp các file hệ thống mà ứng dụng chúng muốn chạy. 

- **Docker Container** là kết quả khi ta chạy ứng dụng đó như một tiến trình. Nó như là một ứng dụng như là NodeJS, PHP... thì Docker Image

 là tập hợp những cái file mà chúng ta chạy để cài đặt những Node JS, PHP, MySQL... Còn Container là kết quả khi chạy ứng dụng lên.

 - **Docker Hub** là kho chứa các **Docker Image**

- Có thể chạy nhiều Container khác nhau trên cùng một Docker Image.

- Mặc định Docker Image được lưu trên "registry": Docker Hub

**Cách để chạy một Container**

```
Docker container run --publish 80:80 nginx
```

Đây là command để chạy một webserver nginx. Chú thích câu lệnh:

- `Nginx` ở đây là docker image mà mình download từ Docker Hub về

- Chữ `run` là command để chạy Container từ Nginx lên. 

- Mở port để mở port trên máy, còn số sau là port trên container.

Sau đó ta có thể mở để test trên web địa chỉ local của mình 

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/Docker/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/Docker/2.png)

**Chuyện gì đã xảy ra khi chạy một Container**?

[![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/Docker/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/Docker/3.png)

1. Tìm kiếm Docker Image ở trên host trong image ở trên host trong image cache và không tìm được.

2. Nó tìm kiếm Image trong image repository(Docker Hub ở trên mạng)

3. Tải về phiên bản mới nhất 

4. Tạo một Container mới trên Image mới tải về 

5. Cấp một Virtural IP trên Private Network bên trong Docker Engine 

6. Mở port 80 trên host và chuyển dữ liệu đến port 80 của Container 

7. Khởi động Container bằng cách chạy lệnh CMD trong bản Dockerfile của Image

**Thay đổi các giá trị mặc định**

```
docker container run --publish 8080:80 --name webhost -d nginx:1.11
```

**Bài tập**

- Chạy database server Mysql server 

- Chạy chế độ --detach (hoặc -d) là chế độ chạy ngầm, đặt tên Container --name mysql 3306:3306

- Khi chạy mysql, sử dụng tùy chọn --env (hoặc -e) để thêm vào MYSQL_RANDOM_ROOT_PASSWORD=yes. Để khi Container chạy lên nó sẽ tự động sinh 

ra một password mặc định.

- Sau khi chạy xong chạy câu lệnh `docker container logs` trên mysql để tìm kiếm mật khẩu. 

- Dừng và xóa Container với câu lệnh `docker container stop` và `docker container remove`

- Sử dụng `docker container ls` để  kiểm tra trước khi xóa container.

```
docker container run --name mysql -d -p 3306:3306 --env MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
```

Để xem password được sinh ra sử dụng câu lệnh 

```
docker container logs mysql
```

**Lưu ý** một image có thể chạy nhiều container ví dụ như

```
docker container run --name mysql1 -d -p 3307:3306 --env MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
```

Ta vừa tạo 2 docker container mysql nhưng khác port

Lệnh dừng container đang chạy

```
docker container stop "dùng id của mysql đang chạy"
```
Để kiểm tra id của mysql hay những tiến trình container đang chạy khác ta sử dụng câu lệnh 

```
docker container ls
```

Câu lệnh ở trên chỉ hiện thị nhưng container đang chạy. Còn muốn kiểm tra toàn bộ container có mặt trên host (bao gồm cả những container đã 

bị dừng). Ta sử dụng câu lệnh 

```
docker container ls -a
```
xóa container 

```
docker container rm "tên container hoặc id"
```

Có thể xóa 1 hay nhiều container cùng lúc

**Bài tập 2**

- Chạy hai `nginx` và `httpd` server

- Chạy ở chế độ --detach (hoặc -d), đặt tên Container

- Nginx server chạy port 80, apache server chạy port 8080 trên host 

- Sử dụng câu lệnh `docker container logs` để kiểm tra truy cập đến server

- Dừng và xóa Container với câu lệnh `docker container stop` và `docker container rm`

- Sử dụng câu lệnh `docker container ls` để kiểm tra trước khi xóa Container

Để chạy câu lệnh cài webserver

```
docker container run --name web-nginx-1 -d  --publish 80:80 nginx
```
```
docker container run --name web-apache-1 -d --publish 8080:80 httpd
```

**Điều gì xảy ra trên container**

Liệt kê các process trên Container 

```
docker container top
```

Các cấu hình của một Container 

```
docker container inspect
```
Thống kê hiệu năng của tất cả các Container

```
docker container stats
```

**Ví dụ**

để kiểm tra các tiến trình trên con web server nginx vừa tạo 

```
docker container top web-nginx-1
```
Để tra thêm thông tin của container 

```
docker container inspect web-nginx-1
```

Để xem host có bao nhiêu container đang chạy và nó chiếm bao nhiêu CPU,RAM,băng thông, tốc độ đọc ghi. Xem sức khỏe của Container trên hệ thống

```
docker container stats
```

**Vào trong Shell của Container**

```
docker container run -it
```

Tham số để tương tác với Shell khi khởi tạo Container 

```
docker container exec -it
```
Chạy câu lệnh mở rộng tương tác với Container 

Ví dụ xem bên trong shell của con web-nginx 

```
docker container exec -it web-httpd /bin/bash
```
Câu lệnh này sử dụng khi đã tải image về và thao tác vào container cũ 

Còn câu lệnh dưới đây là câu lệnh thao tác trực tiếp vào container khi vừa mới tải xong 

```
docker container run -it name web-nginx bash
```

Sau khi vào được shel bên trong ta gõ command `ls` lúc này sẽ thấy các thư mục như 1 hệ điều hành. Để thoát ra sử dụng lệnh `exit`

Kiểm tra lại trạng thái bằng câu lệnh 

```
docker container ps -a
```
thì ta thấy lệnh đã tắt. Lý do là: Command này đã thay đổi bằng cách thêm command bash. Command bash này chính là cái process mà docker 

nginx nó quản lý cái con container proxy này. Nên khi tắt cái shell này thì process cũng tắt. Process này cũng là process quản lý của con 

container này 



