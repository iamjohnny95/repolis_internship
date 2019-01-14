# Hướng dẫn Network in VMware Workstation
### Hướng dẫn Network in VMware Workstation
-   1. [Network](http://ksec.info/tags/network/) mặc định khi mới cài đặt VMware
- -   2. Các thao tác với một card mạng ảo trong VMware Workstation
    -   2.1. Thêm, xóa một vmnet – Thêm một vmnet – Xóa một vmnet
    -   2.2. Sửa dải IP của một vmnet
    -   2.3. Cấu hình DHCP
    -   2.4. Cách thêm một card mạng vào máy ảo
VMware Workstation là một phần mềm ảo hóa dùng cho desktop mạnh và rất phổ biến.

Tính năng của nó thì không cần giới thiệu nhiều, chắc hẳn ai trong chúng ta cũng đều biết cách tạo một máy ảo trong VMware. Tuy nhiên trong quá trình lab nhiều bài lab với VMware Workstation đôi khi gặp trường hợp mạng giữa các máy ảo và máy thật không thông, địa chỉ IP của máy ảo tự nhiên bị thay đổi,..vv.

**Chú ý:**

-   Phiên bản VMware sử dụng là VMware Workstation 12
-   Host cài đặt VMware Workstation: Windows 10 Pro 64bit
-   Quy ước: các card mạng ảo trong VMware sẽ được gọi là vmnetx (với x là số thứ tự của card mạng)

**1. Network mặc định khi mới cài đặt VMware**  
Khi mới cài đặt VMware Workstation, mặc định phần mềm sẽ cài cho chúng ta 2 card mạng:

-   Một card bridge, card này sử dụng chính card mạng thật của chúng ta để kết nối ra ngoài Internet (card ethernet hoặc wireless). Do đó khi sử dụng card mạng này IP của máy ảo sẽ cùng với dải IP của máy thật.

Ưu điểm: đơn giản, ra được internet và cùng dải máy thật nên cấu hình gì cũng dễ dàng.

Nhược điểm: nhiều trường hợp dùng card bridge cấu hình bình thường và đến khi nơi nào không có mạng (lên lớp chẳng hạn) thì hỏi “hôm qua làm bình thường, sao nay lại không kết nối được?”  
=> mất mạng là mất hết!!!!

Một card Nat, card này sẽ Nat địa chỉ IP của máy thật ra một địa chỉ khác cho máy ảo sử dụng. Card này cũng có thể kết nối ra bên ngoài Internet.

Để xem các card mạng đã có trong VMware Workstation ta chỉ cần bật VMware lên, chọn Edit => Virtual Network Editor

![[​IMG]](https://camo.githubusercontent.com/685edb82d7771ab1f538102d5af1efb621c9e849/687474703a2f2f692e696d6775722e636f6d2f48513643334e702e706e67)

Ta có thể thấy trong hình card bridge có tên là VMnet0, card Nat có tên là VMnet8  
Card bridge không có địa chỉ IP do nó sẽ sử dụng dải IP của máy thật. VMware sẽ tự sinh một dải IP và gán cho VMnet8. Trong trường hợp này là dải 192.168.238.0/24.

Một lưu ý quan trọng đó là việc chọn card mạng trên máy ảo, bây giờ mình sẽ nói rõ hơn. Khi cài đặt, VMWare tạo ra ở máy thật 2 card mạng ảo:

-   VMWare Virtual Ethernet Adapter for VMnet1
-   VMWare Virtual Ethernet Adapter for Vmnet8

![dffdffd](https://psglee.files.wordpress.com/2015/07/dffdffd.png?w=611)

Hai card mạng này có thể được sử dụng để máy thật giao tiếp với các máy tính ảo. Khi “gắn” một card mạng vào một máy ảo, card mạng này có thể được chọn 1 trong 3 loại sau:

-   Bridge: ở chế độ này, card mạng trên máy ảo được gắn vào VMnet0, VMnet0 này liên kết trực tiếp với card mạng vật lý trên máy thật, máy ảo lúc này sẽ kết nối internet thông qua card mạng vật lý và có chung lớp mạng với card mạng vật lý.
-   ![](https://public.sn2.livefilestore.com/y2pt0QnN_xQOE_pgIJRAxtK5EM-sTUw3tPhgNsDZSts-Qh6fZ0W_qxt6WIiUui_jP8QpGgV0aatQfIFo39L_MjwKRk2v0XHixtbEMALXPlrISQ/briged.png?psid=1)
    -   Card Bridge trên máy ảo chỉ có thể giao tiếp với card mạng thật trên máy thật.
    -   Card mạng Bridge này có thể giao tiếp với mạng vật lý mà máy tính thật đang kết nối.
-   Host-only: máy ảo được kết nối với VMnet có tính năng Host-only, trong trường hợp này là VMnet1 . VNnet Host-only kết nối với một card mạng ảo tương ứng ngoài máy thật (như đã nói ở phần trên). Ở chế độ này, các máy ảo không có kết nối vào mạng vật lý bên ngoài hay internet thông qua máy thật , có nghĩa là mạng VMnet Host-only và mạng vật lý hoàn toàn tách biệt. IP của máy ảo được cấp bởi DHCP của VMnet tương ứng. Trong nhiều trường hợp đặc biệt cần cấu hình riêng, ta có thể tắt DHCP trên VMnet và cấu hình IP bằng tay cho máy ảo.![](https://public.sn2.livefilestore.com/y2pP5x5S-hctvRaGYnS19WRmpkhDnqGeWbKsqJrxMmcJgj4nplOWuXgZ6VmlYVVQJhr2O771zgIP0tH7WHIbdaCaAZKF_ms1PqKptl3ioj-COI/host-only.png?psid=1)
    -   Card Host-only chỉ có thể giao tiếp với card mạng ảo VMnet1 trên máy thật.
    -   Card Host-only chỉ có thể giao tiếp với các card Host-only trên các máy ảo khác.
    -   Card Host-only không thể giao tiếp với mạng vật lý mà máy tính thật đang kết nối.
-   NAT: ở chế độ này, card mạng của máy ảo kết nối với VMnet8, VNnet8 cho phép máy ảo đi ra mạng vật lý bên ngoài internet thông qua cơ chế NAT (NAT device). Lúc này lớp mạng bên trong máy ảo khác hoàn toàn với lớp mạng của card vật lý bên ngoài, hai mạng hoàn toàn tách biệt. IP của card mạng máy ảo sẽ được cấp bởi DHCP của VMnet8, trong trường hợp bạn muốn thiết lập IP tĩnh cho card mạng máy ảo bạn phải đảm bảo chung lớp mạng với VNnet8 thì máy ảo mới có thể đi internet.![](https://public.sn2.livefilestore.com/y2pvoXPJXGiHRiv4zknu2S7UJjcxNmiQXMNkFNlkZcSIgqKXV6631h6n3sBnQ6BTue9rr4PvO2Leemq816L5Hk_oUjUhvYzxwsoTCJ9S-3FByk/NAT.png?psid=1)
    -   Card NAT chỉ có thể giao tiếp với card mạng ảo VMnet8 trên máy thật.
    -   Card NAT chỉ có thể giao tiếp với các card NAT trên các máy ảo khác.
    -   Card NAT không thể giao tiếp với mạng vật lý mà máy tính thật đang kết nối. Tuy nhiên nhờ cơ chế NAT được tích hợp trong VMWare, máy tính ảo có thể gián tiếp liên lạc với mạng vật lý bên ngoài.

**2. Các thao tác với một card mạng ảo trong VMware Workstation**  
**2.1. Thêm, xóa một vmnet**  
**Thêm một vmnet**  
Cũng trong Virtual Network Editor ta chọn như sau:

![[​IMG]](https://camo.githubusercontent.com/0112c25af7636ee16891bc928582e9bf07d9a125/687474703a2f2f692e696d6775722e636f6d2f633548326c4f4c2e706e67)

-   Bước 1: chọn Add Network
-   Bước 2: chọn card cần add thêm (ở đây là VMnet1)
-   Bước 3: ấn OK

Lúc này trên cửa sổ Virtual Network Editor sẽ xuất hiện thêm card VMnet1 và được gắn tự động một dải IP, như hình dưới đây:

![[​IMG]](https://camo.githubusercontent.com/5ed4c02e4de5da0bb048bf66ac48b2bd2aa4f965/687474703a2f2f692e696d6775722e636f6d2f4b3644435347382e706e67)

Làm tương tự để add thêm các vmnet tiếp theo.  
**Xóa một vmnet**  
Trong Virtual Network Editor chọn một vmnet và ấn Remove Network (button cạnh Add Network)

**2.2. Sửa dải IP của một vmnet**  
Có thể thấy các dải IP mà VMware tự sinh ra và gắn cho các card mạng rất khó nhớ. Ta có thể thay đổi dải IP này bằng cách ấn vào vmnet muốn đổi địa chỉ.  
Trong dòng Subnet IP chọn dải IP và subnet muốn thay đổi.

![[​IMG]](https://camo.githubusercontent.com/a22f66e3d1e68b1a65cdf7edc5636073c4f74478/687474703a2f2f692e696d6775722e636f6d2f386139506a6f432e706e67)

Click Apply và OK  
**2.3. Cấu hình DHCP**  
Các card mạng này có thể cấp DHCP cho các máy ảo sử dụng nó.  
để làm việc này ta ấn vào DHCP Settings, sau đó chọn dải IP dùng để cấp DHCP

![[​IMG]](https://camo.githubusercontent.com/12d6ecf547ea042eca943d478ee251b18f864622/687474703a2f2f692e696d6775722e636f6d2f526267484b50452e706e67)

**2.4. Cách thêm một card mạng vào máy ảo**  
Ví dụ ở đây có một máy ảo Ubuntu Server gắn sẵn một card bridge khi tạo máy ảo.  
Show IP trên máy ảo:

![[​IMG]](https://camo.githubusercontent.com/10545216908ab7b65329db9e760654a30069532d/687474703a2f2f692e696d6775722e636f6d2f61544d576955452e706e67)

Thêm card mạng thứ 2 vào máy ảo bằng cách vào Edit Virtual Machine Settings, chọn Add => Network và làm theo hình dưới:

![[​IMG]](https://camo.githubusercontent.com/3c1221bf4005c1ba642d6cd315994ace12c00192/687474703a2f2f692e696d6775722e636f6d2f547833436664322e706e67)

Xin cấp IP cho card mạng mới trên máy ảo bằng lệnh **_dhclient eth1_**  
IP của máy ảo sau khi thực hiện xong (đã có thêm card eth1):

![[​IMG]](https://camo.githubusercontent.com/618580711bc4f1fdca4b78ea6dc9b206a6ea8e65/687474703a2f2f692e696d6775722e636f6d2f71664c454566632e706e67)

Đối với trường hợp muốn thay đổi từ card bridge (hoặc nat hoặc vmnet) sang card khác thì chỉ cần chọn vào card cần đổi và làm như bước 3 bên trên (không add thêm card mới)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDA0NzE1N119
-->