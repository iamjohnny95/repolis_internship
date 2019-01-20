# L� thuy?t v? VMware(update b? sung th�m 1 s? c�c y�u c?u)
## T�m hi?u 3 ch? d? card m?ng 
**Ch? d? Bridge:**
- ? ch? d? n�y, card m?ng tr�n m�y ?o du?c g?n v�o VMnet0, VMnet0 n�y li�n k?t tr?c ti?p v?i card m?ng v?t l� tr�n m�y th?t, m�y ?o l�c n�y s? k?t n?i internet th�ng qua  card m?ng v?t l� v� c� chung l?p m?ng v?i card m?ng v?t l�.
**Ch? d? Nat:**
- �p d?ng co ch? Nat d?a ch? Ip cho ph�p nhi?u m�y t�nh k?t n?i m?ng qua 1 d?a ch? publish. ? ch? d? n�y m�y ?o c� kh? nang k?t n?i m?ng nhung d?i d?a ch? kh�c v?i m�y th?t
**Ch? d? Host- Only:**
- Cho ph�p t?o ra c�c m�y ?o v?i d?a ch? t? t?o c� th? k?t n?i v?i nhau. S? d?ng trong tru?ng h?p t?o m?t m?ng ri�ng. C� th? k?t n?i m?ng n?u c�i d?t DNS

## Gateway c?a 3 ki?u m?ng
**Ch? d? Bridge**
- Gateway s? tr? d?n d?a ch? m?ng v?t l� c?a router hay wifi
**Ch? d? Nat** 
- Gateway s? tr? d?n d?a ch? inside local
**Ch? d? Host-Only**
- Gateway s? tr? d?n d?i m?ng v?t l� m�nh t?o ra

## Kh�i ni?m v? LAN Segment 
- C�c card m?ng c?a m�y ?o c� th? g?n k?t v?i nhau th�nh t?ng LAN Segment. Kh�ng gi?ng nhu VMnet, LAN Segment ch? k?t n?i c�c m�y ?o du?c g�n trong m?t LAN Segment l?i v?i nhau m� kh�ng c� nh?ng t�nh nang nhu DHCP v� LAN Segment kh�ng th? k?t n?i ra m�y th?t nhu c�c Virtual Switch VMnet. 

## Ph�n v�ng ? c?ng cho Ubuntu ? d�y c� 4 s? l?a ch?n
- Guided - use entire disk: S? d?ng cho ? c?ng chua t?ng du?c ph�n v�ng, m�y t�nh s? t? d?ng format l?i to�n b? ? c?ng v� d?nh d?ng cho t?ng v�ng d� chia.
- Guided - use entire disk and with set up LVM: T? d?ng ph�n v�ng b?ng LVM, l� m?t phuong ph�p cho ph�p ?n d?nh kh�ng gian dia c?ng th�nh nh?ng logical volume, khi?n cho vi?c thay d?i k�ch thu?c c�c ? dia d? d�ng hon m� kh�ng ph?i s?a l?i table c?a OS. Trong tru?ng h?p b?n d� s? d?ng h?t ph?n b? nh? c�n tr?ng c?a partition v� mu?n m? r?ng dung lu?ng th� LVM l� m?t s? l?a ch?n t?t.
- Guided - use entire disk and with set encrypted up LVM: Gi?ng v?i l?a ch?n 2 nhung s? c�i d?t m� h�a ? c?ng d? tang t�nh b?o m?t.
- Manual: Ph�n v�ng th? c�ng.
## Nat Advance 
- Khi m?t m�y ?o trong VMWare s? d?ng card m?ng NAT th� s? du?c NAT ra ngo�i m?ng qua d?a ch? c?a m�y th?t, v� c�c m�y t? m?ng ngo�i s? kh�ng th? truy c?p v�o c�c m�y trong d?i NAT d�. N?u mu?n truy c?p v�o du?c (v� d? ssh v�o m?t m�y ?o b�n trong dang s? d?ng NAT) th� c?n t?o du?ng v� cho ph�p m�y b�n ngo�i truy c�p v�o.
- V� d?:
  - M?t m�y Ubuntu c� ip 192.168.220.10
  - Ip m�y th?t c� d?a ch? : 192.168.100.11
  - V�o VMWare -> Ch?n Edit -> Virtual Network Editor

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/1.png)

  - Thay d?i c�i d?t -> Change Setting l�m theo h�nh

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/2.png)

  - Ch?n c?ng n?m trong d?i kh? d?ng m� m�y th?t c?a b?n chua s? d?ng

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/3.png)

  - Luu l?i, v� ssh v�o m�y ?o b?ng d?a ch? m�y th?t qua port 1111. ? d�y t�i s? d?ng Xshell. Sau d� dang nh?p m?t kh?u

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/5.png)


