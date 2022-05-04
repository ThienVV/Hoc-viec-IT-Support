  # HƯỚNG DẪN CÀI ĐẶT FIREWALLD CHO CLOUD SERVER CHẠY TRÊN CENTOS 7
  
  ## FirewallD là gì?
  
  FirewallD hay tường lửa động thay thế Iptables. Là giao diện người dùng của Fedora 18 trong RHEL được cài đặt mặc định trên RHEL 7 và CentOS 7.

Với FirewallD, quản trị viên hệ thống Linux Cloud Server có thể cho phép thay đổi cấu hình mà không làm các kết nối hiện tại bị gián đoạn. FirewallD cung cấp giao diện cho các dịch vụ hoặc ứng dụng để trực tiếp thêm quy tắc tường lửa. Nó cũng kết nối với mã hạt nhân của bộ lọc mạng và hỗ trợ giao thức IPv4 và IPv6.

FirewallD động cung cấp thông tin về các cài đặt tường lửa hoạt động hiện tại với D-BUS. Đây là một hệ thống BUS tin nhắn cho phép giao tiếp giữa các quá trình dễ dàng, cũng như các vùng. Giao diện D-BUS cho phép daemon FirewallD giao tiếp với các quy trình và cho phép các ứng dụng, trình nền và quản trị viên bật hoặc tắt tính năng FirewallD. Ví dụ như mở cổng, chuyển tiếp cổng hoặc gói và thực hiện các tác vụ nâng cao hơn. Trong bài viết dưới đây, ODS sẽ hướng dẫn bạn cách cài đặt tường lửa FirewallD trên Cloud Server sử dụng hệ điều hành CentOS 7.

**Zone**

Trong FirewallD, Zone là một nhóm các quy tắc nhằm xác định các luồng dữ liệu được cho phép. Dựa trên mức độ tin tưởng của điểm xuất phát luồng dữ liệu đó trong hệ thống mạng.

Trong quá trình sử dụng, bạn có thể chọn Zone mặc định, thiết lập các quy tắc trong Zone hoặc chỉ định giao diện mạng (Network Interface) để xác định hành vi được phép.

Các Zone được xác định trước theo mức độ tin cậy, từ thấp đến cao như sau:

Drop: Mức tin cậy thấp nhất – toàn bộ các kết nối đến sẽ bị từ chối mà không phản hồi, chỉ cho phép duy nhất kết nối đi ra.
Block: Gần giống với Drop nhưng các kết nối đến bị từ chối và phản hồi bằng tin nhắn từ icmp-host-prohibited (hoặc icmp6-adm-prohibited).
Public: Đại diện cho mạng công cộng, không đáng tin cậy. Các máy tính/Services khác không được tin tưởng trong hệ thống nhưng vẫn cho phép các kết nối đến trên cơ sở chọn từng trường hợp cụ thể.
External: Hệ thống mạng bên ngoài trong trường hợp bạn sử dụng tường lửa làm Gateway, được cấu hình giả lập NAT để giữ bảo mật mạng nội bộ mà vẫn có thể truy cập.
Internal: Được sử dụng cho phần nội bộ của Gateway. Các máy tính/Services thuộc Zone này thì khá đáng tin cậy.
Dmz: sử dụng cho các máy tính/service trong khu vực DMZ(Demilitarized) – cách ly không cho phép truy cập vào phần còn lại của hệ thống mạng, chỉ cho phép một số kết nối đến nhất định.
Work: sử dụng trong công việc, tin tưởng hầu hết các máy tính và một vài services được cho phép hoạt động.
Home: môi trường gia đình – tin tưởng hầu hết các máy tính khác và thêm một vài services được cho phép hoạt động.
Trusted: đáng tin cậy nhất – tin tưởng toàn bộ thiết bị trong hệ thống.
Trong FirewallD, các quy tắc được cấu hình thời gian hiệu lực Runtime hoặc Permanent.

Runtime (mặc định): Có hiệu quả ngay lập tức, mất hiệu lực khi Reboot lại hệ thống.
Permanent: Không thể sử dụng cho hệ thống đang chạy. Bạn cần Reload mới có hiệu lực, tác dụng vĩnh viễn cả khi Reboot hệ thống.
Việc Restart/Reload sẽ hủy bộ các thiết lập Runtime. Đồng thời áp dụng thiết lập Permanent mà không làm phá vỡ các kết nối và Session hiện tại. Điều này giúp kiểm tra hoạt động của các quy tắc trên tường lửa và dễ dàng khởi động lại nếu có vấn đề xảy ra.

## Hiệu lực của các quy tắc Runtime/Permanent

Runtime(mặc định): có tác dụng ngay lập tức, mất hiệu lực khi reboot hệ thống.

Permanent: không áp dụng cho hệ thống đang chạy, cần reload mới có hiệu lực, tác dụng vĩnh viễn cả khi reboot hệ thống.

# Cài đặt tường lửa FirewallD

FirewallD được cài đặt mặc định

`yum install firewalld`

