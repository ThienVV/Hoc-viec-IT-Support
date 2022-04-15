# Zimbra là gì?

Zimbra được biết đến là bộ phần mềm bao gồm máy chủ email và máy khách website, hay nói cách khác dễ hiểu hơn, Zimbra Collaboration Suite(Zimbra) là một trong những ứng dụng nguồn mở miễn phí nổi tiếng về tính năng, độ định và bảo mật cao. Zimbra không chỉ đơn giản là tên của một ứng dụng về email mà nó còn là một giải pháp, một hệ thống khá hoàn chỉnh để triển khai môi trường chia sẻ công tác phục vụ cho quản lý và công việc thông qua các tính năng chính sau:

Thư điện tử: một hệ thống thư điện tử hoàn chỉnh gồm Mail server (SMTP, POP3, IMAP, antivirus, antispam, openLDAP, backup, …, có đầy đủ các tính năng như auto-reply, auto-forward, mail filter, …) và Mail client (Zimbra desktop và Zimbra Web Client).

Lịch công tác (calendar): lịch cá nhân và lịch nhóm, tự động gửi mail mời họp,…

Sổ địa chỉ (Contacts): sổ cá nhân và sổ chung của nhóm

Danh mục công việc (Task): của cá nhân và nhóm.

Tài liệu (Documents): tài liệu dưới dạng wiki của cá nhân hoặc soạn tập thể

Cặp hồ sơ (Briefcase): lưu file dùng riêng hoặc chung.

Chat: chat nội bộ trong mạng LAN hoặc trên Internet.

Tất cả các mục trên đều có phần chạy trên máy chủ (nằm trong Zimbra Server), lưu trên máy chủ để có thể dùng chung được và truy cập được từ bất kỳ đâu có Internet. (nếu cài trên máy chủ có Internet). Các mục đó đều có khả năng share (kể cả các thư mục email: Inbox, Sent) cho người khác dùng chung.

Zimbra có hai phần mềm client: Zimbra desktop và Zimbra Web client là giao diện với người dùng. Zimbra desktop (tương tự như Outlook, KMail,…) cài được trên Windows, Mac, Linux. Ngoài ra có thể dùng các mail client khác như Outlook, Evolution, KMail, Thunderbird, … Hai loại mail client trên ứng với hai cách làm việc:

Làm việc online, dùng Zimbra web client. Mọi thông tin sẽ lưu trên máy chủ Zimbra. Zimbra Web Client có hai giao diện: dạng html thông thường, nhanh nhưng ít tính năng và dạng Ajax (tương tự Yahoo Mail). Zimbra Web Client là một trong những Web Client hoàn chỉnh nhất hiện nay (hỗ trợ hầu hết tính năng của Zimbra Server, kể cả chat).

Làm việc offline, dùng các mail client còn lại. Riêng Outlook, Apple Desktop và Evolution có thể đồng bộ email, calendar, contacts và task với máy chủ Zimbra, các mail client khác chỉ dùng đọc và gửi email.

Zimbra cũng hỗ trợ làm việc với các điện thoại di động iPhone, Blackberry, …

Về kiến trúc bên trong, Zimbra vẫn sử dụng các bộ phần mềm chức năng (nguồn mở) phổ biến như OpenLDAP, Postfix, SpamAssassin, Amavisd, Tomcat, … cùng với một số phần mềm riêng tạo nên một hệ thống tích hợp chặt chẽ. Có thể không dùng OpenLDAP mà dùng Windows Active Directory, hoặc import user từ một máy chủ Exchange sang.

Hiện tại, Zimbra Server có các bản cài trên RedHat, Fedora, CentOS, Debian, SUSE, Ubuntu và MacOS. Nếu chỉ cài trên một máy chủ độc lập thì cách cài đặt khá đơn giản và nhanh.

Zimbra có thể cài theo nhiều cấu hình khác nhau từ một hệ thống nhỏ vài chục account trên một máy chủ duy nhất cho đến hệ thống rất lớn hàng nghìn account trên nhiều máy chủ có các chức năng khác nhau. Có khả năng mở rộng (scalability) bằng cách thêm máy chủ dễ dàng.

Hiện đang chạy thử trên một cặp máy chủ clustering bằng drbd và heartbeat và chưa chê được điểm gì. Hoàn toàn có thể thay được cặp Exchange + Outlook (nhất là với trình độ sử dụng như hiện nay). Phải chạy thật và sau một thời gian mới có thể phát hiện xem có lỗi gì không.

Zimbra có một kho các Zimlet (một thứ tương tự các extensions của Firefox) mà các quản trị mạng có thể chọn cài để bổ xung tính năng. Mọi người có thể tự viết các Zimlet để kết nối hệ thống Zimbra với các hệ thống thông tin khác hoặc mở rộng tính năng. Đây có lẽ là một trong những điểm mạnh nhất và sẽ gây nghiện cho người dùng giống như các extensions của Firefox vậy.

