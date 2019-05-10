## **Tìm hiểu các loại Cơ sở dữ liệu**

**1. Overview**

- Database (Cơ sở dữ liệu) là một tập hợp dữ liệu đã được tổ chứ sắp xếp. Mục đích chính của database là để tổ chứ một lượng thông tin lớn 

thông tin bằng việc lưu trữ, thu thập và quản lý. 

- RDBMS là viết tắt của Relational Database Management System nghĩa là hệ quản trị cơ sở dữ liệu quan hệ. RDBMS là cơ sở cho SQL, và cho tất

cả hệ thống cơ sở dữ liệu hiện đại như MS SQL Serve, IBM DB2, Oracle, MySQL và Microsoft Access.

Hệ thống quản lý cơ sở dữ liệu quan hệ (RDBMS) là một hệ thống quản lý cơ sở dữ liệu (DBMS) dựa trên mô hình quan hệ được giới thiệu bởi 

EF Codd.

**2. Phân loại database theo mục đích**

Tùy theo mục đích mà có thể phân database theo các loại sau: `Cơ sở dữ liệu dạng file`: dữ liệu được lưu trữ dưới dạng các file có thể là 

text,ascii, .dbf. Tiêu biểu cho cơ sở dữ liệu dạng file là .mdb Foxpro

**Cơ sở dữ liệu quan hệ**: Dữ liệu được lưu trữ trong các bảng dữ liệu gọi là các thực thể, giữa các thực thể này có các mối liên hệ với nhau

gọi là các quan hệ, mối quan hệ có các thuộc tính, trong đó có các thuộc tính khóa chính. Các hệ quản trị hỗ trợ cơ sở dữ liệu quan hệ như:  

 MS SQL server, Oracle, MySQL...

 **Cơ sở dữ liệu hướng đối tượng**: Dữ liệu cũng được lưu trữ bằng các bảng dữ liệu nhưng các bảng có bổ sung thêm các tính năng hướng đối 

 tượng như lưu trữ các hành vi của đối tượng. Mỗi bảng được xem như là một lớp dữ liệu, một dòng dữ liệu trong bảng là một đối tượng. Các hệ

 quản trị có hỗ trợ cơ sở dữ liệu hướng đối tượng như: MS SQL server, Oracle, Postgres 

 **Cơ sở dữ liệu bán cấu trúc**: Dữ liệu được lưu dưới dạng XML, với định dạng này thông tin mô tả về đối tượng thể hiện trong các tag. Đây 

 là cơ sở dữ liệu có nhiều ưu điểm do lưu trữ được hầu hết dữ liệu khác nhau nên cơ sở dữ liệu bán cấu trúc là hướng mới trong nghiên cứu và 

 ứng dụng.

 **3.Một số hệ quản trị cơ sở dữ liệu**

 - PostgreSQL : hệ quản trị cơ sở dữ liệu (CSDL) quan hệ và đối tượng được phát triển tại khoa điện toán Đại học California dựa trên 

 POSTGRES 4.2. Đây là hệ thống CSDL mã nguồn mở tiên tiến nhất (so với các CSDL SQL mã nguồn mở khác như MySQL, MariaDB và Firebird), mở 

 đường cho nhiều hệ quản trị dữ liệu thương mại.

 - MongoDB : Cơ sở dữ liệu không ràng buộc, nó lưu trữ dữ liệu trong các document dạng JSON với schema động rất linh hoạt. Nghĩa là bạn có  

 thể lưu các bản ghi mà không cần lo lắng về cấu trúc dữ liệu như là số trường, kiểu của trường lưu trữ. Tài liệu MongoDB tương tự như các 

 đối tượng JSON.

- MYSQL :  Hỗ trợ các cơ sở dữ liệu lớn, lên tới 50 triệu hàng hoặc nhiều hơn nữa trong một bảng. Kích cỡ file mặc định được giới hạn cho 

một bảng là 4 GB, nhưng bạn có thể tăng kích cỡ này (nếu hệ điều hành của bạn có thể xử lý nó) để đạt tới giới hạn lý thuyết là 8 TB.

- MariaDB : là một nhánh của MySQL( một trong những CSDL phổ biến trên thế giới ), là máy chủ cơ sở dữ liệu cung cấp các chức năng thay thế 

