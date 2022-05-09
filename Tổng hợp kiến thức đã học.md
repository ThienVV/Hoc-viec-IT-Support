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
