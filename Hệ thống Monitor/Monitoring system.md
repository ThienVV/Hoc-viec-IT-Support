# Tại sao chúng ta cần Monitoring System?

Sự thành công của các sản phẩm IT có thể được đo bằng số lượng người dùng và sự hài lòng của họ khi sử dụng sản phẩm. Khi người dùng có những trải nghiệm tốt đối với sản phẩm, họ sẽ gắn bó lâu dài hơn với chúng ta và giới thiệu những người khác cùng trải nghiệm. Chính vì vậy, đối với các công ty IT thì nhiệm vụ hàng đầu là phải làm thỏa mãn người dùng.

Một trong những cách để thoả mãn người dùng là cung cấp một hệ thống có chất lượng đủ tốt và ổn định. Một website thường xuyên gặp vấn đề (người dùng không thể sử dụng tính năng mà họ muốn hoặc tốc độ xử lý của trang web cực kì chậm) có thể khiến người dùng mất kiên nhẫn và tìm kiếm các sản phẩm khác thay thế.

Các công ty cần có những phương pháp để đảm bảo sự tin cậy cho các sản phẩm mình cung cấp và một hệ thống monitoring được xem như là giải pháp hiệu quả cho vấn đề này. 

# Monitoring System là gì?

Monitoring là một hệ thống dùng để thu thập thông tin về phần cứng và phần mềm của một hệ thống IT. Hệ thống monitoring có thể thu thập từ trạng thái của của server (CPU, memory, network, …) cho đến những thông tin chi tiết về cách server xử lý request đến từ người dùng (số lượng requests/s, thời gian server xử lý requests, …).

Một hệ thống monitoring sẽ giúp chúng ta có một cái nhìn dễ dàng về chất lượng và những vấn đề xảy ra với sản phẩm. Nó sẽ tự động cảnh báo cho chúng ta ngay khi phát hiện ra điều bất thường. Bây giờ, thay vì được người dùng thông báo rằng server gặp trục trặc, chúng ta sẽ sớm phát hiện và giải quyết trước khi người dùng nhận ra. Hơn nữa, đối với các hệ thống đủ lớn và phức tạp, hệ thống monitoring còn giúp chúng ta biết được những thành phần nào hay gặp sự cố để có thể tập trung cải thiện chất lượng.

# Service Level Objectives (SLOs) – Khái niệm quan trọng trong monitoring

Không hiểu rõ hệ thống IT hoặc những gì thực sự quan trọng đối với hệ thống khiến cho việc quản lý gặp nhiều khó khăn. Hãy thử tưởng tượng bạn là huấn luyện viên của một đội bóng, và bạn không hề biết mục tiêu của đội bóng là gì, trong đội bóng có bao nhiêu cầu thủ và năng lực của từng cầu thủ là thế nào. Đối với các đội bóng hàng đầu, họ không được phép thua bất cứ trận nào để dành chức vô địch. Nhưng đối với các đội bóng yếu và tầm trung, họ được phép thua nhiều trận, miễn sao có thể trụ hạng. Không hiểu rõ những vấn đề này khiến cho việc quản lý đội bóng gần như không tưởng và rất khó để đạt được mục tiêu của đội.

Tương tự đối với các hệ thống IT, người dùng luôn là mục tiêu cuối cùng của sản phẩm. Hiểu được những gì thực sự quan trọng đối với người dùng và xây dựng được các công thức tính toán các yếu tố này giúp chúng ta tập trung vào những thứ cần thiết và có được một cái nhìn chính xác về sự hiệu quả của sản phẩm. Từ đó, chúng ta có thể xây dựng một hệ thống monitoring hiệu quả để đảm bảo mục tiêu cụ thể mà chúng ta đề ra.

SLOs là một khái niệm được sinh ra bởi các kỹ sư SRE của Google để giúp hệ thống monitoring tập trung vào những thứ quan trọng đối với sản phẩm. SLOs miêu tả những mục tiêu của hệ thống, cùng với đó là các công thức để tính toán rằng chúng ta đang ở đâu so với mục tiêu, và chúng ta phải cải thiện những gì để đạt được mục tiêu. SLOs được đánh giá quan trọng đến mức nếu không có nó, chúng ta cũng không cần có hệ thống monitoring nào cả.

# Elastic Stack

Elastic stack là một tập hợp các công nghệ dùng để thu thập, biến đổi, lưu trữ và phân tích dữ liệu với thành phần chính là Elasticsearch.

![image](https://user-images.githubusercontent.com/62273292/165018183-85db7d34-e079-4145-8957-a88b685369b7.png)

Về khía cạnh monitoring, beats sẽ được sử dụng để thu thập thông tin của server. Hệ thống monitoring

- Metricbeat: Thu thập metrics về server (CPU, memory, …)
- Filebeat: Thu thập logs của các services.
- Heartbeat: Ping để kiểm tra xem các services có còn hoạt động không.

Logstash được sử dụng để biến đổi dữ liệu theo cách mà chúng ta mong muốn. Sau đó, tất cả dữ liệu sẽ được lưu trong Elasticsearch và được hiển thị qua dashboard trong Kibana.

**Monitoring System hoạt động thế nào?**

![image](https://user-images.githubusercontent.com/62273292/165018277-a0d7bfe0-e8f5-4250-8289-751b984b4f6e.png)

Metricbeat, Heartbeat và Filebeat sẽ thu thập các thông tin về hệ thống và gửi trực tiếp về Elasticsearch. Ở đây, chúng ta không dùng Logstash để biến đổi dữ liệu mà thay vào đó Ingest Node của Elasticsearch sẽ được sử dụng để giảm bớt đi một layer trong hệ thống, khiến hệ thống đơn giản hơn. Dữ liệu thu thập được từ hệ thống monitoring thường khá thường xuyên và lớn nên các kỹ sư ở Got It luôn phải có phương án kỹ lưỡng về thời gian lưu trữ chúng trên Elasticsearch cũng như backup thường xuyên để tránh mất dữ liệu.

Watcher là một tính năng được cung cấp bởi Elasticsearch giúp chúng ta phát hiện ra những sự cố xảy ra trong hệ thống một cách tự động. Sau mỗi khoảng thời gian nhất định, Watcher sẽ thực hiện một câu hỏi truy vấn vào Elasticsearch để lấy dữ liệu cần thiết. Sau đó, nó sẽ sử dụng dữ liệu để so sánh với những điều kiện chúng ta quy định và thông báo cho chúng ta biết ngay khi tìm thấy một điểm bất thường trong hệ thống. Dựa vào tính nghiêm trọng của sự cố, Watcher sẽ sử dụng chọn một (hoặc nhiều) phương pháp:

# Kết luận

Đối với các công ty lớn, hệ thống monitoring là công cụ không thể thiếu để đảm bảo chất lượng của sản phẩm cũng như trải nghiệm của người dùng. Bài viết này miêu tả một trong những hệ thống monitoring, các kỹ sư xây dựng và sử dụng thành công. Lưu ý rằng, ngoài hệ thống trên, các sản phẩm còn được giám sát cẩn thận bởi các monitoring system khác (mà không được nhắc đến trong bài viết này) vì có rất nhiều khía cạnh khác nhau của các hệ thống IT mà chúng ta cần bảo vệ.
























