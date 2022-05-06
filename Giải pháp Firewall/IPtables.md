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




1. Cài đặt Iptables

– Iptables thường được cài đặt mặc định trong hệ thống. Nếu chưa được cài đặt:

CentOS: # yum install iptables

CentOS 7 sử dụng FirewallD làm tường lửa mặc định thay vì Iptables. Nếu bạn muốn sử dụng Iptables thực hiện:

```
# systemctl mask firewalld
# systemctl enable iptables
# systemctl enable ip6tables
# systemctl stop firewalld
# systemctl start iptables
# systemctl start ip6tables
```

– Kiểm tra Iptables đã được cài đặt trong hệ thống:
Trên CentOS:

```
# rpm -q iptables
iptables-1.4.7-16.el6.x86_64
# iptables --version
iptables v1.4.7
```

![image](https://user-images.githubusercontent.com/62273292/167108014-64a4a0d7-b067-4a5c-871a-272c5c63d19b.png)


– Check tình trạng của Iptables, cũng như cách bật tắt services trên CentOS

```
# service iptables status
# service iptables start
# service iptables stop
# service iptables restart
```

![image](https://user-images.githubusercontent.com/62273292/167108182-ae8f818a-f693-42cc-a5de-e1b49ace0bed.png)

![image](https://user-images.githubusercontent.com/62273292/167108330-fe6ac30a-c0a7-414f-b7d0-489247d48e6a.png)


– Khởi động Iptables cùng hệ thống

`# chkconfig iptables on`

2. Các nguyên tắc áp dụng trong Iptables


Để bắt đầu, bạn cần xác định các services muốn đóng/mở và các port tương ứng.

Ví dụ, với một website và mail server thông thường

Để truy cập VPS bằng SSH, bạn cần mở port SSH – 22.

Để truy cập website, bạn cần mở port HTTP – 80 và HTTPS – 443.

Để gửi mail, bạn sẽ cần mở port SMTP – 22 và SMTPS – 465/587

Để người dùng nhận được email, bạn cần mở port POP3 – 110, POP3s – 995, IMAP – 143 và IMAPs – 993

Sau khi đã xác định được các port cần mở, bạn cần thiết lập các quy tắc tường lửa tương ứng để cho phép.

Bạn có thể xóa toàn bộ các quy tắc firewall mặc định để bắt đầu từ đầu: # iptables -F

Mình sẽ hướng dẫn các bạn xem và hiểu các quy tắc của iptables. Liệt kê các quy tắc hiện tại:

# iptables -L

Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere            state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:ssh
REJECT     all  --  anywhere             anywhere            reject-with icmp-host-prohibited
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:http
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:https
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:smtp
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:urd
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:pop3
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:pop3s
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:imap
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:imaps
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere             anywhere            reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination

![image](https://user-images.githubusercontent.com/62273292/167108635-831c0a01-5b0a-450f-bfa1-d977bd4a3170.png)


### Cột 1: TARGET hành động sẽ được áp dụng cho mỗi quy tắc

**Accept:** gói dữ liệu được chuyển tiếp để xử lý tại ứng dụng cuối hoặc hệ điều hành

**Drop:** gói dữ liệu bị chặn, loại bỏ

**Reject:** gói dữ liệu bị chặn, loại bỏ đồng thời gửi một thông báo lỗi tới người gửi

#### Cột 2: PROT (protocol – giao thức) quy định các giao thức sẽ được áp dụng để thực thi quy tắc, bao gồm all, TCP hay UDP. Các ứng dụng SSH, FTP, sFTP… đều sử dụng giao thức TCP.

### Cột 4, 5: SOURCE và DESTINATION địa chỉ của lượt truy cập được phép áp dụng quy tắc.

3. Cách sử dụng Iptables để mở port VPS


Để mở port trong Iptables, bạn cần chèn chuỗi ACCEPT PORT. Cấu trúc lệnh để mở port xxx như sau:

`# iptables -A INPUT -p tcp -m tcp --dport xxx -j ACCEPT`


A tức Append – chèn vào chuỗi INPUT (chèn xuống cuối)

hoặc

`# iptables -I INPUT [rulenum] -p tcp -m tcp --dport xxx -j ACCEPT`

I tức Insert- chèn vào chuỗi INPUT (chèn vào dòng chỉ định rulenum)

Để tránh xung đột với rule gốc, các bạn nên chèn rule vào đầu, sử dụng -I

3.1. Mở port SSH

Để truy cập VPS qua SSH, bạn cần mở port SSH 22. Bạn có thể cho phép kết nối SSH ở bất cứ thiết bị nào, bởi bất cứ ai và bất cứ dâu.

# iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT

Mặc định sẽ hiển thị ssh cho cổng 22, nếu bạn đổi ssh thành cổng khác thì iptables sẽ hiển thị số cổng

ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:ssh

Bạn có thể chỉ cho phép kết nối VPS qua SSH duy nhất từ 1 địa chỉ IP nhất định (xác định dễ dàng bằng cách truy cập các website check ip hoặc lệnh # w)

# iptables -I INPUT -p tcp -s xxx.xxx.xxx.xxx -m tcp --dport 22 -j ACCEPT

Khi đó, trong iptables sẽ thêm rule

ACCEPT     tcp  --  xxx.xxx.xxx.xxx       anywhere            tcp dpt:ssh

3.2. Mở port Web Server

Để cho phép truy cập vào webserver qua port mặc định 80 và 443:

```
# iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
# iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
```

Mặc định Iptables sẽ hiển thị HTTP và HTTPS

```
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:http
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:https
```

3.3. Mở port Mail

– Để cho phép user sử dụng SMTP servers qua port mặc định 25 và 465:

```
# iptables -I INPUT -p tcp -m tcp --dport 25 -j ACCEPT
# iptables -I INPUT -p tcp -m tcp --dport 465 -j ACCEPT
```

Mặc định Iptables sẽ hiển thị SMTP và URD

```
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:smtp
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:urd
```

– Để user đọc email trên server, bạn cần mở port POP3 (port mặc định 110 và 995)

```
# iptables -A INPUT -p tcp -m tcp --dport 110 -j ACCEPT
# iptables -A INPUT -p tcp -m tcp --dport 995 -j ACCEPT
```

Mặc định Iptables sẽ hiển thị POP3 và POP3S

```
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:pop3
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:pop3s
```

Bên cạnh đó, bạn cũng cần cho phép giao thức IMAP mail protocol (port mặc định 143 và 993)

```
# iptables -A INPUT -p tcp -m tcp --dport 143 -j ACCEPT
# iptables -A INPUT -p tcp -m tcp --dport 993 -j ACCEPT
```

Mặc định Iptables sẽ hiển thị IMAP và IMAPS

```
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:imap
ACCEPT     tcp  --  anywhere             anywhere            tcp dpt:imaps
```

3.4. Chặn 1 IP truy cập

`# iptables -A INPUT -s IP_ADDRESS -j DROP`

– Chặn 1 IP truy cập 1 port cụ thể:

`#iptables -A INPUT -p tcp -s IP_ADDRESS –dport PORT -j DROP`

Sau khi đã thiết lập đầy đủ, bao gồm mở các port cần thiết hay hạn chế các kết nối, bạn cần block toàn bộ các kết nối còn lại và cho phép toàn bộ các kết nối ra ngoài từ VPS

```
# iptables -P OUTPUT ACCEPT
# iptables -P INPUT DROP
```

Sau khi đã thiết lập xong, bạn có thể kiểm tra lại các quy tắc

`# service iptables status`

Hoặc

`# iptables -L –n`

-n nghĩa là chúng ta chỉ quan tâm mỗi địa chỉ IP . Ví dụ, nếu chặn kết nối từ hocvps.com thì iptables sẽ hiển thị là xxx.xxx.xxx.xxx với tham số -n
Cuối cùng, bạn cần lưu lại các thiết lập tường lửa Iptables nếu không các thiết lập sẽ mất khi bạn reboot hệ thống. Tại CentOS, cấu hình được lưu tại /etc/sysconfig/iptables.

`# iptables-save | sudo tee /etc/sysconfig/iptables`

Hoặc

`# service iptables save`

iptables: Saving firewall rules to /etc/sysconfig/iptables:[ OK ]