![image](https://user-images.githubusercontent.com/62273292/166642228-ebecbf5b-4aff-4790-80b3-9b7bd5d7a246.png)


Khởi động FirewallD:

`systemctl start firewalld`

Kiểm tra tình trạng hoạt động

```
systemctl status firewalld
```

![image](https://user-images.githubusercontent.com/62273292/166642427-1c4cd363-4ffa-4ff0-8efc-55a43cf56f21.png)


```
systemctl is-active firewalld
active
```

```
firewall-cmd --state
running
```

Thiết lập FirewallD khởi động cùng hệ thống

`systemctl enable firewalld`

Kiểm tra lại :

```
systemctl is-enabled firewalld
enabled
```

![image](https://user-images.githubusercontent.com/62273292/166643454-bfc4b7fd-3182-43f0-95de-9711083c4ae1.png)


Ban đầu, bạn không nên cho phép FirewallD khởi động cùng hệ thống cũng như thiết lập Permanent, tránh bị khóa khỏi hệ thống nếu thiết lập sai. Chỉ thiết lập như vậy khi bạn đã hoàn thành các quy tắc tường lửa cũng như test cẩn thận.

Khởi động lại

```
# systemctl restart firewalld
# firewall-cmd --reload
```

Dừng và vô hiệu hóa FirewallD

```
# systemctl stop firewalld
# systemctl disable firewalld
```

## Cấu hình FirewallD


**Thiết lập các Zone**

Liệt kê tất cả các zone trong hệ thống

`firewall-cmd --get-zones`

Kiểm tra zone mặc định

`firewall-cmd --get-default-zone`

Kiểm tra zone active (được sử dụng bởi giao diện mạng)

Vì FirewallD chưa được thiết lập bất kỳ quy tắc nào nên zone mặc định cũng đồng thời là zone duy nhất được kích hoạt, điều khiển mọi luồng dữ liệu.


`firewall-cmd --get-active-zones`

Hướng dẫn sử dụng duy nhất public zone – cho phép những services/port được thiết lập và từ chối mọi thứ khác

Thay đổi zone mặc định, ví dụ thành **home**:

`firewall-cmd --set-default-zone=home`


![image](https://user-images.githubusercontent.com/62273292/166643906-1b756fa9-df9f-4447-88c2-e00cbe965004.png)

**Thiết lập các quy tắc**

Trước khi thiết lập các quy tắc mới, hãy cùng HocVPS kiểm tra các quy tắc hiện tại:

– Liệt kê toàn bộ các quy tắc của các zones:

`firewall-cmd --list-all-zones`

- Liệt kê toàn bộ các quy tắc trong zone mặc định và zone active

`firewall-cmd --list-all`

Kết quả cho thấy public là zone mặc định đang được kích hoạt, liên kết với card mạng eth0 và cho phép DHCP cùng SSH.

– Liệt kê toàn bộ các quy tắc trong một zone cụ thể, ví dụ home

`firewall-cmd --zone=home --list-all`

– Liệt kê danh sách services/port được cho phép trong zone cụ thể:

```
# firewall-cmd --zone=public --list-services
# firewall-cmd --zone=public --list-ports
```

a. Thiết lập cho Service
Đây chính là điểm khác biệt của FirewallD so với Iptables – quản lý thông qua các services. Việc thiết lập tường lửa đã trở nên dễ dàng hơn bao giờ hết – chỉ việc thêm các services vào zone đang sử dụng.
– Đầu tiên, xác định các services trên hệ thống:

`firewall-cmd --get-services`

Hệ thống thông thường cần cho phép các services sau: ssh(22/TCP), http(80/TCP), https(443/TCP), smtp(25/TCP), smtps(465/TCP) và smtp-submission(587/TCP)

– Thiết lập cho phép services trên FirewallD, sử dụng --add-service

`# firewall-cmd --zone=public --add-service=http`

`# firewall-cmd --zone=public --add-service=http --permanent`

Ngay lập tức, zone “public” cho phép kết nối HTTP trên cổng 80. Kiểm tra lại

`firewall-cmd --zone=public --list-services`

– Vô hiệu hóa services trên FirewallD, sử dụng --remove-service:

```
# firewall-cmd --zone=public --remove-service=http
# firewall-cmd --zone=public --remove-service=http --permanent
```

b. Thiết lập cho Port
Trong trường hợp bạn thích quản lý theo cách truyền thống qua Port, FirewallD cũng hỗ trợ bạn điều đó.
– Mở Port với tham số --add-port:

```
# firewall-cmd --zone=public --add-port=9999/tcp
# firewall-cmd --zone=public --add-port=9999/tcp --permanent
```

Mở 1 dải port

```
# firewall-cmd --zone=public --add-port=4990-5000/tcp
# firewall-cmd --zone=public --add-port=4990-5000/tcp --permanent

```

Kiểm tra lại

```
# firewall-cmd --zone=public --list-ports
9999/tcp 4990-5000/tcp
```

– Đóng Port với tham số --remove-port:

```
firewall-cmd --zone=public --remove-port=9999/tcp
firewall-cmd --zone=public --remove-port=9999/tcp --permanent

```

## Cấu hình nâng cao














