# L� thuy?t v? VMware(update b? sung th�m 1 s? c�c y�u c?u)
## T�m hi?u 3 ch? d? card m?ng 
**Ch? d? Bridge:**
- ? ch? d? n�y, card m?ng tr�n m�y ?o du?c g?n v�o VMnet0, VMnet0 n�y li�n k?t tr?c ti?p v?i card m?ng v?t l� tr�n m�y th?t, m�y ?o l�c n�y s? k?t n?i internet th�ng qua  card m?ng v?t l� v� c� chung l?p m?ng v?i card m?ng v?t l�.
**Ch? d? Nat:**
- �p d?ng co ch? Nat d?a ch? Ip cho ph�p nhi?u m�y t�nh k?t n?i m?ng qua 1 d?a ch? publish. ? ch? d? n�y m�y ?o c� kh? nang k?t n?i m?ng nhung d?i d?a ch? kh�c v?i m�y th?t
**Ch? d? Host- Only:**
- Cho ph�p t?o ra c�c m�y ?o v?i d?a ch? t? t?o c� th? k?t n?i v?i nhau. S? d?ng trong tru?ng h?p t?o m?t m?ng ri�ng. C� th? k?t n?i m?ng n?u c�i d?t DNS

## Gateway c?a 3 ki?u m?ng
**Ch? d? Bridge**
- Gateway s? tr? d?n d?a ch? m?ng v?t l� c?a router hay wifi
**Ch? d? Nat** 
- Gateway s? tr? d?n d?a ch? inside local
**Ch? d? Host-Only**
- Gateway s? tr? d?n d?i m?ng v?t l� m�nh t?o ra

## Kh�i ni?m v? LAN Segment 
- C�c card m?ng c?a m�y ?o c� th? g?n k?t v?i nhau th�nh t?ng LAN Segment. Kh�ng gi?ng nhu VMnet, LAN Segment ch? k?t n?i c�c m�y ?o du?c g�n trong m?t LAN Segment l?i v?i nhau m� kh�ng c� nh?ng t�nh nang nhu DHCP v� LAN Segment kh�ng th? k?t n?i ra m�y th?t nhu c�c Virtual Switch VMnet. 

## Ph�n v�ng ? c?ng cho Ubuntu ? d�y c� 4 s? l?a ch?n
- Guided - use entire disk: S? d?ng cho ? c?ng chua t?ng du?c ph�n v�ng, m�y t�nh s? t? d?ng format l?i to�n b? ? c?ng v� d?nh d?ng cho t?ng v�ng d� chia.
- Guided - use entire disk and with set up LVM: T? d?ng ph�n v�ng b?ng LVM, l� m?t phuong ph�p cho ph�p ?n d?nh kh�ng gian dia c?ng th�nh nh?ng logical volume, khi?n cho vi?c thay d?i k�ch thu?c c�c ? dia d? d�ng hon m� kh�ng ph?i s?a l?i table c?a OS. Trong tru?ng h?p b?n d� s? d?ng h?t ph?n b? nh? c�n tr?ng c?a partition v� mu?n m? r?ng dung lu?ng th� LVM l� m?t s? l?a ch?n t?t.
- Guided - use entire disk and with set encrypted up LVM: Gi?ng v?i l?a ch?n 2 nhung s? c�i d?t m� h�a ? c?ng d? tang t�nh b?o m?t.
- Manual: Ph�n v�ng th? c�ng.
## Nat Advance 
- Khi m?t m�y ?o trong VMWare s? d?ng card m?ng NAT th� s? du?c NAT ra ngo�i m?ng qua d?a ch? c?a m�y th?t, v� c�c m�y t? m?ng ngo�i s? kh�ng th? truy c?p v�o c�c m�y trong d?i NAT d�. N?u mu?n truy c?p v�o du?c (v� d? ssh v�o m?t m�y ?o b�n trong dang s? d?ng NAT) th� c?n t?o du?ng v� cho ph�p m�y b�n ngo�i truy c�p v�o.
- V� d?:
  - M?t m�y Ubuntu c� ip 192.168.220.10
  - Ip m�y th?t c� d?a ch? : 192.168.100.11
  - V�o VMWare -> Ch?n Edit -> Virtual Network Editor

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/1.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/1.png)

  - Thay d?i c�i d?t -> Change Setting l�m theo h�nh

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/2.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/2.png)

  - Ch?n c?ng n?m trong d?i kh? d?ng m� m�y th?t c?a b?n chua s? d?ng

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/3.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/3.png)

  - Luu l?i, v� ssh v�o m�y ?o b?ng d?a ch? m�y th?t qua port 1111. ? d�y t�i s? d?ng Xshell. Sau d� dang nh?p m?t kh?u

  [![](https://github.com/iamjohnny95/repolis_internship/raw/master/img/VM/5.png)](https://github.com/iamjohnny95/repolis_internship/blob/master/img/VM/5.png)


