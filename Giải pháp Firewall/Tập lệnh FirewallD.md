# Một vài lệnh cơ bản của FirewallD:

`systemctl start firewalld        # to start the FirewallD service on the system`

`systemctl restart firewalld      # For restarting the service`

`systemctl enable firewalld       #to enable it at boot level, thus it automatically start when a system booted up.`

`systemctl stop firewalld`         # Stop the service`

`systemctl disable firewalld      #vô hiệu hóa firewall`

`firewall-cmd --state             #View the running status`

`firewall-cmd --zone=public --list-ports    #View open port`

## Các lệnh để mở cổng hàng ngày của trang web trên CentOS Linux

```
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

**Mở cổng UDP**

Cũng giống như các cổng TCP, chúng ta có thể mở cổng UDP để truy cập công khai bằng lệnh dưới đây:

`firewall-cmd –zone = public –add-port = 443 / udp –permosystem`

![image](https://user-images.githubusercontent.com/62273292/166889031-5166e080-d414-43d8-8d2e-b75c1f717db5.png)

Configuration file:

`/usr/lib/firewalld ` Lưu cấu hình mặc định để tránh sửa đổi chúng.

`/etc/firewalld ` Lưu tệp cấu hình hệ thống, bạn sẽ ghi đè cấu hình mặc định.

`/usr/lib/firewalld/zone/` -Firewalld cung cấp các tệp cấu hình chín vùng theo mặc định: block.xml, dmz.xml, drop.xml, external.xml, home.xml, internal.xml, public.xml, trust.xml, work.xml

Few other commands to play around this Linux Firewall.

`firewall-cmd –help ` Hiển thị tất cả các lệnh tường lửa có sẵn

`firewall-cmd –version`

`firewall-cmd –state`

`firewall-cmd –get-active-zones` Xem khu vực được sử dụng bởi giao diện mạng.

`firewall-cmd –zone=public –list-all` Hiển thị tất cả các cấu hình trong khu vực được chỉ định.

`firewall-cmd –list-all-zones` Liệt kê tất cả các cấu hình vùng

`firewall-cmd –get-default-zone` Xem khu vực mặc định

`firewall-cmd –set-default-zone=internal` Đặt vùng mặc định

`firewall-cmd –get-zone-of-interface=eth0` Xem khu vực mà giao diện được chỉ định thuộc về.

`firewall-cmd –zone=public –add-interface=eth0` Thêm giao diện vào vùng, tất cả các giao diện mặc định đều là công khai, có giá trị vĩnh viễn cộng thêm –permanent sau đó reload


## Need to có giá trị vĩnh viễn, thêm –permanent

`firewall-cmd –panic-on|off   ` reject | mở tất cả các gói

`firewall-cmd –query-panic ` Xem có từ chối không

`firewall-cmd –reload ` Cập nhật các quy tắc tường lửa mà không cần ngắt kết nối

`firewall-cmd –complete-reload` tương tự để khởi động lại các quy tắc cập nhật

`firewall-cmd –zone=dmz –list-ports` Xem tất cả các cổng đang mở

`firewall-cmd –zone=dmz –add-port=8080/tcp `  Thêm một cổng vào khu vực

`Firewall-cmd –get-services` Xem các dịch vụ có sẵn mặc định

`Firewall-cmd –zone=zone –(add|remove)-service=http –permanent` Bật hoặc tắt vĩnh viễn dịch vụ HTTP

`Firewall-cmd –zone=public –add-port=123456/tcp –permanent`  Thêm lưu lượng TCP cho cổng 123456

`Firewall-cmd –zone=public –add-forward-port=port=80:proto=tcp:toport=123456` Lưu lượng đi từ cổng 80 đến cổng 123456
















