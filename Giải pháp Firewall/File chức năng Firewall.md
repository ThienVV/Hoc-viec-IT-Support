# File có chức năng allow, deny, ignore(bypass) trong loại fw

Hành động quy tắc tường lửa

Các quy tắc tường lửa có thể thực hiện các hành động sau:

allow: Cho phép rõ ràng lưu lượng truy cập phù hợp với quy tắc đi qua, sau đó ngầm phủ nhận mọi thứ khác.

Bypass: Cho phép lưu lượng vượt qua cả tường lửa và phân tích ngăn chặn xâm nhập. Sử dụng cài đặt này cho các giao thức chuyên sâu về phương tiện hoặc cho lưu lượng truy cập bắt nguồn từ các nguồn đáng tin cậy. Quy tắc bỏ qua có thể dựa trên IP, cổng, hướng lưu lượng và giao thức.

Deny: Chặn rõ ràng lưu lượng truy cập phù hợp với quy tắc.

Force Allow: Buộc cho phép lưu lượng truy cập mà nếu không sẽ bị các quy tắc khác từ chối.
 lưu ý: Lưu lượng truy cập được cho phép bởi quy tắc Force Allow sẽ vẫn được phân tích bởi mô-đun phòng chống xâm nhập.

Log only: Lưu lượng truy cập sẽ chỉ được ghi lại. Không có hành động nào khác sẽ được thực hiện.

Tìm hiểu thêm về quy tắc Cho phép

Quy tắc cho phép có hai chức năng:

1. Cho phép lưu lượng truy cập được cho phép một cách rõ ràng.

2. Từ chối ngầm tất cả các lưu lượng truy cập khác.

lưu ý: Lưu lượng truy cập không được quy tắc Cho phép rõ ràng sẽ bị loại bỏ và được ghi lại dưới dạng sự kiện tường lửa 'Nằm ngoài "Chính sách" Được phép ".

Các quy tắc Cho phép thường được áp dụng bao gồm:

**ARP** : Cho phép lưu lượng truy cập Giao thức phân giải địa chỉ (ARP) đến.

**Cho phép trả lời TCP / UDP** được trưng cầu : Cho phép máy tính nhận câu trả lời cho các thông báo TCP và UDP của chính nó. Điều này hoạt động cùng với cấu hình trạng thái TCP và UDP.

**Cho phép trả lời ICMP** được trưng cầu : Cho phép máy tính nhận câu trả lời cho tin nhắn ICMP của chính nó. Điều này hoạt động cùng với cấu hình trạng thái ICMP.

Tìm hiểu thêm về quy tắc Bỏ qua

Quy tắc Bỏ qua được thiết kế cho các giao thức chuyên sâu về phương tiện hoặc cho lưu lượng truy cập bắt nguồn từ các nguồn đáng tin cậy mà việc lọc bằng tường lửa hoặc các mô-đun ngăn chặn xâm nhập là không bắt buộc hoặc không mong muốn.

Một gói phù hợp với các điều kiện của quy tắc Bỏ qua:

- Không phụ thuộc vào các điều kiện của cài đặt cấu hình trạng thái.

- Vượt qua cả tường lửa và phân tích ngăn chặn xâm nhập.

Vì không áp dụng chế độ kiểm tra trạng thái đối với giao thông được bỏ qua, nên việc bỏ qua giao thông ở một hướng không tự động bỏ qua phản ứng theo hướng khác. Các quy tắc bỏ qua phải luôn được tạo và áp dụng theo cặp, một quy tắc cho lưu lượng truy cập đến và một quy tắc khác cho lưu lượng đi.

lưu ý: Các sự kiện quy tắc bỏ qua không được ghi lại. Đây không phải là một hành vi có thể định cấu hình.

Lưu ý thêm: Nếu Trình quản lý bảo mật sâu sử dụng cơ sở dữ liệu từ xa được Bảo vệ bởi Tác nhân bảo mật sâu , các cảnh báo sai liên quan đến phòng chống xâm nhập có thể xảy ra khi Trình quản lý bảo mật sâu lưu các quy tắc ngăn chặn xâm nhập vào cơ sở dữ liệu. Bản thân nội dung của các quy tắc có thể bị xác định nhầm là một cuộc tấn công. Một trong những giải pháp thay thế cho điều này là tạo quy tắc bỏ qua cho lưu lượng truy cập từ Trình quản lý bảo mật sâu đến cơ sở dữ liệu.

