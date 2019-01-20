# Lý thuy?t v? VMware(update b? sung thêm 1 s? các yêu c?u)
## Tìm hi?u 3 ch? d? card m?ng 
**Ch? d? Bridge:**
- ? ch? d? này, card m?ng trên máy ?o du?c g?n vào VMnet0, VMnet0 này liên k?t tr?c ti?p v?i card m?ng v?t lý trên máy th?t, máy ?o lúc này s? k?t n?i internet thông qua  card m?ng v?t lý và có chung l?p m?ng v?i card m?ng v?t lý.
**Ch? d? Nat:**
- Áp d?ng co ch? Nat d?a ch? Ip cho phép nhi?u máy tính k?t n?i m?ng qua 1 d?a ch? publish. ? ch? d? này máy ?o có kh? nang k?t n?i m?ng nhung d?i d?a ch? khác v?i máy th?t
**Ch? d? Host- Only:**
- Cho phép t?o ra các máy ?o v?i d?a ch? t? t?o có th? k?t n?i v?i nhau. S? d?ng trong tru?ng h?p t?o m?t m?ng riêng. Có th? k?t n?i m?ng n?u cài d?t DNS

## Gateway c?a 3 ki?u m?ng
**Ch? d? Bridge**
- Gateway s? tr? d?n d?a ch? m?ng v?t lý c?a router hay wifi
**Ch? d? Nat** 
- Gateway s? tr? d?n d?a ch? inside local
**Ch? d? Host-Only**
- Gateway s? tr? d?n d?i m?ng v?t lý mình t?o ra

## Khái ni?m v? LAN Segment 
- Các card m?ng c?a máy ?o có th? g?n k?t v?i nhau thành t?ng LAN Segment. Không gi?ng nhu VMnet, LAN Segment ch? k?t n?i các máy ?o du?c gán trong m?t LAN Segment l?i v?i nhau mà không có nh?ng tính nang nhu DHCP và LAN Segment không th? k?t n?i ra máy th?t nhu các Virtual Switch VMnet. 

## Phân vùng ? c?ng cho Ubuntu ? dây có 4 s? l?a ch?n
- Guided - use entire disk: S? d?ng cho ? c?ng chua t?ng du?c phân vùng, máy tính s? t? d?ng format l?i toàn b? ? c?ng và d?nh d?ng cho t?ng vùng dã chia.
- Guided - use entire disk and with set up LVM: T? d?ng phân vùng b?ng LVM, là m?t phuong pháp cho phép ?n d?nh không gian dia c?ng thành nh?ng logical volume, khi?n cho vi?c thay d?i kích thu?c các ? dia d? dàng hon mà không ph?i s?a l?i table c?a OS. Trong tru?ng h?p b?n dã s? d?ng h?t ph?n b? nh? còn tr?ng c?a partition và mu?n m? r?ng dung lu?ng thì LVM là m?t s? l?a ch?n t?t.
- Guided - use entire disk and with set encrypted up LVM: Gi?ng v?i l?a ch?n 2 nhung s? cài d?t mã hóa ? c?ng d? tang tính b?o m?t.
- Manual: Phân vùng th? công.
## Nat Advance 
- Khi m?t máy ?o trong VMWare s? d?ng card m?ng NAT thì s? du?c NAT ra ngoài m?ng qua d?a ch? c?a máy th?t, và các máy t? m?ng ngoài s? không th? truy c?p vào các máy trong d?i NAT dó. N?u mu?n truy c?p vào du?c (ví d? ssh vào m?t máy ?o bên trong dang s? d?ng NAT) thì c?n t?o du?ng và cho phép máy bên ngoài truy câp vào.
- Ví d?:
  - M?t máy Ubuntu có ip 192.168.220.10
  - Ip máy th?t có d?a ch? : 192.168.100.11
  - Vào VMWare -> Ch?n Edit -> Virtual Network Editor

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/1.png)

  - Thay d?i cài d?t -> Change Setting làm theo hình

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/2.png)

  - Ch?n c?ng n?m trong d?i kh? d?ng mà máy th?t c?a b?n chua s? d?ng

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/3.png)

  - Luu l?i, và ssh vào máy ?o b?ng d?a ch? máy th?t qua port 1111. ? dây tôi s? d?ng Xshell. Sau dó dang nh?p m?t kh?u

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/5.png)


