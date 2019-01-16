## Cơ bản về ảo hóa

Là công nghệ giúp khai thác triệt để khả năng làm việc của một máy chủ vật lý. Ảo hóa cho phép vận hành nhiều máy ảo trên cùng một máy chủ vật lý, dùng chung các tài nguyên của một máy chủ vật lý như CPU, Ram, ổ cứng,… và các tài nguyên khác. Các máy ảo khác nhau có thể vận hành hệ điều hành và ứng dụng trên cùng một máy chủ vật lý.

Lợi ích của ảo hóa: Giảm số lượng máy chủ vật lí, giảm lượng điện năng tiêu thụ, tiết kiệm được chi phí cho việc bảo trì phần cứng, nâng cao hiệu quả công việc. Dễ dàng mở rộng hệ thống khi có nhu cầu, triển khai máy chủ ảo nhanh, tận dụng tài nguyên hiện có: vì mỗi máy ảo đơn giản chỉ là một tập tin hoặc một thư mục, ta có thể tạo ra máy chủ ảo mới bằng cách sao chép từ một file của máy chủ ảo hiện tại và cấu hình lại, chọn máy chủ vật lý còn dư tài nguyên để đưa máy chủ ảo mới lên.

## VMware Workstation

VMware là một chương trình tạo máy ảo trên máy tính, nó giúp cho một máy tính có thể chạy song song nhiều hệ điều hành thay vì một hệ điều hành trên một máy như bình thường. Có 3 loại Vmware đó là: Vmware Work Station, Vmware Server và Vmware Vsphere.

VMware Workstation dùng cho desktop, nó là 1 chương trình ứng dụng chạy trên hệ điều hành window hoặc linux giúp cho chúng ta tạo ra máy ảo 1 cách dễ dàng nhằm mục đích thử nghiệm PC hay tần dụng tối đa hiệu năng của PC để làm được nhiều việc khác

-   Tính năng:
    
    -   Hỗ trợ nhiều HĐH
    -   Có 5 tùy chọn Networking phù hợp với nhiều mục đích khác nhau
    -   Tính năng Take Snapshot giúp khôi phục lại máy ảo
    -   Có khả năng kết nối với ESXi host  **Networking**