Quy tắc bỏ qua mặc định cho lưu lượng truy cập Trình quản lý bảo mật sâu

Trình quản lý bảo mật sâu tự động triển khai quy tắc Bỏ qua 4 ưu tiên để mở lưu lượng TCP đến trên cổng lắng nghe của tác nhân cho nhịp tim(xem Định cấu hình nhịp tim )trên máy tính chạy Deep Security Agent. Mức độ ưu tiên 4 đảm bảo rằng quy tắc này được áp dụng trước bất kỳ quy tắc Từ chối nào và Bỏ qua đảm bảo rằng lưu lượng truy cập không bao giờ bị suy giảm. Quy tắc Bỏ qua không được hiển thị rõ ràng trong danh sách quy tắc tường lửa vì quy tắc được tạo nội bộ.

Tuy nhiên, quy tắc này chấp nhận lưu lượng truy cập từ bất kỳ địa chỉ IP và bất kỳ địa chỉ MAC nào. Để tăng cường bảo mật của tác nhân trên cổng này, bạn có thể tạo một quy tắc bỏ qua thay thế, hạn chế hơn cho cổng này. Tác nhân sẽ thực sự vô hiệu hóa quy tắc lưu lượng truy cập Trình quản lý bảo mật sâu mặc định để có lợi cho quy tắc tùy chỉnh mới miễn là nó có các đặc điểm sau:

**Mức độ ưu tiên:** 4 - Cao nhất

**Hướng gói**: Đang đến

**Loại khung**: IP

**Giao thức**: TCP

**Cổng đích gói:** số cổng lắng nghe của tác nhân đối với nhịp tim từ Người quản lý

Quy tắc tùy chỉnh phải sử dụng các thông số trên để thay thế quy tắc mặc định. Tốt nhất, địa chỉ IP hoặc địa chỉ MAC của Trình quản lý bảo mật sâu thực tế nên được sử dụng làm nguồn gói cho quy tắc.

Tìm hiểu thêm về quy tắc Buộc cho phép

Tùy chọn Buộc cho phép loại trừ một tập hợp phụ lưu lượng truy cập có thể đã bị che bởi hành động Từ chối. Mối quan hệ của nó với các hành động khác được minh họa bên dưới. Buộc cho phép có tác dụng tương tự như quy tắc Bỏ qua. Tuy nhiên, không giống như Bypass, lưu lượng vượt qua tường lửa vì hành động này vẫn phải chịu sự kiểm tra của mô-đun phòng chống xâm nhập. Hành động Force Allow đặc biệt hữu ích để đảm bảo rằng các dịch vụ mạng thiết yếu có thể giao tiếp với máy tính DSA. Nói chung, các quy tắc Buộc cho phép chỉ nên được sử dụng cùng với Cho phép và các quy tắc Cho phép một tập hợp con lưu lượng truy cập đã bị cấm bởi các quy tắc Cho phép và Từ chối. Các quy tắc Buộc cho phép cũng được yêu cầu để Cho phép lưu lượng ICMP và UDP không mong muốn khi ICMP và UDP ở trạng thái ở trạng thái được bật.

Lưu ý: Khi sử dụng nhiều Trình quản lý bảo mật sâu trong một sắp xếp nhiều nút, có thể hữu ích khi xác định danh sách IP cho các máy chủ này, sau đó tạo quy tắc lưu lượng Trình quản lý bảo mật sâu tùy chỉnh với danh sách đó.

Trình tự quy tắc tường lửa

Các gói tin đến một máy tính được xử lý trước tiên bởi các quy tắc tường lửa, sau đó là các điều kiện cấu hình trạng thái tường lửa và cuối cùng là các quy tắc ngăn chặn xâm nhập.

Đây là thứ tự áp dụng các quy tắc tường lửa (đến và đi):

1. Quy tắc tường lửa với mức độ ưu tiên 4 (cao nhất)

a,**Đường vòng**

