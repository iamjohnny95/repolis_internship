# **Iptables**

### ***Netfilter là gì***

 - Netfilter là một khung bên trong linux giúp cung cấp sự linh hoạt cho các hoạt động mạng khác nhau để phù hợp với các cách xử lý khác nhau. Netfilter có các lựa chọn như: packet filtering, network address translation, và port translation. Các phương thức của Netfilter sẽ cung cấp các hướng dẫn cho packet trong phạm vi dễ ảnh hưởng trong mạng máy tính. Netfilter là một framework cho các packet filtering software nằm ở bên trong các bản Linux kernel từ 2.4 đổ lên.

- Các software nằm bên trong framework này có thể lọc, NAT và mangling gói tin

- netfilter, ip_tables, connection tracking (ip_conntrack, nf_conntrack) và NAT subsystem là những nhân tố chính tạo lên framework này.

- Netfilter đại diện cho một tập các hooks trong mạng máy tính (trong lập trình hooks bao gồm các kỹ thuật sử dụng để thay đổi hoặc tăng cường hành vi của một hệ điều hành, các ứng dụng, hoặc các thành phần phần mềm khác bằng cách chặn các chức năng như cuộc gọi, tin nhắn hay các sự kiện như các thành phần phần mềm) 


### ***Iptables là gì***

- Iptables là firewall được cấu hình để lọc gói dữ liệu rất mạnh, miễn phí có sẵn trên linux 

- Tích hợp tốt với kenel của Linux. Có khả năng phân tích package hiệu quả. Lọc package dựa vào MAC và một số cờ hiệu trong TCP Header. Cung cấp chi tiết các tùy chọn để ghi nhận sự kiện hệ thống. Cung cấp kỹ thuật NAT. Có khả năng ngăn chặn một số cơ chế tấn công theo kiểu DOS.

- Gồm 2 phần là Netfilter ở trong nhân linux và iptables nằm ngoài nhân. Iptables làm nhiệm vụ giao tiếp giữa người dùng Netfilter để đẩy các rules từ người dùng vào cho netfilter xử lý. Netfilter làm việc trong kernel nhanh mà không ảnh hưởng đến tốc độ hệ thống. 


### ***Tính năng của iptables***

- Tích hợp tốt với Linux Kernel, để cải thiện sự tin cậy và tốc độ chạy iptables cũng như đảm bảo ở mức tối thiểu tài nguyên tiêu tốn cần dùng cho việc lọc gói tin. 

- Quan sát kỹ tất cả các gói dữ liệu. Điều này cho phép firewall theo dõi một kết nối thông qua nó, và xem xét nội dung của từng luồng dữ liệu để từ đó tiên liệu hành động kế tiếp của các giao thức. Điều này rất quan trọng hỗ trợ các giao thức DNS, FTP.

- Việc lọc gói tin dựa trên địa chỉ MAC và các cờ trong TCP header. Điều này giúp ngăn chặn việc tấn công bằng cách sử dụng các gói tin dị dạng và ngăn chặn truy cập nội bộ đến một mạng khác bất chấp IP của nó. 

- Ghi chép hệ thống (System logging) cho phép việc điều chỉnh mức độ của báo cáo. 

- Hỗ trợ việc tích hợp các trình Web Proxy chẳng hạn như Squid. 

- Ngăn chặn hiệu quả các kiểu tấn công từ chối dịch vụ cũng như các tình huống tấn công khác. 

- Cung cấp kỹ thuật NAT linh hoạt. 

### ***Cơ chế xử lý gói tin trong iptables*** 

- Iptables cơ bản gồm 3 thành phần chính: Tables, chain, target

- Table

Các table được sử dụng để định nghĩa các rules cụ thể cho các gói tin. Có 4 loại table khác nhau:

|**Name**|**Định nghĩa**|
|------|------|
|Filter table|Quyết định gói tin được gửi tới đích hay không|
|Magle table|Bảng quyết định sửa head của gói tin (Các giá trị của các trường TTL, MTU, Type of Service)
|Nat table|Cho phép route các gói tin đến các host khác nhau trong mạng NAT, cách đổi ip nguồn và ip đích của gói tin|
|Raw table|Một gói tin có thể thuộc một kết nối mới hoặc cũng có thể là một kết nối đã tồn tại. Table raw cho phép bạn làm việc với gói tin trước khi kernel kiểm tra trạng thái gói tin|

 - Chain

 Mỗi table được tạo ra với mỗi một sô chain nhất định. Chain cho phép lọc gói tin tại các "hook points" khác nhau. Netfilter định nghĩa ra 5 "hook point" khác nhau trong quá trình xử lý gói tin của kernel: PREROUTING, INPUT, FORWARD, POSTROUTING, OUTPUT. 

 - Các build-int chains được gán vào các hook point và có thể add một loạt các rules cho mỗi hook points.

 - Chains không chỉ nằm trên một table và một table không chỉ chứa một chain 

 |Hook points| Cho phép xử lý các packet|
 |-------|---------|
 |PREROUTING|vừa mới tiến vào từ network interface. Nó sẽ được thực thi trước khi quá trình routing diễn ra, thường dùng cho DNAT (destination NAT)|
 |INPUT|có địa chỉ đích đến là server của bạn|
 |FORWARD|có đích là một server khác nhưng không được tạo được server của bạn. Chain này là cách cơ bản để cấu hình server của bạn để route các request tới một thiết bị khác|
 |OUTPUT|được tạo bởi server của bạn|
 |POSTROUTING|đi ra ngoài hoặc forward sau khi quá trình routing hoàn tất, chỉ trước khi nó tiền vào đường truyền, thường dùng cho SNAT (source NAT)|

 - Target 

 Target đơn giản là các hoạt động áp dụng cho các gói tin. Đối với những gói tin đúng theo rule mà chúng ta đặt ra thì các hành động (target) có thể được thực hiện đó là:

 - Accept: Chấp nhận gói tin 

 - Drop: Loại bỏ gói tin, không có gói tin trả lời, phía nguồn sẽ không biết đích có tồn tại hay không.

 - Reject: Loại bỏ gói tin nhưng có trả lời table gói tin khác, ví dụ trả lời table 1 gói tin "connection reset" đối với gói TCP hoặc bản tin "destination host unreachable" đối với gói UDP và ICMP. 

 - Log: chấp nhận gói tin và ghi log lại 

 Khi có nhiều rule, gói tin sẽ đi qua tất cả các rule chứ không chỉ dừng lại khi đã đúng với một rule đầu. Đối với gói tin, không khớp với rule nào thì mặc định sẽ được chấp nhận. 

 - Bảng NAT

 Bảng NAT có 3 chain được xây dựng sẵn trong table NAT là 

 - Chain PREROUTING: Ví dụ đối với gói tin tcp có port đích là 80 thì sẽ đổi địa chỉ đích thành 10.0.30.100: `iptables -t NAT -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 10.0.30.100:80`

 - Chain POSTROUTING: Ví dụ đổi địa chỉ nguồn với gói tin tcp thành 10.0.30.200: `ptables -t NAT -A POSTROUTING -p tcp -j SNAT --to-source 10.0.30.200`

 - Chain Output

 Bảng filter:

 - Chain Input

 - Chain Forward

 - Chain Postrouting

 - Chain Prerouting

 ### **Quá trình xử lý gói tin** 

 Đầu tiên, khi gói tin đi vào từ mạng sẽ qua PREROUTING trước. Tại đây gói tin sẽ đi qua bảng mangle để thay đổi một số thông tin header, sau đó sẽ đi tới bảng NAT để quyết định xem có thay đổi IP đích không (DNAT), tiếp theo sẽ đi vào bộ định tuyến routing để quyết định xem gói tin có được qua firewall không. Ở đây có 2 trường hợp:

   - Nếu là local packets thì sẽ được đưa tới chain INPUT. Tại chain INPUT, packets sẽ đi qua bảng mangle và bảng filter để kiểm tra các chính sách (rule), ứng với mỗi rule cụ thể sẽ được áp dụng cho mỗi target, packet có thể được chấp nhận hoặc hủy bỏ. Tiếp theo packet sẽ được chuyển lên cho các ứng dụng (client/server) xử lí local và chuyển ra chain OUTPUT với các bảng mangle, nat, filter, gói tin có thể bị thay đổi các thông số, bị lọc hoặc bị hủy bỏ.

   - Nếu là forwarded packets, gói tin sẽ đi tới chain FORWARD, qua table mangle và filter. Đây là chain được sử dụng rất nhiều để bảo vệ người dùng trong mạng LAN với người sử dụng internet, các gói tin phải thỏa mãn các rule mới được chuyển qua các card mạng với nhau.

  Sau khi đi qua chain OUTPUT hoặc FORWARD, gói tin đi tiếp tới chain POSTROUTING (sau khi được định tuyến), tại chain này packets đi qua bảng mangle, nat có thể bị thay đổi ip nguồn (SNAT) hoặc Masquerade trước khi đi ra ngoài mạng

  ### **Iptables command**

  - Để xem các rule đang có trong iptables

 ```
 iptables -L -v
 ```