# Lý thuy?t v? VMware(update b? sung thêm 1 s? các yêu c?u)
## Tìm hi?u 3 ch? d? card m?ng 
**Ch? d? Bridge:**
- ? ch? d? này, card m?ng trên máy ?o du?c g?n vào VMnet0, VMnet0 này liên k?t tr?c ti?p v?i card m?ng v?t lý trên máy th?t, máy ?o lúc này s? k?t n?i internet thông qua  card m?ng v?t lý và có chung l?p m?ng v?i card m?ng v?t lý.
**Ch? d? Nat:**
- Áp d?ng co ch? Nat d?a ch? Ip cho phép nhi?u máy tính k?t n?i m?ng qua 1 d?a ch? publish. ? ch? d? này máy ?o có kh? nang k?t n?i m?ng nhung d?i d?a ch? khác v?i máy th?t
**Ch? d? Host- Only:**
- Cho phép t?o ra các máy ?o v?i d?a ch? t? t?o có th? k?t n?i v?i nhau. S? d?ng trong tru?ng h?p t?o m?t m?ng riêng. Có th? k?t n?i m?ng n?u cài d?t DNS

## Gateway c?a 3 ki?u m?ng
**Ch? d? Bridge**
- Gateway s? tr? d?n d?a ch? m?ng v?t lý c?a router hay wifi
**Ch? d? Nat** 
- Gateway s? tr? d?n d?a ch? inside local
**Ch? d? Host-Only**
- Gateway s? tr? d?n d?i m?ng v?t lý mình t?o ra

## Khái ni?m v? LAN Segment 
- Các card m?ng c?a máy ?o có th? g?n k?t v?i nhau thành t?ng LAN Segment. Không gi?ng nhu VMnet, LAN Segment ch? k?t n?i các máy ?o du?c gán trong m?t LAN Segment l?i v?i nhau mà không có nh?ng tính nang nhu DHCP và LAN Segment không th? k?t n?i ra máy th?t nhu các Virtual Switch VMnet. 

## Phân vùng ? c?ng cho Ubuntu ? dây có 4 s? l?a ch?n
- Guided - use entire disk: S? d?ng cho ? c?ng chua t?ng du?c phân vùng, máy tính s? t? d?ng format l?i toàn b? ? c?ng và d?nh d?ng cho t?ng vùng dã chia.
- Guided - use entire disk and with set up LVM: T? d?ng phân vùng b?ng LVM, là m?t phuong pháp cho phép ?n d?nh không gian dia c?ng thành nh?ng logical volume, khi?n cho vi?c thay d?i kích thu?c các ? dia d? dàng hon mà không ph?i s?a l?i table c?a OS. Trong tru?ng h?p b?n dã s? d?ng h?t ph?n b? nh? còn tr?ng c?a partition và mu?n m? r?ng dung lu?ng thì LVM là m?t s? l?a ch?n t?t.
- Guided - use entire disk and with set encrypted up LVM: Gi?ng v?i l?a ch?n 2 nhung s? cài d?t mã hóa ? c?ng d? tang tính b?o m?t.
- Manual: Phân vùng th? công.
## Nat Advance 
- Khi m?t máy ?o trong VMWare s? d?ng card m?ng NAT thì s? du?c NAT ra ngoài m?ng qua d?a ch? c?a máy th?t, và các máy t? m?ng ngoài s? không th? truy c?p vào các máy trong d?i NAT dó. N?u mu?n truy c?p vào du?c (ví d? ssh vào m?t máy ?o bên trong dang s? d?ng NAT) thì c?n t?o du?ng và cho phép máy bên ngoài truy câp vào.
- Ví d?:
  - M?t máy Ubuntu có ip 192.168.220.10
  - Ip máy th?t có d?a ch? : 192.168.100.11
  - Vào VMWare -> Ch?n Edit -> Virtual Network Editor

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/1.png)

  - Thay d?i cài d?t -> Change Setting làm theo hình

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/2.png)

  - Ch?n c?ng n?m trong d?i kh? d?ng mà máy th?t c?a b?n chua s? d?ng

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/3.png)

  - Luu l?i, và ssh vào máy ?o b?ng d?a ch? máy th?t qua port 1111. ? dây tôi s? d?ng Xshell. Sau dó dang nh?p m?t kh?u

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/5.png)


