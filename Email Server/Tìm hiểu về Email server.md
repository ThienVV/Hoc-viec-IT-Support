# Mail Server là gì?

Mail Server hay Email Server là hệ thống máy chủ được cấu hình riêng theo tên miền của doanh nghiệp dùng để gửi và nhận thư điện tử.

Bên cạnh tính năng lưu trữ và sắp xếp các Email trên Internet, Mail Server là một giao thức chuyên nghiệp để giao tiếp thư tín, quản lý và truyền thông nội bộ, giao dịch thương mại… Không chỉ thao tác với tốc độ nhanh chóng và ổn định, Mail Server còn đảm bảo tính an toàn với khả năng khôi phục dữ liệu cao.

Mail Server cơ bản vẫn là Dedicated Server (Server riêng lẻ) hay Cloud Server (Server điện toán đám mây) được cấu hình để biến thành một cỗ máy gửi và nhận thư điện tử. Nó cũng có đầy đủ các thông số như một Server bình thường như Ram, CPU, Storage,… ngoài ra, nó còn có các thông số khác liên quan đến yếu tố Email như số lượng tài khoản Email, Email fowarder, Mail list,…

Cách thức hoạt động của Mail Server

![image](https://user-images.githubusercontent.com/62273292/161193888-254ae71a-a3a8-4b21-a645-932684cef8ca.png)

*Có 3 giao thức hoạt động chính của Mail Server*

Mail Server hoạt động dựa trên 3 giao thức cơ bản bao gồm:

Outgoing Mail Server là gì?

Outgoing Mail Server hay Mail Server gửi đi sử dụng giao thức SMTP (Simple Mail Transfer Protocol). Đây là giao thức dịch chuyển mail đơn giản được dùng để liên lạc với server từ xa. Đồng thời cho phép gửi nhiều thư cùng một lúc tới các server khác nhau.

Incoming Mail Server là gì?

Giao thức này hay còn được biết đến dưới 2 hình thức:

- POP3 (Post Office Protocol phiên bản 3): chuyển email tới lưu ở máy tính chứa Mail Client, thường là nội bộ máy tính của người dùng thông qua một ứng dụng email như Outlook, Mac Mail, Windows Mail…


- IMAP (Internet Message Access Protocol) là phương thức phức tạp hơn cho phép nhiều client cùng lúc kết nối tới một Mailbox. Email từ Mailbox sẽ được sao chép tới máy client và bản gốc của Email vẫn sẽ được lưu trên Mail Server.

## Tính năng nổi bật của Mail Server

![image](https://user-images.githubusercontent.com/62273292/161237513-35636ce4-a982-4b62-a1da-ff37e8d6d9cd.png)

*Hệ thống Mail Server giúp ngăn chặn spam cho người dùng*

**Mail Server** mang đến cho người dùng cá nhân và doanh nghiệp nhiều tính năng:

- Cho phép người dùng khi gửi email hay nhận mail có thể thông qua Internet trực tiếp với những tên miền cụ thể của từng tổ chức.

- Hạn chế tối đa các thư spam hoặc chứa virus.

- Đảm bảo sự bảo mật thông tin nội bộ một cách chặt chẽ.

- Có thể thiết lập dung lượng tối đa cho từng người dùng Mail Server.

- Quản lý được toàn bộ nội dung mail của tất cả các thành viên thuộc hệ thống.

- Thiết lập được chức năng sao lưu dữ liệu tự động. Đảm bảo thông tin cần thiết luôn tồn tại.

## Phân loại Mail Server

Mail server có vai trò rất quan trọng với quá trình kinh doanh của doanh nghiệp

- Mail Server Microsoft, Google là gì?

Mail server Microsoft và Google là 2 cái tên lớn đại diện cho dịch vụ này. Nền tảng xây dựng loại server mail này có quy mô lớn, hệ thống bảo mật chặt chẽ. Có thể quản lý tốt những dữ liệu hiện có. Người dùng có thể sử dụng được nhiều tiện ích khác nhau. Cũng chính vì thế mà giá cả sử dụng dịch vụ server mail loại này thường khá cao. Ví dụ: Email 365 (Microsoft), G Suite (Google),….Tuy nhiên giá cả của các dịch vụ này thường rất đắt, giá trung bình khoảng 5USD/Email /tháng, nếu doanh nghiệp của bạn có số lượng email lớn thì chi phí duy trì hàng tháng rất lớn.

- Mail Server độc lập là gì?

Mail Server độc lập là hệ thống Mail Server được thiết kế cho các tổ chức hoặc ISP xử lý khối lượng thư lớn, yêu cầu kiểm soát và linh hoạt hơn đối với các dịch vụ thư. Nó bổ sung các tính năng như hợp tác, đồng bộ hóa Outlook, quản trị từ xa, Webmail và Quản trị Web nâng cao hơn và kết nối cơ sở dữ liệu, cung cấp cho bạn sức mạnh và kiểm soát cần thiết cho các hoạt động quy mô lớn

## Các thuật ngữ thường đi kèm Mail Server

- TLS Mail Server là gì?

TLS là bảo mật tầng truyền tải (Transport Layer Security). TLS hoạt động cùng với tầng ổ bảo mật SHL (Secure Sockets Layer). Mục đích chính cung cấp phương thức vận chuyển mã hoá cho đăng nhập được chứng thực của SASL.

- SASL Mail Server là gì?

SASL là lớp xác thực và bảo mật đơn giản (Simple Authentication and Security Layer). Để xác thực người dùng. SASL thực hiện xác thực, sau đó TLS cung cấp vận chuyển mã hoá dữ liệu xác thực.

- Webmail là gì?

Webmail là email trên nền website. Một số webmail mà các bạn có thường thấy như hotmail, gmail, yahoo mail. Webmail cho phép người dùng truy cập email bất cứ lúc nào

- SMTP-IN Queue là gì?

Trước khi phân tán thư đến các Local queue hoặc Remote Queue, giao thức SMTP sẽ làm một thao tác sao lưu toàn bộ thư điện tử gửi đi từ email server của doanh nghiệp ở SMTP-IN Queue. Nói cách khác, SMTP-IN Queue chính là kho lưu trữ thông tin thư từ trước khi được gửi đi.

- Webmail là gì?

Webmail là email trên nền website. Một số webmail mà các bạn có thường thấy như hotmail, gmail, yahoo mail. Webmail cho phép người dùng truy cập email bất cứ lúc nào.

- SMTP-IN Queue là gì?

Trước khi phân tán thư đến các Local queue hoặc Remote Queue, giao thức SMTP sẽ làm một thao tác sao lưu toàn bộ thư điện tử gửi đi từ email server của doanh nghiệp ở SMTP-IN Queue. Nói cách khác, SMTP-IN Queue chính là kho lưu trữ thông tin thư từ trước khi được gửi đi.

- Local Queue là gì?

Sau khi tiếp nhận thông tin thư từ, hệ thống sẽ tự động điều phối phân loại và xếp thư từ theo thứ tự ngay hàng thẳng lối trước khi chuyến vào hộp thư của người nhận. Việc xếp hàng các bức thư chính là Local Queue.

Để tăng cường khả năng bảo mật và giữ an toàn cho hệ thống email server, trước khi thư được gửi đến người dùng, local queue và remote queue sẽ tiến hành quét virut. Sau đó kiểm tra spam để chắc chắn về chất lượng thư gửi đi. Tránh trường hợp mail server bị các Blacklist liệt vào danh sách IP spam.

- Local Mailboxes là gì?

Local Mailboxes là hộp thư của các account có đăng kí tài khoản mail server của công ty.

- Email Authentication là gì?

Email Authentication là tính năng xác nhận danh tính của các user khi truy cập vào hộp thư email. Tính năng này giúp bạn bảo mật thông tin thư từ của chính mình. Nói cách khác Alternate Email là một dạng email dự phòng. Khi quên mật khẩu của mail server, bạn có thể sử dụng email này để giúp bạn lấy lại mật khẩu một cách nhanh chóng.

- Mail Exchanger Record (MX) là gì?

MX record có nhiệm vụ là chỉ đường cho email đi đến mail server của bạn. MX record thường đi kèm theo một A record sẽ trỏ về địa chỉ IP của mail server. Một thông số pref có giá trị số để chỉ ra mức độ ưu tiên của các mail server. Giá trị pref càng nhỏ thì mức độ ưu tiên càng cao.




