b,**Chỉ nhật ký** (Quy tắc Chỉ nhật ký chỉ có thể được chỉ định mức độ ưu tiên là 4 (cao nhất) )

c,**Buộc cho phép**

d,**Phủ nhận**

2. Quy tắc tường lửa với mức độ ưu tiên 3 (cao)

a, **Đường vòng**

b, **Buộc cho phép**

c, **Phủ nhận**

3. Quy tắc tường lửa với mức độ ưu tiên 2 (bình thường)
a, **Đường vòng**

b, **Buộc cho phép**

c, **Phủ nhận**

4. Quy tắc tường lửa với mức độ ưu tiên 1 (thấp)
a, **Đường vòng**

b, **Buộc cho phép**

c, **Phủ nhận**

5. Quy tắc tường lửa với mức độ ưu tiên 0 (thấp nhất)

a, **Đường vòng**

b, **Buộc cho phép**

c, **Phủ nhận**

d, **Cho phép **(Lưu ý rằng quy tắc Cho phép chỉ có thể được chỉ định mức độ ưu tiên là 0 (thấp nhất) )

**Lưu ý:** Nếu bạn không có quy tắc Cho phép nào có hiệu lực trên máy tính, thì tất cả lưu lượng truy cập đều được phép trừ khi nó bị chặn cụ thể bởi quy tắc Từ chối. Sau khi bạn tạo một quy tắc Cho phép, tất cả lưu lượng truy cập khác sẽ bị chặn trừ khi nó đáp ứng các điều kiện của quy tắc Cho phép. Có một ngoại lệ cho điều này: lưu lượng ICMPv6 luôn được phép trừ khi nó bị chặn cụ thể bởi quy tắc Từ chối.

Trong cùng ngữ cảnh ưu tiên, quy tắc Từ chối sẽ ghi đè quy tắc Cho phép và quy tắc Buộc cho phép sẽ ghi đè quy tắc Từ chối. Bằng cách sử dụng hệ thống ưu tiên quy tắc, quy tắc Từ chối có mức ưu tiên cao hơn có thể được thực hiện để ghi đè quy tắc Buộc cho phép có mức ưu tiên thấp hơn.

Hãy xem xét ví dụ về chính sách máy chủ DNS sử dụng quy tắc Buộc cho phép để Cho phép tất cả các truy vấn DNS đến . Tạo quy tắc Từ chối có mức độ ưu tiên cao hơn quy tắc Buộc cho phép cho phép bạn chỉ định một dải địa chỉ IP cụ thể phải bị cấm truy cập vào cùng một máy chủ công cộng.

Bộ quy tắc dựa trên mức độ ưu tiên cho phép bạn đặt thứ tự áp dụng các quy tắc. Nếu quy tắc Từ chối được đặt với mức độ ưu tiên cao nhất và không có quy tắc Buộc cho phép có cùng mức độ ưu tiên, thì bất kỳ gói nào phù hợp với quy tắc Từ chối sẽ tự động bị loại bỏ và các quy tắc còn lại sẽ bị bỏ qua. Ngược lại, nếu tồn tại quy tắc Buộc cho phép với bộ cờ ưu tiên cao nhất, bất kỳ gói nào đến khớp với quy tắc Cho phép bắt buộc sẽ được tự động cho phép thông qua mà không bị kiểm tra so với bất kỳ quy tắc nào khác.

**Một lưu ý về ghi nhật ký**

Các quy tắc bỏ qua sẽ không bao giờ tạo ra một sự kiện. Điều này không thể cấu hình.

Quy tắc Chỉ ghi nhật ký sẽ chỉ tạo ra một sự kiện nếu gói được đề cập sau đó không bị dừng lại bởi một trong hai:

**quy tắc Từ chối hoặc**

**quy tắc Cho phép loại trừ nó.**

Nếu gói bị dừng bởi một trong hai quy tắc đó, các quy tắc đó sẽ tạo ra Sự kiện chứ không phải quy tắc Chỉ nhật ký. Nếu không có quy tắc nào tiếp theo dừng gói, quy tắc Chỉ ghi nhật ký sẽ tạo ra một sự kiện.

## Cách các quy tắc tường lửa hoạt động cùng nhau

