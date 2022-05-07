Để VPS của bạn hoạt động hiệu quả và bảo mật, bạn cần thường xuyên kiểm tra các dấu vết truy cập trái phép. Như thế, một tường lửa là giải pháp ban đầu mà bạn nên nghĩ đến. APF Firewall là một tường lửa có khả năng chặn khá tốt (ở mức cơ bản) những kết nối không mong muốn.

Để cài đặt VPS, bạn truy cập vào VPS của bạn sử dụng kết nối SSH (xài Putty).


`# cd /root/ `| Truy cập vào thư mục gốc
`# wget http://www.rfxnetworks.com/downloads/apf-current.tar.gz`

`# tar -xvzf apf-current.tar.gz `| Giải nén file nào!!!!

![image](https://user-images.githubusercontent.com/62273292/167247069-8b23386f-9a09-42f2-b7d4-d6541d7be90e.png)


Bạn sẽ thấy một danh sách thư mục. Hãy truy cập vào thư mục vừa giải nén sử dụng lệnh:

`# cd /tên thư mục/` | Chuyển con trỏ tới thư mục bạn muốn cài đặt

`# ./install.sh `| Chạy file cài đặt

![image](https://user-images.githubusercontent.com/62273292/167247086-f77d8364-08cd-42f2-8536-76130024d218.png)


Nếu cài đặt thành công, bạn sẽ thấy thông báo:

Installing APF 0.9.5-1: Completed.

Installation Details:
Install path: /etc/apf/
Config path: /etc/apf/conf.apf
Executable path: /usr/local/sbin/apf
AntiDos install path: /etc/apf/ad/
AntiDos config path: /etc/apf/ad/conf.antidos
DShield Client Parser: /etc/apf/extras/dshield/

Other Details:
Listening TCP ports: 1,21,22,25,53,80,110,111,143,443,465,993,995,2082, 2083,2086,2087,2095,2096,3306
Listening UDP ports: 53,55880
Note: These ports are not auto-configured; they are simply presented for information purposes. You must manually configure all port options.


Cuối cùng, hãy lưu file vào. Bây giờ, bạn phải khởi động APF Firewall nhé:

`# apf -s `| Command khởi động APF Firewall

![image](https://user-images.githubusercontent.com/62273292/167247960-12cc9e15-18cb-408b-b234-8121f8c8e515.png)

Hãy kiểm tra. Website của bạn có thể bị block trong vài phút ở cổng 80. Đừng lo lắng, hãy cứ kiểm tra. Với chế độ ban đầu, tường lửa sẽ thường xuyên update tròng vòng 5 phút/lần.

Bây giờ, bạn cần phải thay đổi chế độ chạy thử về chế độ chạy chính thức.

`# vi /etc/apf/conf.apf` | Dùng trình soạn thảo VI để sửa file conf.apf
Tìm mục
DEVEL_MODE=”1″
sửa thành
DEVEL_MODE=”0″

Đổi thành 

`IFACE_UNTRUSTED="ens33"`


![image](https://user-images.githubusercontent.com/62273292/167247732-a3da84fe-57e4-477f-94e6-b34010d19712.png)


![image](https://user-images.githubusercontent.com/62273292/167247279-97d2cf33-79a1-459e-bf80-8f217d1a2ae8.png)


Cuối cùng, phải khởi động lại APF Firewall

`# apf -r` | Command khởi động lại APF Firewall

![image](https://user-images.githubusercontent.com/62273292/167247675-3334e0f7-3e84-4047-ac6a-90d1f5cb38ea.png)


Như vậy, VPS của bạn có một bức tường lửa giúp chặn những truy cập không mong muốn. Trong bài sau, YêuHost sẽ giới thiệu chi tiết hơn về cách ngăn chặn DDOS và cấu hình APF Firewall chi tiết hơn.

Một số command dành cho APF Firewall

```
# apf -s | Khởi động APF Firewall
# apf -r | Update và khởi động lại APF Firewall
# apf -f | Dọn sạch tường lửa
# apf -st | Trạng thái hiện tại của APF Firewall
```
![image](https://user-images.githubusercontent.com/62273292/167247687-d10c081d-07b1-446b-93a0-8a91cff6e70b.png)


`# apf -a IP {Lý do mở}` | Cho phép một IP nào đó vượt qua tường lửa và điền vào nhóm “Cho phép truy cập” (allow_hosts.rules)

![image](https://user-images.githubusercontent.com/62273292/167247802-3fbc63f0-cdc4-4f3f-85a8-863444eb2900.png)

`# apf -d IP {Lý do khóa}` | Khóa một IP nào đó và xếp vào nhóm “Chặn truy cập” (deny_hosts.rules)

![image](https://user-images.githubusercontent.com/62273292/167247826-1d0fe1e5-245c-4528-a728-09f723b672eb.png)


`# chkconfig –level 2345 apf on` | Thêm APF Firewall vào danh sách tự động chạy khi khởi động lại VPS

`# chkconfig –del apf `| Gỡ bỏ APF Firewall khỏi list chạy tự động sau khi khởi động lại VPS.

