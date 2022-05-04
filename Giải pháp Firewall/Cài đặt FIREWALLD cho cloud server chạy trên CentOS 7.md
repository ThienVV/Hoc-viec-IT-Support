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

![image](https://user-images.githubusercontent.com/62273292/166646129-2dd8354e-a36a-4f3d-b49f-c7f17aa96fcb.png)


- Liệt kê toàn bộ các quy tắc trong zone mặc định và zone active

`firewall-cmd --list-all`

![image](https://user-images.githubusercontent.com/62273292/166646210-b8f2208e-9b4c-40a2-a829-5820e107cd83.png)


Kết quả cho thấy public là zone mặc định đang được kích hoạt, liên kết với card mạng ens33 và cho phép DHCP cùng SSH.

– Liệt kê toàn bộ các quy tắc trong một zone cụ thể, ví dụ home

`firewall-cmd --zone=home --list-all` 

![image](https://user-images.githubusercontent.com/62273292/166647621-ced3d862-aab2-4c4e-bf06-20cf609ba47c.png)


– Liệt kê danh sách services/port được cho phép trong zone cụ thể:

```
# firewall-cmd --zone=public --list-services
# firewall-cmd --zone=public --list-ports
```
![image](https://user-images.githubusercontent.com/62273292/166647747-4e4bc669-e78f-4092-8b3b-1e6b0c3dd6b2.png)


a. Thiết lập cho Service

Đây chính là điểm khác biệt của FirewallD so với Iptables – quản lý thông qua các services. Việc thiết lập tường lửa đã trở nên dễ dàng hơn bao giờ hết – chỉ việc thêm các services vào zone đang sử dụng.

– Đầu tiên, xác định các services trên hệ thống:

`firewall-cmd --get-services`

![image](https://user-images.githubusercontent.com/62273292/166647829-eb61dd8f-de31-41d6-bff0-6e4cd5f95142.png)


Hệ thống thông thường cần cho phép các services sau: ssh(22/TCP), http(80/TCP), https(443/TCP), smtp(25/TCP), smtps(465/TCP) và smtp-submission(587/TCP)

– Thiết lập cho phép services trên FirewallD, sử dụng --add-service

`# firewall-cmd --zone=public --add-service=http`

`# firewall-cmd --zone=public --add-service=http --permanent`

![image](https://user-images.githubusercontent.com/62273292/166647908-1f50484e-70cf-4a09-8e6c-205732bf7251.png)


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
![image](https://user-images.githubusercontent.com/62273292/166648070-190fbf8d-859b-4852-b8f9-0c83422ed11d.png)


Mở 1 dải port

```
# firewall-cmd --zone=public --add-port=4990-5000/tcp
# firewall-cmd --zone=public --add-port=4990-5000/tcp --permanent

```
![image](https://user-images.githubusercontent.com/62273292/166648156-a39802e2-5755-4a2c-95c4-4eb9a2641e96.png)



Kiểm tra lại

```
# firewall-cmd --zone=public --list-ports
9999/tcp 4990-5000/tcp
```
![image](https://user-images.githubusercontent.com/62273292/166648204-1cffffe8-b98c-4dd4-a942-21102ddaf161.png)



– Đóng Port với tham số --remove-port:

```
firewall-cmd --zone=public --remove-port=9999/tcp
firewall-cmd --zone=public --remove-port=9999/tcp --permanent

```

## Cấu hình nâng cao

1. Tạo Zone riêng

Mặc dù, các zone có sẵn là quá đủ với nhu cầu sử dụng, bạn vẫn có thể tạo lập zone của riêng mình để mô tả rõ ràng hơn về các chức năng của chúng. Ví dụ, bạn có thể tạo riêng một zone cho webserver publicweb hay một zone cấu hình riêng cho DNS trong mạng nội bộ privateDNS. Bạn cần thiết lập Permanent khi thêm một zone.

```
# firewall-cmd --permanent --new-zone=publicweb
success
# firewall-cmd --permanent --new-zone=privateDNS
success
# firewall-cmd --reload
success
```

![image](https://user-images.githubusercontent.com/62273292/166648680-78764442-c35a-478a-b786-53710ff0dd8a.png)


Kiểm tra lại

```
# firewall-cmd --get-zones
block dmz drop external home internal privateDNS public publicweb trusted work
```

Khi đã có zone thiết lập riêng, bạn có thể cấu hình như các zone thông thường: thiết lập mặc định, thêm quy tắc… Ví dụ:

```
# firewall-cmd --zone=publicweb --add-service=ssh --permanent
# firewall-cmd --zone=publicweb --add-service=http --permanent
# firewall-cmd --zone=publicweb --add-service=https --permanent
```
2. Định nghĩa services riêng trên FirewallD

Việc mở port trên tường lửa rất dễ dàng nhưng lại khiến bạn gặp khó khăn khi ghi nhớ các port và các services tương ứng. Vì vậy, khi có một services mới thêm vào hệ thống, bạn sẽ có 2 phương án:

Mở Port của services đó trên FirewallD

Tự định nghĩa services đó trên FirewallD

Ví dụ, HocVPS Admin Port có thể là 2017, 9999 hay 4 chữ số bất kì nào đó. Bạn sẽ tự định nghĩa servies hocvps-admin với port 9999.

– Tạo file định nghĩa riêng từ file chuẩn ban đầu

`# cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/hocvps-admin.xml`

– Chỉnh sửa để định nghĩa servies trên FirewallD

`# nano /etc/firewalld/services/hocvps-admin.xml`

```
<?xml version="1.0" encoding="utf-8"?>
<service>
<short>HocVPS-Admin</short>
<description>Control HocVPS Admin Web Tool</description>
<port protocol="tcp" port="9999"/>
</service>
```

– Lưu lại và khởi động lại FirewallD

![image](https://user-images.githubusercontent.com/62273292/166649235-7dacc99c-289e-47b5-ab45-49c63df6a287.png)


`# firewall-cmd --reload`

– Kiểm tra lại danh sách services:

![image](https://user-images.githubusercontent.com/62273292/166649314-76a3b667-4e47-4c12-9e85-fb4411fb8aa4.png)

`# firewall-cmd --get-services`

![image](https://user-images.githubusercontent.com/62273292/166649716-5b12d711-2282-43e9-9294-6c2a68a1d29a.png)


Như vậy, hocvps-admin đã được thêm vào danh sách services của FirewallD. Bạn có thể thiết lập như các servies thông thường, bao gồm cả cho phép/chặn trong zone. Ví dụ:

```
# firewall-cmd --zone=public --add-service=hocvps-admin
# firewall-cmd --zone=public --add-service=hocvps-admin --permanent
```

![image](https://user-images.githubusercontent.com/62273292/166649875-39f85e09-b536-456e-b99e-5bbf3ce6d535.png)






Nguồn tham khảo

https://cloud.z.com/vn/support/cloud/thiet-lap-tuong-lua-firewalld-tren-centos-7/


