cho MySQL. MariaDB được xây dựng bởi một số tác giả sáng lập ra MySQL được sự hỗ trợ của đông đảo cộng đồng các nhà phát triển phần mềm mã 

nguồn mở. Ngoài việc kế thừa các chức năng cốt lõi của MySQL, MariaDB cung cấp thêm nhiều tính năng cải tiến về cơ chế lưu trữ, tối ưu máy 

chủ.

- Oracle : được tích hợp tất cả các công cụ để quản trị cũng như nhập xuất dữ liệu nên rất tiện lợi cho người quản trị, có thể cài đặt trên 

đa hệ điều hành.

- NoSQL : một lớp các hệ cơ sở dữ liệu không sử dụng mô hình quan hệ (RDBMS). RDBMS vốn tồn tại khá nhiều nhược điểm như có hiệu năng không 

tốt nếu kết nối dữ liệu nhiều bảng lại hay khi dữ liệu trong một bảng là rất lớn.

-TimescaleDB : read-time data

- Redis: Redis là một trong số các Hệ quản trị cơ sở dữ liệu phát triển theo phong cách NoSQL. Redis là hệ thống lưu trữ key-value với rất 

nhiều tính năng và được sử dụng rộng

- SQlite: SQLite là hệ thống cơ sở dữ liệu quan hệ nhỏ gọn, hoàn chỉnh, có thể cài đặt bên trong các trình ứng dụng khác. SQLite được viết

 dưới bằng ngôn ngữ lập trình C

- Elasticsearch : hoạt động như 1 web server, có khả năng tìm kiếm nhanh chóng thông qua giao thức RESTful APII .Elasticsearch có khả năng

phân tích và thống kê dữ liệu

**5. Tìm hiểu MYSQL**

Mysql là một trong những cơ sở dữ liệu có khả năng mở rộng phổ biến nhất hiện nay. Tập hợp nhiều tính năng, là một sản phẩm mã nguồn mở mạnh

mẽ trên các website và các ứng dụng online. Việc bắt đầu với MySQL là cực kỳ dễ dàng và nhà phát triển dễ dàng tiếp cận với một lượng lớn 

các thông tin về cơ sở dữ liệu trên internet. 

- Ưu điểm của MySQL

	- **Dễ dàng sử dụng**: MySQL có thể dễ dàng cài đăt. Với các công cụ bên thứ 3 làm cho nó dễ đơn giản hơn để có thể sử dụng.

	- **Giàu tính năng**: MySQL hỗ trợ rất nhiều chức năng SQL được mong chờ từ một hệ quản trị cơ sở dữ liệu quan hệ-cả trực tiếp lẫn gián 

	tiếp.

	- **Bảo mật**: Có nhiều tính năng bảo mật đều được xây dựng trong MySQL

	- **Khả năng mở rộng và mạnh mẽ**: MySQL có thể xử lý rất nhiều dữ liệu và hơn thế nữa nó có thể mở rộng nếu cần thiết. 

	- **Nhanh**: Việc đưa ra một số tiêu chuẩn cho phép MySQL để làm việc hiệu quả và tiết kiệm chi phí, do đó làm tăng tốc độ thực thi.

## **Tìm hiểu PostgreSQL**

Postgre SQL là hệ quản trị cơ sở dữ liệu quan hệ mã nguồn mở tiên tiến mà mục đích tuân thủ theo chuẩn và khả năng mở rộng. Postgre SQL hay 

còn gọi là Postgree áp dụng SQL ANSI/IOS cùng với các phiên bản. 

So với các hệ quản trị cơ sở dữ liệu dạng quan hệ khác, PostgreSQL khá khác. Nó hỗ trợ hướng đối tượng mạnh mẽ và chức năng cơ sở dữ liệu 

quan hệ. Ví dụ như hỗ trợ hoàn toàn cho các giao dịch đáng tin cậy như là Atomicity, Consistency, Isolation, Durability (ACID).