-   Switch ảo: Cũng giống như switch vật lý, một Virtual Switch kết nối các thành phần mạng ảo lại với nhau. Những switch ảo hay còn gọi là mạng ảo, chúng có tên là VMnet1, VMnet2, VMnet8… Ta có thể thêm, bớt, chỉnh các option của VMnet bằng cách vào menu Edit -> Virtual Network Editor…
![enter image description here](https://lh3.googleusercontent.com/2WrpdhQ_xVlzzUFnW9u7lBuanctluERlXqeB0Ne8WaqreHTpVcW6Ws142DKRHy3MAnzf1fh19xGQ)


- Khi ta tạo các VMnet, thì trên máy thật sẽ tạo ra những card mạng ảo tương ứng với VMnet đó, dùng để kết nối Virtual Switch với máy tính thật, giúp máy thật và máy ảo có thể liên lạc được với nhau.
![enter image description here](https://lh3.googleusercontent.com/n3KfmIHHJCmsnMsZJi78oD9x_msPei4_ACCL-S0J6pmd4oxmKAV1aJkTM2GRiHwgbV4UUcgRoYnD)


- Khi bạn tạo một máy ảo mới, card mạng được tạo ra cho máy ảo, những card mạng này hiển thị trên hệ điều hành máy ảo với tên thiết bị như là AMD PCNET PCI hay Intel Pro/1000 MT Server Adapter. Từ VMware Workstation 6.0 trở về sau này máy ảo có thể hổ trợ đến 10 card, các phiên bản trước bị giới hạn ở 3 card mạng. Thêm bớt card mạng bạn nhấn vào nút Add… hoặc Remove… trong Virtual Machine Setting.

![enter image description here](https://lh3.googleusercontent.com/DRRm_OvqGUrNJ_eJx4ywTM276RnE-_glk7o5N0Z4TP5OS3NLNpuUmocW_rqukHNgdy3eKhCm-yxf)
- Khi copy một máy ảo thì chúng ta nên thay đổi địa chỉ MAC của nó. Vì địa chỉ MAC là địa chỉ duy nhất, cho nên chúng ta nên thay đổi địa chỉ MAC để tránh xảy ra lỗi khi làm việc với hệ thống máy ảo.
![enter image description here](https://lh3.googleusercontent.com/QliYI7BXBgBry-Oh3iBSpXErt1fJiz0hKlLSKReeh2hrp3F32G96TLrZselDSDBCgtniPTAlI4Jr)

- DHCP (Dynamic Host Configuration"> server ảo đảm nhiệm việc cung cấp địa chỉ IP cho các máy ảo trong việc kết nối máy ảo vào các Switch ảo không có tính năng Bridged (VMnet0">. DHCP server ảo cấp phát địa chỉ IP cho các máy ảo có kết nối với VMnet Host-only và NAT.Nếu không muốn sử dụng DHCP server ảo của VMnet , chỉ cần bỏ dấu check tại Use local DHCP service to distribute IP address to VMs. Nếu bạn muốn tùy chỉnh lại DHCP, bạn có thể chọn vào DHCP Setting, ở đây, bạn có thể chỉnh lại các tham số thời gian, tham số Scope IP (lưu ý: Chỉ có thể sửa lại vùng địa chỉ host chứ không được chỉnh lại vùng network">.
![enter image description here](https://lh3.googleusercontent.com/Lth3NxuRClIKyy7w_Ds-GHW6VPhP9DwOq53ZhFGOcJJahDBkI2Fnq-gaO1LKeb-iT7O-n3mLE2jy)
- Các cơ chế hoạt động

-   Chế độ Bridge: ở chế độ này, card mạng trên máy ảo được gắn vào VMnet0, VMnet0 này liên kết trực tiếp với card mạng vật lý trên máy thật, máy ảo lúc này sẽ kết nối internet thông qua card mạng vật lý và có chung lớp mạng với card mạng vật lý.
-   Chế độ NAT: ở chế độ này, card mạng của máy ảo kết nối với VMnet10, VNnet10 cho phép máy ảo đi ra mạng vật lý bên ngoài internet thông qua cơ chế NAT (NAT device">. Lúc này lớp mạng bên trong máy ảo khác hoàn toàn với lớp mạng của card vật lý bên ngoài, hai mạng hoàn toàn tách biệt. IP của card mạng máy ảo sẽ được cấp bởi DHCP của VMnet10, trong trường hợp muốn thiết lập IP tĩnh cho card mạng máy ảo, phải đảm bảo chung lớp mạng với VNnet10 thì máy ảo mới có thể đi internet.
-   Cơ chế Host-only: máy ảo được kết nối với VMnet có tính năng Host-only, trong trường hợp này là các VMnet khác VMnet0,8 . VNnet Host-only kết nối với một card mạng ảo tương ứng ngoài máy thật (như đã nói ở phần trên">. Ở chế độ này, các máy ảo không có kết nối vào mạng vật lý bên ngoài hay internet thông qua máy thật , có nghĩa là mạng VMnet Host-only và mạng vật lý hoàn toàn tách biệt. IP của máy ảo được cấp bởi DHCP của VMnet tương ứng. Trong nhiều trường hợp đặc biệt cần cấu hình riêng, ta có thể tắt DHCP trên VMnet và cấu hình IP bằng tay cho máy ảo.

- Thực hành

- Khởi tạo một network VMnet 10 sử dụng subnet : 192.168.220.0/24, cấp DHCP từ 192.168.220.10 -> 192.168.220.50, và máy ảo gắn sử dụng card này có thể đi ra internet

- Khởi tạo một máy ảo Windown 10 từ ISO. Gồm  2 CPU, 2GB RAM, 32 GB ổ cứng  và sử dụng card mạng trên để ra internet . không có sound card và USB Controller .
![enter image description here](https://lh3.googleusercontent.com/pHxzJU0i8tG1CiqKvOQ3Pqhg-Z3cVAG-MV31WEz7NHAG80QC-icXOaItQZXUKqN_X3DszVdDrTiQ)

![enter image description here](https://lh3.googleusercontent.com/7_UQtLOa8pEQfTvDcB28d1wq7k_HiWCAtdc_g6icwLcJVtevt59TH3YR7xd0fflTuGmwuTDczsYT)
<!--stackedit_data:
eyJoaXN0b3J5IjpbODM1NTU5NjkwXX0=
-->