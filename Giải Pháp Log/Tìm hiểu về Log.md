# Mô hình triển khai hệ thống thu thập Log cơ bản

**Giới thiệu về log**

- Log ghi lại liên tục các thông báo về hoạt động của cả hệ thống hoặc của các dịch vụ được triển khai trên hệ thống và file tương ứng. Log file thường là các file văn bản thông thường dưới dạng “clear text”, có thể dễ dàng đọc được bằng các trình soạn thảo văn bản (vi, vim, nano...) hoặc các trình xem văn bản thông thường (cat, tailf, head...) là có thể xem được file log. Các file log có thể cung cấp các thông tin cần biết, để giải quyết các vấn đề với các ứng dụng, tiến trình được ghi vào log.

- Tóm lại:

          + Log = Thời điểm + Dữ liệu.

          + Log ghi lại những hoạt động của hệ thống.

![image](https://user-images.githubusercontent.com/62273292/164176703-052db1ca-f65b-4dad-8797-7472aa9a9415.png)

**Một vòng đời của Log**

- Bao gồm 5 bước chính được minh họa trong hình trên cụ thể là:

+ Đầu tiên log sẽ được ghi lại tại chính máy local sau đó nó sẽ được vận chuyển sang máy chủ quản lý log.

+ Người quản trị mạng sẽ từ những bản ghi đó mà tiến hành phân tích, từ đó có thể giám sát được hoạt động của các máy client.

+ Qua bước phân tích này mà người quản trị có thể phát hiện các hoạt động, hành vi xâm nhập không được phép.

+ Sau khi phân tích, dữ liệu log sẽ được lưu trữ để sử dụng lại nếu cần.

+ Bước cuối cùng là xóa, thường những tập tin log không cần thiết có thể được xóa bởi người quản trị nhằm giảm bớt lượng thông tin log không cần thiết.

**Công dụng của Log**

- Phân tích nguyên nhân khi có sự cố xảy ra.

- Giúp cho việc khắc phục sự cố nhanh hơn khi hệ thống gặp vấn đề.

- Giúp cho việc phát hiện, dự đoán một vấn đề có thể xảy ra đối với hệ thống.

- Khi xử lý log, thường quản trị viên có thể sử dụng 1 trong 2 phương pháp, đó là: xử lý log trên local và xử lý log tập trung.

**Log trên Local**

- Chỉ lưu lại bản thân Server

- Dùng command find, tail… để xem log.

![image](https://user-images.githubusercontent.com/62273292/164176888-c5b1e0a1-44be-447e-9977-f68fe76a24a1.png)


**Log tập trung**

- Log tâp trung là quá trình tập trung, thu thập, phân tích... các log cần thiết từ nhiều nguồn khác nhau về một nơi an toàn để thuận lợi cho việc phân tích, theo dõi hệ thống.

**Lợi ích của Log tập trung:**

- Giúp quản trị viên có cái nhìn chi tiết về hệ thống -> có định hướng tốt hơn về hướng giải quyết.

- Mọi hoạt động của hệ thống được ghi lại và lưu trữ ở một nơi an toàn (log server) -> đảm bảo tính toàn vẹn phục vụ cho quá trình phân tích điều tra các cuộc tấn công vào hệ thống.

- Log tập trung kết hợp với các ứng dụng thu thập và phân tích log khác nữa giúp cho việc phân tích log trở nên thuận lợi hơn -> giảm thiểu nguồn nhân lực.

- Log máy local đẩy về máy Log Server.

- Mỗi ứng dụng có giao thức đẩy Log khác nhau.

![image](https://user-images.githubusercontent.com/62273292/164176989-737cf724-2202-405f-9c85-5561697dbce4.png)


**Lợi ích của quản trị tập trung Log:**

- Để có thể đánh giá khái quát về tình trạng an toàn, an ninh thông tin của một cơ quan, tổ chức, thì việc thu thập, phân tích và lưu trữ các sự kiện an toàn thông tin (ATTT) từ các thiết bị, dịch vụ và ứng dụng như: Router, Switch, Firewall, IDS/IPS, Mail Security, Web Security, Anti-Virus, ứng dụng Mail, Web, cơ sở dữ liệu, hệ điều hành… là hết sức cần thiết.

- Chính vì thế, hệ thống quản lý Log tập trung hay cao hơn là SIEM được ra đời với mục tiêu thu thập và liên kết tất cả các sự kiện trên cả hệ thống mạng giúp các quản trị viên có cái nhìn tổng quan và thống nhất về các vấn đề trên cả hệ thống.

- Quản trị tập trung Log giúp quản lý và phân tích các sự kiện an toàn thông tin, thực hiện thu thập, chuẩn hóa, lưu trữ và phân tích tương quan toàn bộ các sự kiện an toàn thông tin được sinh ra từ các thành phần trong hạ tầng công nghệ thông tin của cơ quan, tổ chức.

- Quản trị tập trung Log có thể thực hiện được các nhiệm vụ sau:

+ Phát hiện kịp thời các tấn công mạng xuất phát từ Internet cũng như các tấn công xuất phát trong nội bộ.
+ Phát hiện kịp thời các điểm yếu, lỗ hổng bảo mật của các thiết bị, ứng dụng và dịch vụ trong hệ thống.
+ Phát hiện kịp thời sự lây nhiễm mã độc trong hệ thống mạng, các máy tính bị nhiễm mã độc, các máy tính bị tình nghi là thành viên của mạng máy tính (botnet).
+ Giám sát việc tuân thủ chính sách an ninh trong hệ thống
+ Cung cấp bằng chứng số phục vụ công tác điều tra sau sự cố

- Tóm lại, việc xây dựng một giải pháp quản lý tập trung Log hợp lý sẽ giúp cải thiện hiệu quả cho hệ thống giám sát an ninh trong việc phân tích và xử lý các biến cố. Các phân tích viên sẽ tốn ít thời gian cho việc đánh giá chính xác được các biến cố nếu khả năng tự động của hệ thống gặp trục trặc.

- Một giải pháp tốt sẽ cho phép tất cả các biến cố an ninh quan trọng được thu thập và lưu trữ vào cơ sở dữ liệu nhằm cung cấp thông tin cho các phân tích viên an ninh, các đội ứng phó sự cố, và các bộ phận khác của tổ chức.

**Khái quát về hệ thống thu thập Log tập trung ELK**

- Elastic Stack (ELK Stack) - là một nhóm phần mềm nguồn mở, dựa trên Elastic nó cho phép tìm kiếm, phân tích, thể hiện trực quan các log thu thập được từ các nguồn, các log này là bất kỳ định dạng nào, ELK là trung tâm phân tích log. Trung tâm log này hữu ích khi trợ giúp xác định các vấn đề phát sinh trên các server, các ứng dụng mà bạn không cần truy cập trực tiếp vào log của từng server, từng ứng dụng. Thường để xây dựng nên trung tâm này dùng đến ELK với các thành phần chính gồm:

![image](https://user-images.githubusercontent.com/62273292/164177173-e83bda7d-3a33-47e8-afcb-6eedbfe6256e.png)


+ Elasticsearch - máy chủ lưu trữ và tìm kiếm dữ liệu

+ Logstash - thành phần xử lý dữ liệu, sau đó nó gửi dữ liệu nhận được cho Elasticsearch để lưu trữ

+ Kibana - ứng dụng nền web để tìm kiếm và xem trực quan các logs

+ Beats - gửi dữ liệu thu thập từ log của máy đến Logstash

**Cơ chế hoạt động của ELK Stack**

![image](https://user-images.githubusercontent.com/62273292/164177235-650a06e7-56fd-4c63-a7fd-a25a7b0fe791.png)

-Đầu tiên, log sẽ được đưa đến Logstash. (Thông qua nhiều con đường, ví dụ như server gửi UDP request chứa log tới URL của Logstash, hoặc Beat đọc file log và gửi lên Logstash)

-Logstash sẽ đọc những log này, thêm những thông tin như thời gian, IP, parse dữ liệu từ log (server nào, độ nghiêm trọng, nội dung log) ra, sau đó ghi xuống database là Elasticsearch.

-Khi muốn xem log, người dùng vào URL của Kibana. Kibana sẽ đọc thông tin log trong Elasticsearch, hiển thị lên giao diện cho người dùng query và xử lý.

**Hướng dẫn triển khai hệ thống ELK cơ bản**

Cần những tài nguyên gì để triển khai hệ thống ELK ?

- Đây là một trong những câu hỏi mà một quản trị hệ thống cần quan tâm. Một trong những ưu điểm của ELK là các bạn có thể bắt đầu rất nhỏ, chỉ với một server (physical hoặc virtual), và có thể mở rộng tùy theo nhu cầu (scale up và scale out). Tuy nhiên, vì đây là phần mềm miễn phí (về cơ bản) và bản chất của Elasticsearch là search engine, không phải là SIEM, nên để xây dựng được hệ thống theo dõi log cho Production thì người quản trị cần phải đầu tư thời gian (đồng nghĩa với tiền bạc).

- Nhân lực: thường thì chỉ cần 1 người là gánh đủ ELK. Ban đầu thì sẽ mất thời gian tìm hiểu để triển khai và tinh chỉnh, sau khi ổn định thì chỉ cần phân tích thông tin và xử lý.

- Tài nguyên hệ thống: ở mức nhở nhất, các bạn có thể bắt đầu triển khai ELK chỉ với 1 server gồm từ 2–4 CPU, 8 GB RAM, 30 GB free HDD. Yêu cầu tài nguyên tỷ lệ với nhiều yếu tố như sau:

- Lưu lượng log được thu thập

+ Yêu cầu về tốc độ truy xuất dữ liệu từ Elasticsearch

+ Yêu cầu về mức độ tìm kiếm (keyword vs. full text search vs. custom full text search)

+Yêu cầu về redundancy (number of replicas)

- Nhìn chung là không có công thức nào để tính trước về mặt tài nguyên. Mỗi nhu cầu sử dụng sẽ yêu cầu tài nguyên khác nhau.

**Mô hình hệ thống theo dõi Log**

- Cơ bản nhất là dùng beats thu thập log từ máy tính và gửi thẳng về Logstash để xử lý. Ngoài ra , nếu sử dụng nxlog bản Enterprise có thể gửi thẳng log vào ES (chắc có thể dùng Ingest pipeline để xử lý), tuy nhiên thường thì chúng ta dùng Logstash để normalize và enrich log events.

- Với hệ thống có nhiều lớp mạng riêng biệt, nếu để beats gửi log trực tiếp đến Logstash thì ta phải tạo firewall access rule cho tất cả máy tính đến Logstash TCP port. Chúng ta có thể tránh điều này bằng cách thêm vào một nxlog tập trung ở mỗi lớp mạng.

- Trên mỗi nxlog tập trung mình có thể sử dụng disk buffer để queue log trong trường hợp nxlog không kết nối được với Logstash.






