Trong đó:

- TARGET: Hành động sẽ thực thi.

- Accept: gói dữ liệu được chuyển tiếp để xử lý tại ứng dụng cuối hoặc hệ điều hành

- Drop: gói dữ liệu bị chặn, loại bỏ

- Reject: gói dữ liệu bị chặn, loại bỏ đồng thời gửi một thông báo lỗi tới người gửi

- Log: Thông tin của nó sẽ được đưa vào syslog để kiểm tra. Iptables tiếp xúc xử lý gói tiin với quy luật kế tiếp. –log-prefix “string”: 

- Iptables sẽ thêm vào log message một chuổi (string) do người dùng định sẳn. Thông thường để thông báo lý do vì sao gói bị loại bỏ

- DNAT: Dùng để thực hiện thay đổi địa chỉ đích của gói dữ liệu. –to-destination ipaddress iptables sẽ viết lại địa chỉ ipaddress vào địa chỉ đích của gói tin,

- SNAT: Thay đổi địa chỉ nguồn của gói dữ liệu.

- MASQUERADE: Dùng để thay đổi địa chỉ ip nguồn. Mặc định thì địa chỉ ip nguồn sẽ giống với ip của firewall.

- PROT: Là viết tắt của chữ Protocol, nghĩa là giao thức. Tức là các giao thức sẽ được áp dụng để thực thi quy tắc này. Ở đây chúng ta có 3 lựa chọn là all, tcp hoặc udp. Các ứng dụng như SSH, FTP, sFTP,..đều sử dụng giao thức kiểu TCP.

- IN: chỉ ra rule sẽ áp dụng cho các gói tin đi vào từ interface nào, chẳng hạn như lo, eth0, eth1 hoặc any là áp dụng cho tất cả interface.

- OUT: Tương tự như IN, chỉ ra rule sẽ áp dụng cho các gói tin đi ra từ interface nào.

- DESTINATION: Địa chỉ của lượt truy cập được phép áp dụng quy tắc.

Ví dụ: 

`ACCEPT all  -- lo any anywhere  anywhere`

- Nghĩa là chấp nhận toàn bộ gói tin từ interface lo (interface loopback), chẳng hạn như là ip 127.0.0.1 là kết nối qua thiết bị này.

`ACCEPT all  -- any any anywhere anywhere ctstate RELATE,ESTABLISHED`