Quản trị hệ thống qua giao diện web khá đầy đủ và chi tiết với nhiều tiện ích. Ví dụ có thể tạo hàng trăm account trong vài phút.

# Cài đặt máy chủ email Zimbra trên CentOS 7

## Tạo domain thêm hostname

![image](https://user-images.githubusercontent.com/62273292/163558486-fd9ee3ec-09d5-4d63-9039-55c5bcf40c1d.png)



Kiểm tra và cập nhật hệ thống

![image](https://user-images.githubusercontent.com/62273292/161475698-f4c0c469-442e-4cfa-b74d-da41ab11ab26.png)

Thực hiện stop postfix và remove postfix.


Postfix là một phầm mềm nguồn mở được dùng để gửi mail (Mail Transfer Agent-MTA). Được phát hành bởi IBM với mục tiêu thay thế trình gửi mail phổ biến là sendmail. Nó được trang bị trên hệ điều hành do đó bạn hãy xoá bỏ để sử dụng dịch vụ riêng của Zimbra.

![image](https://user-images.githubusercontent.com/62273292/161476051-2fc65c98-1ea3-4482-bfc5-a1d63f1c0213.png)

Kiểm tra và set hostname

![image](https://user-images.githubusercontent.com/62273292/163560194-c12d3223-18fe-44a1-8644-fe864c1b18cb.png)

Sau khi set hostname xong bạn thêm dòng sau vào file hosts bạn nhớ thay đổi IP bằng IP của bạn nha.

![image](https://user-images.githubusercontent.com/62273292/163560279-7099cfc9-5524-49d9-812c-5ef6b7d9f6d9.png)

Cài đặt Zimbra

Bạn thực hiệ chạy lệnh sau để install Zimbra & ZCS dependencies

`yum install unzip net-tools sysstat openssh-clients perl-core libaio nmap-ncat libstdc++.so.6 wget -y`

![image](https://user-images.githubusercontent.com/62273292/161488070-95c51758-dbaa-443d-9425-6db3371bff00.png)

Bước tiếp theo bạn cần Download Zimbra và cài đặt. Và bạn cần tạo một thư mục zimbra để cài vào đó. Bạn cũng có thể xem các phiên bản Zimbra ở trang chủ để download nhé.

```
[root@mail ~]# mkdir zimbra && cd zimbra
[root@mail zimbra]# wget https://files.zimbra.com/downloads/8.8.15_GA/zcs-NETWORK-8.8.15_GA_3869.RHEL7_64.20190918004220.tgz.md5
```
![image](https://user-images.githubusercontent.com/62273292/161487987-5d89cb45-21cc-4220-82bd-a18586464f57.png)

Sau khi download về hoàn tất bạn tiến hành giải nén file ra


![image](https://user-images.githubusercontent.com/62273292/161488253-cc08b19a-da05-4b2a-a300-8456f7e5c3b1.png)


`cd zcs* && ./install.sh`

![image](https://user-images.githubusercontent.com/62273292/161488441-c43114d4-6493-4eb5-8dd4-51af1c338eff.png)


![image](https://user-images.githubusercontent.com/62273292/161488721-5f9c0dad-1732-47e1-b462-391cec4d0e8e.png)


![image](https://user-images.githubusercontent.com/62273292/161512593-a28614c1-21a1-4733-bf25-592f89d98ef8.png)

![image](https://user-images.githubusercontent.com/62273292/161916201-dc046be5-ca68-4245-a731-00a3bd2467a8.png)

Cài mật khẩu

![image](https://user-images.githubusercontent.com/62273292/161949529-191bf480-ce3e-4e4b-822e-19fe98ac0273.png)


Mở Port Firewall

```
firewall-cmd --permanent --add-port={25,80,110,143,443,465,587,993,995,5222,5223,9071,7071}/tcp
firewall-cmd --reload
```


![image](https://user-images.githubusercontent.com/62273292/161916801-9739bb2d-630e-4b00-bac9-b5eea94e7133.png)



![image](https://user-images.githubusercontent.com/62273292/161935282-e0fc3e16-d24d-4d54-a8cb-f4306b84b818.png)


Đăng nhập địa chỉ ip https://192.168.176.132:7071/

![image](https://user-images.githubusercontent.com/62273292/163558723-647df287-910a-47b1-9d10-7212ac87466c.png)

Đăng nhập thành công

![image](https://user-images.githubusercontent.com/62273292/163558846-8a1ac637-a6c9-4d20-94a6-8e5d01c55eb5.png)




link tham khảo https://dotrungquan.info/huong-dan-cai-dat-may-chu-email-zimbra-tren-centos-7/










