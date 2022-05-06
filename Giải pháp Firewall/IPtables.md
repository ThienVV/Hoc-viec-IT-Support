# IPtables là gì?

IPtables là ứng dụng tường lửa miễn phí trong Linux, cho phép thiết lập các quy tắc riêng để kiểm soát truy cập, tăng tính bảo mật. Khi sử dụng máy chủ, tường lửa là một trong những công cụ quan trọng giúp bạn ngăn chặn các truy cập không hợp lệ. Đối với các bản phân phối Linux như Ubuntu, Fedora, CentOS… bạn có thể tìm thấy công cụ tường lửa tích hợp sẵn IPtables.

IPtables là một ứng dụng tường lửa có sẵn trên Linux, IPtables Linux firewall cho phép người dùng thiết lập các quyền truy cập để kiểm soát lưu lượng một cách chọn lọc trên máy chủ.

![image](https://user-images.githubusercontent.com/62273292/167060805-5383f22f-6d35-4944-a83a-bcadb7caec01.png)

## Các bảng trong IPtables là gì?

Table được IPtables sử dụng để định nghĩa các rules(quy tắc) dành cho các gói tin. Trong đó, có các Table sau. 

**Filter Table**

Là một trong những tables được IPtables sử dụng nhiều nhất, Filter Table sẽ quyết định việc một gói tin có được đi đến đích dự kiến hay từ chối yêu cầu của gói tin.

**NAT Table**

Để dùng các rules về NAT(Network Address Translation), NAT Table sẽ có trách nhiệm chỉnh sửa source(IP nguồn) hoặc destination(IP đích) của gói tin khi thực hiện cơ chế NAT.

**Mangle Table**

Cho phép chỉnh sửa header của gói tin, giá trị của các trường TTL, MTU, Type of Service.

**Raw Table**

IPtables là một stateful firewall với các gói tin được kiểm tra liên quan đến trạng thái(state). Ví dụ gói có thể là một phần của một kết nối mới hoặc là một phần của kết nối hiện có. Raw Table sẽ giúp bạn làm việc với các gói tin trước khi kernel bắt đầu kiểm tra trạng thái và có thể loại một số gói khỏi việc tracking vì vấn đề hiệu năng của hệ thống.

**Security Table**

Một vài kernel có thể hỗ trợ thêm Security Table, được dùng bởi SELinux để thiết lập các chính sách bảo mật.

### Chains
Chains được tạo ra với một số lượng nhất định ứng với mỗi Table, giúp lọc gói tin tại các điểm khác nhau.

**Chain PREROUTING** tồn tại trong Nat Table, Mangle Table và Raw Table, các rules trong chain sẽ được thực thi ngay khi gói tin vào đến giao diện mạng (Network Interface).

**Chain INPUT** chỉ có ở Mangle Table và Nat Table với các rules được thực thi ngay trước khi gói tin gặp tiến trình.

**Chain OUTPUT** tồn tại ở Raw Table, Mangle Table và Filter Table, có các rules được thực thi sau khi gói tin được tiến trình tạo ra.

**Chain FORWARD** tồn tại ở Manle Table và Filter Table, có các rules được thực thi cho các gói tin được định tuyến qua host hiện tại.

**Chain POSTROUTING** chỉ tồn tại ở Manle Table và Nat Table với các rules được thực thi khi gói tin rời giao diện mạng.


### Target

Target có thể được hiểu là hành động dành cho các gói tin khi gói tin thỏa mãn các rules đặt ra.

- ACCEPT: chấp nhận và cho phép gói tin đi vào hệ thống.

- DROP: loại gói tin, không có gói tin trả lời.

- REJECT: loại gói tin những có trả lời table gói tin khác. Ví dụ: trả lời table 1 gói tin “connection reset” đối với gói TCP hoặc “destination host unreachable” đối với gói UDP và ICMP.

- LOG: chấp nhận gói tin nhưng có ghi lại log.

- Gói tin sẽ được đi qua tất cả các rules đặt ra mà không dừng lại ở bất kì rule nào đúng. Trường hợp gói tin không khớp với rules nào mặc định sẽ được chấp nhận

## Cấu hình IPtables cơ bản là gì?

Một target (mục tiêu) sẽ được đưa ra khi có một gói tin được xác định. Target có thể là một chuỗi khác để khớp với một trong các giá trị sau:

**ACCEPT**: gói tin được phép đi qua.
**DROP:** gói tin không được phép đi qua.
**RETURN:** bỏ qua chuỗi hiện tại và quay trở lại quy tắc tiếp theo từ chuỗi mà nó được gọi.

## Các rules trong IPtables là gì?

![image](https://user-images.githubusercontent.com/62273292/167064937-fe4b89aa-7eae-4f53-b5b7-6eb1c82c4637.png)

Người dùng có thể dùng lệnh sau để xem các rules hiện có trong IPtables:

`IPtables -L –v`

![image](https://user-images.githubusercontent.com/62273292/167084837-4e4c9062-44cf-48df-b746-afca110290c4.png)


## Ý nghĩa của từng cột và hàng

**TARGET:** hành động sẽ thực thi.

**PROT:** viết tắt của Protocol, là các giao thức sẽ được áp dụng để thực thi quy tắc này. Ở đây chúng ta có 3 lựa chọn là all, tcp hoặc udp. Các ứng dụng như SSH, FTP, sFTP,..đều sử dụng giao thức TCP.

**IN:** chỉ ra rule sẽ áp dụng cho các gói tin đi vào từ interface nào, ví dụ lo, eth0, eth1 hoặc any là áp dụng cho tất cả interface.

**OUT:** tương tự  IN, chỉ ra rule sẽ áp dụng cho các gói tin đi ra từ interface nào.

**DESTINATION:** địa chỉ của lượt truy cập được phép áp dụng quy tắc. 

**ACCEPT    all —   lo any anywhere   anywhere:** chấp nhận toàn bộ gói tin từ interface lo (Loopback Interface), là interface ảo nội bộ, ví dụ IP 127.0.0.1 là kết nối qua thiết bị này.

**ACCEPT    all — any  any anywhere   anywhere ctstate  RELATED,ESTABLISHED:** chấp nhận toàn bộ gói tin của kết nối hiện tại. Tức khi bạn đang ở trong SSH và sửa đổi lại Firewall, nó sẽ không đẩy bạn ra khỏi SSH nếu bạn không thỏa mãn quy tắc. 

**ACCEPT    tcp —   any any anywhere   anywhere tcp dpt:ssh:** chấp nhận toàn bộ gói tin của giao thức SSH ở bất cứ interface nào, với bất kể IP nguồn và đích là bao nhiêu. Mặc định sẽ hiển thị dpt:ssh để biểu diễn cổng 22 của SSH, nếu bạn đổi SSH thành cổng khác thì sẽ hiển thị số cổng.

**ACCEPT    tcp —   any any anywhere   anywhere tcp dpt:http:** cho phép kết nối vào cổng 80, mặc định sẽ biểu diễn thành chữ http.

**ACCEPT    tcp —   any any anywhere   anywhere tcp dpt:https:** cho phép kết nối vào cổng 443, mặc định nó sẽ biểu diễn thành chữ https.

**DROP      all —   any any anywhere   anywhere:** loại bỏ tất cả các gói tin nếu không khớp với các rule ở trên.


## Các tùy chọn của IPtables là gì?

![image](https://user-images.githubusercontent.com/62273292/167086059-3f6a29b8-69f8-47e9-872c-64f91ee6c0c0.png)

**Các tùy chọn để chỉ định thông số IPtables là gì?**

- Chỉ định tên table: -t ,

- Chỉ định loại giao thức: -p ,

- Chỉ định card mạng vào: -i ,

- Chỉ định card mạng ra: -o ,

- Chỉ định địa chỉ IP nguồn: -s <địa_chỉ_ip_nguồn>,

- Chỉ định địa chỉ IP đích: -d <địa_chỉ_ip_đích>, tương tự như –s.

- Chỉ định cổng nguồn: –sport ,

- Chỉ định cổng đích: –dport , tương tự như –sport

**Các tùy chọn để thao tác với chain trong IPtables là gì?**

- Tạo chain mới: IPtables -N

- Xóa hết các rule đã tạo trong chain: IPtables -X

- Đặt chính sách cho các chain `built-in` (INPUT, OUTPUT & FORWARD): IPtables -P , ví dụ: IPtables -P INPUT ACCEPT để chấp nhận các packet vào chain INPUT

- Liệt kê các rule có trong chain: IPtables -L

- Xóa các rule có trong chain (flush chain): IPtables -F

- Reset bộ đếm packet về 0: IPtables -Z

**Các tùy chọn để thao tác với rule trong IPtables là gì?**

- Thêm rule: -A (append)

- Xóa rule: -D (delete)

- Thay thế rule: -R (replace)

- Chèn thêm rule: -I (insert)

**Một số lệnh cơ bản IPtables là gì?**

Tạo một rule mới

`IPtables -A INPUT -i lo -j ACCEPT`

Lệnh này có nghĩa là:

- A INPUT: khai báo kiểu kết nối sẽ được áp dụng (A nghĩa là Append).

- i lo: Khai báo thiết bị mạng được áp dụng (i nghĩa là Interface).

- j ACCEPT: khai báo hành động sẽ được áp dụng cho quy tắc này (j nghĩa là Jump).


Gõ lại lệnh IPtables -L -v bạn sẽ thấy 1 rule mới xuất hiện

`after-created-IPtables-rule`

Sau khi thêm mới hoặc thay đổi gõ lệnh lưu và khởi động lại IPtables để áp dụng các thay đổi.

```
service IPtables save 
service IPtables restart
```

Tiếp tục thêm một rule mới để cho phép lưu lại các kết nối hiện tại tránh hiện tượng tự block ra khỏi máy chủ.

`IPtables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT`

Cho phép các cổng được truy cập từ bên ngoài vào qua giao thức tcp: SSH(22), HTTP(80), HTTPS(443)

`IPtables -A INPUT -p tcp --dport 22 -j ACCEPT`

-p tcp : Giao thức được áp dụng (tcp, udp, all)

–dport 22: Cổng cho phép áp dụng. 22 là cho SSH

Cuối cùng, chặn toàn bộ các kết nối truy cập từ bên ngoài vào không thỏa mãn những rule trên. Tương ứng với rule 5 ở trên.

`IPtables -A INPUT -j DROP`

Bổ sung một rule mới

Để chèn 1 rule mới vào 1 vị trí (hàng) nào đó, ví dụ là vị trí thứ 2. Hãy thay tham số -A table bằng tham số INSERT -I.

`IPtables -I INPUT 2 -p tcp --dport 8080 -j ACCEPT`

Xóa 1 rule

Để xóa 1 rule mà đã tạo ra tại vị trí 4, ta sẽ sử dụng tham số -D

`IPtables -D INPUT 4`

Xóa toàn bộ các rule chứa hành động DROP có trong IPtables:

`IPtables -D INPUT -j DROP`

# Cách sử dụng IPtables để mở port VPS

Chèn chuỗi ACCEPT PORT để mở port trong IPtables với cấu trúc lệnh mở port xxx:

`# IPtables -A INPUT -p tcp -m tcp --dport xxx -j ACCEPT`

A là Append – chèn vào chuỗi INPUT (chèn xuống cuối)

`# IPtables -I INPUT -p tcp -m tcp --dport xxx -j ACCEPT`

I là Insert – chèn vào chuỗi INPUT (chèn vào dòng chỉ định rulenum).

Để tránh xung đột với rule gốc, chèn rule vào đầu, dùng –I.

**Mở port SSH**

Mở port SSH 22 để truy cập VPS thông qua SSH, cho phép kết nối SSH ở bất kì thiết bị nào, người nào, ở bất cứ đâu.

`# IPtables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT`

SSH được hiển thị mặc định ở cổng 22, nếu đổi SSH sang một cổng khác thì IPtables sẽ hiển thị số cổng.

```
ACCEPT
tcp  -- anywhere 
anywhere
cp dpt:ssh
```

Cấu hình chỉ cho phép kết nối VPS qua SSH từ một địa chỉ IP duy nhất được xác định.

`# IPtables -I INPUT -p tcp -s xxx.xxx.xxx.xxx -m tcp --dport 22 -j ACCEPT`

Lúc đó, IPtables sẽ thêm rule

`ACCEPT  tcp  -- xxx.xxx.xxx.xxx    anywhere         tcp dpt:ssh`

Mở port Web Server

Cho phép truy cập vào web server qua port mặc định 80 và 443:

```
# IPtables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT

# IPtables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
```

IPtables hiển thị HTTP và HTTPS theo mặc định

```
ACCEPT tcp -- anywhere       anywhere    tcp dpt:http

ACCEPT tcp -- anywhere      anywhere     tcp dpt:https
```

**Mở port Mail**

Cho phép user dùng SMTP Server qua port mặc định là 25 và 465:

```
# IPtables -I INPUT -p tcp -m tcp --dport 25 -j ACCEPT

# IPtables -I INPUT -p tcp -m tcp --dport 465 -j ACCEPT
```

IPtables sẽ hiển thị SMTP và URD theo mặc định

```
ACCEPT   tcp  -- anywhere      anywhere           tcp dpt:smtp

ACCEPT   tcp  -- anywhere      anywhere           tcp dpt:urd
```

Mở port POP3 (port mặc định 110 và 995) cho phép user đọc mail trên server

```
# IPtables -A INPUT -p tcp -m tcp --dport 110 -j ACCEPT

# IPtables -A INPUT -p tcp -m tcp --dport 995 -j ACCEPT
```

IPtables sẽ hiển thị POP3 và POP3S theo mặc định

```
ACCEPT 	tcp  --  anywhere         	anywhere        	tcp dpt:pop3
ACCEPT 	tcp  --  anywhere         	anywhere        	tcp dpt:pop3s
```

Cho phép sử dụng giao thức IMAP mail protocol (port mặc định là 143 và 993)

```
# IPtables -A INPUT -p tcp -m tcp --dport 143 -j ACCEPT
# IPtables -A INPUT -p tcp -m tcp --dport 993 -j ACCEPT
```

IPtables sẽ hiển thị IMAP và IMAPS theo mặc định

```
ACCEPT 	tcp  --  anywhere         	anywhere        	tcp dpt:imap
ACCEPT 	tcp  --  anywhere         	anywhere        	tcp dpt:imaps
```

Chặn 1 IP truy cập

`# IPtables -A INPUT -s IP_ADDRESS -j DROP`

Chặn 1 IP truy cập vào 1 port cụ thể

`#IPtables -A INPUT -p tcp -s IP_ADDRESS –dport PORT -j DROP`

Sau khi đã thiết lập tất cả bao gồm mở các port cần thiết hoặc hạn chế kết nối cần block toàn bộ các kết nối còn lại và cho phép toàn bộ các kết nối ra ngoài từ VPS.

```
# IPtables -P OUTPUT ACCEPT
# IPtables -P INPUT DROP
```

Kiểm tra lại các quy tắc sau khi thiết lập

`# service IPtables status`

Hoặc

`# IPtables -L –n`

-n để nói đến yếu tố cần quan tâm là địa chỉ IP, ví dụ nếu chặn kết nối từ một địa chỉ xác định thì IPtables sẽ hiển thị là xxx.xxx.xxx.xxx với tham số -n

Kết thúc, lưu lại các thiết lập tường lửa IPtables nếu không chúng sẽ mất khi reboot hệ thống. Đối với CenOS, cấu hình được lưu tại /etc/sysconfig/IPtables.

`# IPtables-save | sudo tee /etc/sysconfig/IPtables`

Hoặc

```
# service IPtables save

IPtables: Saving firewall rules to /etc/sysconfig/IPtables:[ OK ]
```

## Cách thiết lập IPtables với Linux Firewall để bảo mật Ubuntu VPS 


Hướng dẫn cài đặt IPtables Linux Firewall

Bước 1: Cài đặt IPtables Linux Firewall

- Cài đặt IPtables

Hầu hết các bản Linux hiện nay đều được tích hợp sẵn IPtables. Tuy nhiên, nếu chưa có sẵn trên Ubuntu hoặc Debian bạn có thể dùng lệnh sau để cài đặt:

```
sudo apt-get update
sudo apt-get install IPtables
```

Xem trạng thái hiện tại của IPtables

`sudo IPtables -L –v`

Trong đó, -L dùng để liệt kê tất cả quy tắc (rule) và –v để liệt kê các danh sách bổ trợ. Chú ý đến ký tự viết hoa và viết thường được phân biệt với nhau.

Ví dụ:

```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target prot opt in out source          destination
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target prot opt in out source          destination
Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target prot opt in out source          destination
```

Kết quả trên cho biết ba Chain được thiết lập mặc định là ACCEPT và không có Chain nào có rule.

**Bước 2: Định nghĩa các chain rules**

Tức là thêm nó vào danh sách chain hiện tại, dưới đây là lệnh IPtables được định dạng với các tùy chọn thông thường.


`sudo IPtables -A  -i <interface> -p <protocol (tcp/udp)> -s <source> --dport <port no.>  -j <target>`


Trong đó:

A là thêm chain rules.

i<interface> là giao diện mạng cần thực hiện lọc các gói tin.
  
p<protocol> là giao thức mang thực hiện lọc (tcp/udp).
  
dort<port no.> là cổng muốn đặt bộ lọc.
  
Cho phép lưu lượng truy cập trên localhost
  
Cho phép giao tiếp giữa ứng dụng mà database của nó trên server như bình thường.

`sudo IPtables -A INPUT -i lo -j ACCEPT`
  
Kết quả:

```
Chain INPUT (policy ACCEPT 7 packets, 488 bytes)
pkts bytes target prot opt in out source            destination
0 0 ACCEPT all  --  lo any anywhere      	anywhere
```
  
-A thêm rules vào chains INPUT cho phép tất cả kết nối ở interface lo

Các cổng được phép truy cập: HTTP, SSH, SSL

```
sudo IPtables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo IPtables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo IPtables -A INPUT -p tcp --dport 443 -j ACCEPT
```

Cho phép tất cả các truy cập TCP trên các cổng 22 (SSH), HTTP (80), HTTPS (443).

**Lọc các gói tin dựa trên nguồn**

Thêm vào tham số -s để cho phép hoặc từ chối các gói tin dựa trên IP nguồn.

`sudo IPtables -A INPUT -s 192.168.1.3 -j ACCEPT`
  
Các gói tin đến từ IP nguồn là 192.168.1.3 sẽ được nhấp nhận.

`sudo IPtables -A INPUT -s 192.168.1.3 -j DROP`
  
Các gói tin đến từ IP nguồn là 192.168.1.3 sẽ bị từ chối.

`sudo IPtables -A INPUT -m iprange --src-range 192.168.1.100-192.168.1.200 -j DROP`
  
Từ chối các gói tin từ một dãy IP, dùng tham số Iprange –m với dãy IP đặt sau-src-range.

Chặn tất cả truy cập
  
`sudo IPtables -A INPUT -j DROP`
  
Kiểm tra lại sau khi thiết lập

`sudo IPtables -L –v`
  
Lưu ý: cần DROP tất cả các gói tin từ các nguồn khác để tránh các truy cập trái phép từ các cổng mở trên server.

Xóa các rules
  
`sudo IPtables -F`
  
Xóa tất cả các rules để tạo lại từ đầu.

Để xóa từng rule khác nhau dùng tham số -D và chọn số tương ứng. Liệt kê các rule bằng lệnh:

`sudo IPtables -L --line-numbers`
  
Kết quả:

```
Chain INPUT (policy ACCEPT)
num  target prot opt source        	destination
ACCEPT all  --  192.168.0.4   	anywhere
ACCEPT tcp  --  anywhere      	anywhere      	tcp dpt:https
ACCEPT tcp  --  anywhere      	anywhere      	tcp dpt:http
ACCEPT tcp  --  anywhere      	anywhere      	tcp dpt:ssh
```
  
Sau đó, xóa một rule bằng cú pháp

`sudo IPtables -D INPUT 3`
  
Xóa rules số 3 ở chain INPUT

Bước 3: Lưu giữ các thay đổi
Những IPtables rules được tạo ra đều được lưu trong bộ nhớ, khi reboot máy chủ cần phải tạo lại các rules này. Để lưu giữ các thay đổi vào hệ thống dùng lệnh:

`sudo /sbin/IPtables-save`
  
Để tắt firewall, dùng lệnh:

```
sudo IPtables -F
sudo /sbin/IPtables-save
```


# 3. Cách sử dụng Iptables để mở port VPS


  



























