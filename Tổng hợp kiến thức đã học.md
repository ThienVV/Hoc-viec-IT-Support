## Tóm tắt lưu ý học việc những gì đã làm và chưa làm

**Database:**

Đã tìm hiểu
- Cài đặt sử dụng MSSQL trên windows server
	+ tạo database và tạo các bảng.
	+ Sử dụng câu lệnh để xem, thêm, sửa, xóa.
- Cài đặt và tìm hiểu MariaDB trên CentOS7
	+  sử dụng miễn phí, khắc phục những hạn chế của MySQL bổ sung thêm nhiều Engine, kết hợp SQL và NoSQL đặc biệt là tốc độ nhanh hơn.
	+  một số thao các cơ bản: dùng lệnh tạo, thêm, sữa, xóa … và nhập xuất dữ liệu người dùng bằng lệnh, xuất dữ liệu thì tạo thư mực để chứa dữ liệu còn nhập dữ liệu thì phải xóa database trước.
	+ một số lệnh cơ bản: tạo người dùng, gán quyền người dùng, phân quyền cho user database.
- Cài đặt và tìm hiểu Mysql trên Ubuntu: 
	+ tạo cơ sỡ dữ liệu và sử dụng các lênh cơ bản thêm sữa xóa và import, export dữ liệu.
- Tìm hiểu những tính năng Phpmyadmin
	+ giống như mysql nhưng phải thao tác thủ công mới có thể import và export dữ liệu được.
	+ không thể tự xuất database, hạn chế truy cập url từ những ip cố định
- Cài đặt Phpmyadmin với apache trên CentOS 7:
- Cài đặt Phpmyadmin với apache trên Ubuntu:

**Email server**

Đã làm được:

Giải pháp Email server phổ biến bao gồm: Microsoft exchange, MDaemon, Zimbra, Dịch vụ lưu trữ, Thư điện tử trên tên miền Google với email server có tính khôi phục dữ liệu cao, nhận mail thông qua tên miền cụ thể, cần cấu hình email server, nếu không sẽ ở trạng thái default sẽ không tối ưu cho sử dụng.

- Tìm hiểu và cài đặt zimbra:
	+ zimbra có nhiều tính năng như: thư điện tử, lịch công tác, sổ địa chỉ cá nhân, danh mục công việc, tài liệu hồ sơ, chat trên nội bộ mạng lan hoặc trên internet
	+ zimbra với tính năng bảo mật cao, có 2 phần mềm cho client: zimbra desktop và zimbra web client, zimbra còn hổ trợ làm việc trên di động.
	+ Cài đặt máy chủ zimbra trên CentOS7: trước hết chúng ta cần tạo 1 domain rồi thiết lập DNS cần thiết để gửi mail.
	+ Cấu hình cho zimbra: cần tăng độ tin cậy cho mail gửi đi: cụ thể là thêm các bản ghi thiết lập trong DNS 

- Tìm hiểu và cài dặt MDaemon:
	+ MDaemon là một giải pháp email server doanh nghiệp nổi tiếng canh tranh với microsoft exchange và giá rẻ hơn ở microsoft, cần triển khai 1 máy chủ và 1 ip riêng ổn định.
	+ Cài đặt MDaemon trên windows server 2019: tải về và cài đặt.

Chưa làm được:
	+ Lỗi không gửi được mail do địa chỉ ip bị backlist (spam)

**File Server**

File server là một máy tính kết nối mạng để lưu hình ảnh ... các workstation (máy trạm) kết nối với máy chủ 

- Mạng SAN là dùng để kết nối nhiều máy tính với nhau truyền tải dữ liệu qua lại với nhau. đặc biệt có thể khởi động trực tiếp từ san, thay đổi update khi đang sử dụng
- Giao thức NFS dùng để chia sẻ các file

**Firewall**

Tường lửa chuỗi quy tắt (rules) ngăn cả sự  truy cập từ bên ngoài và kiểm soát truy cập.
- FTP: dùng để tải tệp tin
- TCP: hổ trợ loại bỏ xây dượng thông tin internet
- Http: dùng cho các website
- SMTP: dùng để gửi thông tin định dạng văn bản
- TELNET: dùng để thực hiện 1 lệnh từ xa 
- ICMP: trao đổi thông tin với các router

**Phần load balancing:**

Đã tìm hiểu:
- Giúp máy chủ ảo hoạt động đồng bộ hơn cụ thể là nếu server chủ bị lỗi, thì load balancing sẽ di chuyển đến máy chủ khác để k bị gián đoạn.
- Bảo mật thông tin 
- Có 4 giao thức mà load balancing xử lý:
	+ HTTP: gửi thông tin về backend.
	+ HTTPS: tương tự như http nhưng được mã hóa rồi gửi đén backend
	+ TCP: khi http và https k hoạt động thì sử dụng TCP truy cập vào csdl, TCP truyền lưu đượng đến máy chủ
	+ UDP: Load Balancer đã bổ sung thêm hỗ trợ cho cân bằng tải giao thức internet lõi như DNS và syslogd sử dụng UDP.
-  Health Checks: kiểm tra tình trạng hoạt động của backend server
- Load balancer có 2 loại: 
	+ layer 4: hoạt động trên dữ liệu tìm thấy của giao thức IP, TCP, FTP, UDP.
	+ layer 7: phân phối các yêu cầu dựa trên dữ liệu được tìm thấy giữa các ứng dụng như http, giúp chạy nhiều webserver trên 1 domain và port.
Chưa tìm hiểu: chưa cài đặt và cấu hình load balancing.
