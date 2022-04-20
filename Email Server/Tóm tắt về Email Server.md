
Hi,
ANh đã xem qua báo cáo, có 1 số nhận xét như sau:
- Phần tìm hiểu, định nghĩa thì a không nhắc tới
- Phần cài đặt, các bước em đã làm qua => vấn đề cần lưu lại trong kiến thức là gì?
cụ thể:
+ Yêu cầu để cài đặt được các email server (cho từng loại là gì)
+ Những chú ý khi cài cho từng loại là gì
Tiếp đó, sau khi cài đặt xong thì sang phần cấu hình => Cần chú ý gì trong cấu hình của các email server này? Nếu không cấu hình gì thì email server sẽ ở trạng thái default , khi đó sẽ không tối ưu cho sử dụng

Xong phần cấu hình sẽ là phần sử dụng.
Ở bước này, anh cần e làm rõ 2 mục:
1- Hướng dẫn sử dụng cho người quản trị (tức là tài khoản ADMIN)
2- Hướng dẫn sử dụng cho người dùng con (tức là End User)

Chỉ khi có được các hướng dẫn này, em mới biết cách thao tác, hướng dẫn hỗ trợ.

Và cuối cùng, là phần trace log trong các trường hợp cần thiết. Cụ thể:
+ Biết được Logs của từng email server nằm ở đâu, đường dẫn nào
+ Mỗi loại log cho ta biết thông tin gì
+ Phân tích luồng mail gửi nhận dựa trên các dòng logs.
+ Đặc biệt, tìm hiểu về các return code, error code => ý nghĩa của chúng
ví dụ:
http://www.greenend.org.uk/rjk/tech/smtpreplies.html
https://datatracker.ietf.org/doc/html/rfc3463


## Phần cài đặt, các bước em đã làm qua => vấn đề cần lưu lại trong kiến thức là gì?

- Trong những phần cài đặt và các bước cài đặt, vấn đề lưu lại là:

+ Đầu tiên là tạo domain, em đã tìm nhiều tài liệu và website để tạo domain miễn phí nhưng k thành công, cuối cùng củng k đâu vào đâu.
+ Thiết lập DNS còn chưa hiểu rõ bản chất phải tìm hiểu lại. còn các phần cài đặt khác thì củng bình thường. giống như tài liệu

- Yêu cầu để cài đặt được các email server:

**Về phần zimbra**

+ Trước hết muốn cài đặt được email server thì chắc chắn phải có domain.

**Về Phần MDaemon**

+ Phải đăng ký tên miền


