- Chấp nhận toàn bộ gói tin của kết nối hiện tại. Nghĩa là khi bạn đang ở trong SSH và sửa đổi lại Firewall, nó sẽ không đá bạn ra khỏi SSH nếu bạn không thỏa mãn quy tắc 

`ACCEPT tcp  -- any any anywhere anywhere tcp  dtp:http`

- Cho phép kết nối vào cổng 80, mặc định hiểu thành http

`ACCEPT tcp  -- any any anywhere anywhere tcp  dtp:https`

- Cho phép kết nối vào cổng 443, mặc định sẽ hiểu thành https.

`DROP      all    --   any  any   anywhere   anywhere`

- Loại bỏ tất cả các gói tin nếu không khớp với các rule ở trên. 

**Tạo một rule mới**

`iptables -A INPUT -i lo -j ACCEPT`

Trong đó:

- A INPUT: Khai báo kiểu kết nối sẽ được áp dụng (A nghĩa là append).

- i lo: khai báo thiết bị mạng đang được sử dụng (nghĩa là interface)

- j-ACCEPT: Khai báo hành động sẽ được áp dụng cho quy tắc này (j:JUMP)

gõ `iptables -L -v` bạn sẽ thấy xuất hiện một rule mới 

Sau khi thêm mới hoặc thay đổi bất cứ gì thì cần lưu và khởi động lại service

```
service iptables restart
```

Tiếp tục bây giờ chúng ta thêm một rule mới để cho phép lưu lại các kết nối hiện tại để tránh hiện tượng tự block bạn ra khỏi máy chủ.

```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

Trong đó:

- `-m contrac`: Áp dụng cho các kết nối thuộc module tên là “Connection Tracking“. Module này sẽ có 4 kiểu kết nối là NEW, ESTABLISHED, RELATED và INVALID. Cụ thể là ở quy tắc này chúng ta sẽ sử dụng kiểu RELATED và ESTABLISHED để lọc các kết nối đang truy cập.

- ctstate RELATED,ESTABLISHED : Khai báo loại kết nối được áp dụng cái module Connection Tracking mà mình đã nói ở trên. 

Ví dụ: 

- Cho phép các cổng được truy cập từ bên ngoài vào qua giao thức tcp: SSH(22)

`iptables -A INPUT -p tcp --dport 22 -j ACCEPT`

Trong đó:

- `p tcp`: Giao thức được áp dụng (tcp,udp,all)

- `dport 22`: Cổng cho phép áp dụng. 22 là cho SSH

Cuối cùng chặn toàn bộ các kết nối truy cập từ bên ngoài vào nếu không thỏa mãn các rule trên.

`iptables -A INPUT -j DROP`

**Thêm một rule mới** 

- Nếu muốn chèn một rule mới vào một hàng nào đó, ví dụ hàng 2 thì thay tham số `-A` thành tham số `INSERT -I` 

`iptables -I INPUT 2 -p tcp --dport 8080 -j ACCEPT`

**Xóa một rule** 

Để xóa 1 rule mà bạn đã tạo ra tại vị trí 4, ta sẽ sử dụng tham số -D

`iptables -D INPUT 4`

Xóa toàn bộ các rule chứa hành động DROP có trong iptables:

`iptables -D INPUT -j DROP`

Kiểm tra xem đã xóa thành công chưa 

**Chặn một ip**

Nếu muốn chặn một ip 59.45.175.62 thì bạn cần thêm một rule mới vào INPUT chain của table filter, sử dụng lệnh sau:

`iptables -t filter -A INPUT -s 59.45.175.62 -j REJECT`

Ngoài ra chúng ta cũng hoàn toàn có thể chặn cả dải địa chỉ IP với việc sử dụng CIDR.

`iptables -A INPUT -s 59.45.175.0/24 -j REJECT`

Tương tự bạn có thể chặn traffic đi tới một IP hoặc một dải IP nào đó bằng cách sử dụng OUTPUT chain:

`iptables -A OUTPUT -d 31.13.78.35 -j DROP`