Quy tắc tường lửa Bảo mật sâu có cả hành động quy tắc và ưu tiên quy tắc. Được sử dụng kết hợp, hai thuộc tính này cho phép bạn tạo các bộ quy tắc rất linh hoạt và mạnh mẽ. Không giống như các bộ quy tắc được sử dụng bởi các tường lửa khác, có thể yêu cầu các quy tắc phải được xác định theo thứ tự mà chúng sẽ được chạy, các quy tắc của Tường lửa Bảo mật Sâu được chạy theo thứ tự xác định dựa trên hành động của quy tắc và mức độ ưu tiên của quy tắc, độc lập thứ tự mà chúng được xác định hoặc gán.

**Hành động quy tắc**

Mỗi quy tắc có thể có một trong bốn hành động.

**Bỏ qua**: nếu một gói phù hợp với quy tắc Bỏ qua, nó sẽ được chuyển qua cả tường lửa và Công cụ ngăn chặn xâm nhập bất kể quy tắc nào khác (ở cùng mức độ ưu tiên).

**Chỉ ghi nhật ký**: nếu một gói phù hợp với quy tắc Chỉ ghi nhật ký thì nó được thông qua và sự kiện được ghi lại.

**Buộc cho phép**: nếu một gói phù hợp với quy tắc Buộc cho phép thì nó được thông qua bất kể quy tắc nào khác (ở cùng mức độ ưu tiên).

**Từ chối**: nếu một gói phù hợp với quy tắc Từ chối, nó sẽ bị loại bỏ.

**Cho phép**: nếu một gói phù hợp với quy tắc Cho phép, nó sẽ được chuyển. Mọi lưu lượng truy cập không phù hợp với một trong các quy tắc Cho phép đều bị từ chối.

Việc triển khai quy tắc Cho phép sẽ khiến tất cả lưu lượng truy cập khác không nằm trong quy tắc Cho phép bị từ chối:

Quy tắc Từ chối có thể được triển khai trên Cho phép chặn các loại lưu lượng cụ thể:

Quy tắc Buộc cho phép có thể được đặt trên lưu lượng bị từ chối để Cho phép một số trường hợp ngoại lệ đi qua:

Mức độ ưu tiên của quy tắc

Các hành động quy tắc thuộc loại Từ chối và Buộc cho phép có thể được xác định ở một trong 5 mức độ ưu tiên bất kỳ để cho phép tinh chỉnh thêm lưu lượng truy cập được phép được xác định bởi bộ quy tắc Cho phép. Các quy tắc được chạy theo thứ tự ưu tiên từ cao nhất (Mức độ ưu tiên 4) đến thấp nhất (Mức độ ưu tiên 0). Trong một mức độ ưu tiên cụ thể, các quy tắc được xử lý theo thứ tự dựa trên hành động của quy tắc (Buộc cho phép, Từ chối, Cho phép, chỉ ghi nhật ký).

Ngữ cảnh ưu tiên Cho phép Người dùng tinh chỉnh liên tiếp các điều khiển lưu lượng bằng cách sử dụng kết hợp quy tắc Từ chối và Buộc cho phép. Trong cùng ngữ cảnh ưu tiên, quy tắc Cho phép có thể bị phủ định bằng quy tắc Từ chối và quy tắc Từ chối có thể bị phủ định bởi quy tắc Buộc cho phép.

Lưu ý: Các hành động quy tắc thuộc loại Cho phép chỉ chạy ở mức độ ưu tiên 0 trong khi các hành động quy tắc thuộc loại Nhật ký Chỉ chạy ở mức độ ưu tiên 4.

## Đặt hành động quy tắc và mức độ ưu tiên cùng nhau

Các quy tắc được chạy theo thứ tự ưu tiên từ cao nhất (Mức độ ưu tiên 4) đến thấp nhất (Mức độ ưu tiên 0). Trong một mức độ ưu tiên cụ thể, các quy tắc được xử lý theo thứ tự dựa trên hành động quy tắc. Thứ tự xử lý các quy tắc có mức độ ưu tiên ngang nhau như sau:

Đường vòng

Chỉ đăng nhập

Buộc cho phép

Phủ nhận

Cho phép