- Ưu điểm của PostgreSQL

	- **Là một chuẩn SQL phù hợp với hệ quản trị cơ sở dữ liệu quan hệ**: PostgreSQL là hệ quản trị cơ sở dữ liệu quan hệ mã nguồn mở, miễn

	 phí và mạnh mẽ

	- **Cộng đồng mạnh**: PostgreSQL được hỗ trợ bởi một cộng đồng nhiệt tình và đầy kinh nghiệm.

	- **Hỗ trợ mạnh mẽ từ các bên thứ 3:** Bất kể các tính năng tiên tiến thì PostgreSQL đều được hỗ trợ bởi các công cụ tuyệt vời của bên 

	 thứ 3 trong việc quản lý cơ sơ dữ liệu

	 - **Sự mở rộng**: Nó có thể mở rộng lập trình PostgreSQL với các thủ tục lưu trữ, giống như một RDBMS tiên tiến.

	 - **Đối tượng hóa**: PostgreSQL không chỉ là một hệ quản trị cơ sở dữ liệu quan hệ, mà nó còn đối tượng hóa dữ liệu.

- Nhược điểm của PostgreSQL

	-**Hiệu suất**: Đối với các toán tử đơn giản thì PostgreSQL thực hiện kém hiệu quả hơn so với các hệ quản trị cơ sở dữ liệu quan hệ 

	khác như MySQL. Nhưng đối với toán tử phức tạp thì PostgreSQL thực hiện tốt hơn rất nhiều

**7. Tìm hiểu NOSQL**

- NoSQL có nghĩa là Non-Relational (NoRel) – không ràng buộc. Tuy nhiên, thuật ngữ đó ít phổ dụng hơn và ngày nay người ta thường dịch 

NoSQL thành Not Only SQL – Không chỉ SQL. NoSQL ám chỉ đến những cơ sở dữ liệu không dùng mô hình dữ liệu quan hệ để quản lý dữ liệu trong 

lĩnh vực phần mềm. Người ta phát triển NoSQL xuất phát từ yêu cầu cần những database có khả năng lưu trữ dữ liệu với lượng cực lớn, truy 

vấn dữ liệu với tốc độ cao mà không đòi hỏi quá nhiều về năng lực phần cứng cũng như tài nguyên hệ thống và tăng khả năng chịu lỗi.

- Các dạng NoSQL cơ bản

**Key – value data stores**: Dữ liệu được dưới dạng cắp key-value. Giá trị được truy xuất thông qua key.

	- **Ví dụ**: Redis, Dynomite, Project Voldemort.

	- **Thường cho**: Content caching Applications

	- **Ưu điểm**: Tìm kiếm nhanh

	- **Nhược điểm**: Lưu dữ liệu không theo khuôn dạng nhất định


**Column-based – Tabular**: Cơ sở dữ liệu tổ chức dưới dạng các bảng. Gần giống với mô hình RDBMS. Tuy nhiên, chúng lưu giữ dữ liệu bởi các 

cột chứ không phải bằng các dòng. Nó khá thích hợp với để hiển thị bằng các phần mềm quản lý kho dữ liệu

	- **Ví dụ** : Apache Hbase, Apache Cassandra, Hypertabl

	- **Thường cho**: các hệ phân tán file

	- **Ưu điểm**: Tìm kiếm nhanh, Phân tán dữ liệu tốt

	- **Nhược điểm:** Hỗ trợ được với rất ít phần mềm

**Document-based**: Dữ liệu (bán cấu trúc hay semi-structured) được lưu trữ và tổ chức dưới dạng một tập hợp các document. Các document này 

linh hoạt, mỗi document có một tập nhiều trường.

	- **Ví dụ** : Apache CouchDB và MongoDB

	- **Thường cho**: Web applications

	- **Ưu điểm**: Dùng khi dữ liệu nguồn không được mô tả đầy đủ

	- **Nhược điểm**: Hiệu năng truy vấn, Không có cú pháp chuẩn cho câu truy vấn dữ liệu

**Graph-based data-stores**: Những CSDL này áp dụng lý thuyết đồ thị trong khoa học máy tính để lưu trữ và truy xuất dữ liệu. Chúng tập trung vào tính rời rạc giữa các phần dữ liệu. Các phần tử đơn vị dữ liệu được biểu thị như một nút và liên kết với các thành phần khác bằng các cạnh.


	- **Ví dụ** : Neo4j, InfiniteGraph, DEX

	- **Thường cho**: Social networking, Hệ trợ giúp

	- **Ưu điểm:** Ứng dụng các thuật toán trên đồ thị như Đường đi ngắn nhất, liên thông,…

	- **Nhược điểm**: Phải duyệt nội bộ đồ thị, để trả lời lại các truy vấn. Không dễ để phân tán