lưu ý: Hãy nhớ rằng các hành động quy tắc thuộc loại Cho phép chỉ chạy ở mức ưu tiên 0 trong khi các hành động quy tắc thuộc loại Nhật ký Chỉ chạy ở mức ưu tiên 4.

Lưu ý: Điều quan trọng cần nhớ là nếu bạn có quy tắc Buộc cho phép và quy tắc Từ chối ở cùng mức độ ưu tiên, quy tắc Buộc cho phép sẽ được ưu tiên hơn quy tắc Từ chối và do đó lưu lượng truy cập phù hợp với quy tắc Buộc sẽ được phép.


# Tham số tường lửa

Các tham số này ảnh hưởng đến hoạt động của S-TAP đối với tường lửa.

Các tham số này được lưu trữ trong phần [TAP] của tệp thuộc tính S-TAP.

|GIM|Guard_tap.ini|Giá trị mặc định|Sự miêu tả|
|--------|-----------|--------------|----------------|
|WINSTAP_FIREWALL_INSTALLED|FIREWALL_INSTALLED|0|Đã bật tính năng tường lửa. Giá trị hợp lệ: 0 : bị vô hiệu hóa. 1 : đã bật.|
|WINSTAP_FIREWALL_TIMEOUT|FIREWALL_TIMEOUT|2|Thời gian, tính bằng giây, chờ phán quyết từ hệ thống Guardium®. Nếu tường lửa hết thời gian chờ, giá trị của tham số firewall_fail_close sẽ xác định xem có chặn hoặc cho phép kết nối hay không. Giá trị hợp lệ: bất kỳ số nguyên nào .|
|WINSTAP_FAIL_CLOSE|FIREWALL_FAIL_CLOSE|0|Giá trị hợp lệ: 0: Tường lửa được kích hoạt mỗi phiên khi được kích hoạt bởi một quy tắc trong chính sách đã cài đặt. 1: Tất cả lưu lượng truy cập được theo dõi để tìm vi phạm chính sách tường lửa|
|WINSTAP_DEFAULT_STATE|FIREWALL_DEFAULT_STATE	|0|Hành động khi phán quyết không thể được đặt theo quy tắc chính sách, ví dụ: firewall_timeout hết hạn. Giá trị hợp lệ: 0 : kết nối đi qua. 1 : kết nối bị chặn. 2: Tất cả lưu lượng được theo dõi để phát hiện vi phạm chính sách tường lửa đối với các gói tin priority_count ban đầu (tham số Guard_tap.ini ). S-TAP® xem phần đầu tiên của mỗi phiên mới vào DB của bạn. Điều này hữu ích khi bạn có các chính sách dựa trên phiên, quy tắc tường lửa dựa trên người dùng hoặc một số thông tin khác được thông qua sớm trong phiên. Nó hạn chế tác động của tường lửa đến hiệu suất. Thay vì xem từng bit của phiên ( firewall_default_state = 1) và chờ kết quả KHÔNG ĐỒNG Ý, S-TAP chỉ đơn giản là tự động mở nếu không có XEM hoặc DROP nào được gửi.|
|WINSTAP_FORCE_WATCH|FIREWALL_FORCE_WATCH|Vô giá trị|Khi firewall_default_state = 0 (tắt), thì firewall_force_watch chỉ định mạng / mặt nạ của các IP mà bạn muốn tường lửa theo dõi, ghi đè mặc định (tắt). Giá trị hợp lệ: danh sách các giá trị IP / mặt nạ được phân tách bằng dấu phẩy.|
|WINSTAP_FORCE_UNWATCH|FIREWALL_FORCE_UNWATCH|Vô giá trị|Khi firewall_default_state = 1 (bật), thì firewall_force_unwatch chỉ định mạng / mặt nạ của các IP mà bạn muốn tường lửa bỏ qua, ghi đè mặc định (bật). Giá trị hợp lệ: danh sách các giá trị IP / mặt nạ được phân tách bằng dấu phẩy.|





link tham khảo (các tính năng ): https://help.deepsecurity.trendmicro.com/10_3/aws/Protection-Modules/Firewall/firewall-rule-action-priority.html
link tham khảo (tham số tường lửa): https://www.ibm.com/docs/en/guardium/11.1?topic=parameters-firewall

















