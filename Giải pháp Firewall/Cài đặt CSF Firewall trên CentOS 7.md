# Cài đặt CSF Firewall trên CentOS 7

1. Bước 1: Dừng và vô hiệu hóa tường lửa.

Để dừng và vô hiệu hoá Firewalld trên centos các bạn sử dụng 2 lệnh sau

```
systemctl disable firewalld 
systemctl stop firewalld
```

![image](https://user-images.githubusercontent.com/62273292/166622653-2a0ecff4-53b9-4927-a7b1-9e382a22119c.png)


2. Bước 2: Cài đặt iptables.

Sau khi đã dừng và vô hiệu hoá Firewalld chúng ta tiến hành cài đặt ibtables

`yum -y install iptables-services`

![image](https://user-images.githubusercontent.com/62273292/166622742-6ce1d74b-a42c-4493-9a77-73efc0b7e350.png)

**Tạo tập tin cần thiết bởi iptables.**

```
touch /etc/sysconfig/iptables 
touch /etc/sysconfig/iptables6
```

![image](https://user-images.githubusercontent.com/62273292/166622803-986e78ca-672b-4b8c-b462-737f10cbf2c9.png)

Khởi động iptables.

```
systemctl start iptables 
systemctl start ip6tables
```

![image](https://user-images.githubusercontent.com/62273292/166623068-25d9925c-774f-4a7c-998e-0da6461745bd.png)


Kích hoạt iptables mỗi khi khởi động lại VPS/Server.

```
systemctl enable iptables 
systemctl enable ip6tables
```

![image](https://user-images.githubusercontent.com/62273292/166623102-d380611c-d6e2-490e-b957-9141191341e7.png)


3. Bước 3: Cài đặt các thư viện cần thiết.

Tiếp theo các bạn tiến hành cài đặt các thư viện cần thiết cho việc hoạt động của CSF

`yum -y install wget perl unzip net-tools perl-libwww-perl perl-LWP-Protocol-https perl-GDGraph`

![image](https://user-images.githubusercontent.com/62273292/166623155-84b7964a-7c70-446f-91f7-76af86aeddf3.png)


4. Bước 4:  cài đặt CSF.

Sau khi đã cài đặt đầy đủ các thư viện chúng ta tiến hành cài đặt CSF. Việc cài đặt diễn ra hết sức đơn giản với các lệnh dưới đây

```
cd /opt
wget https://download.configserver.com/csf.tgz 
tar -xzf csf.tgz 
cd csf 
sh install.sh
```

![image](https://user-images.githubusercontent.com/62273292/166623529-ac957022-2053-4bdc-a8f6-8708043d61ad.png)

![image](https://user-images.githubusercontent.com/62273292/166623613-4ce4a77d-5049-4d57-8e1c-e6b32bab4794.png)


Loại bỏ các tập tin cài đặt.

```
cd /
rm -rf /opt/csf /opt/csf.tgz
```
![image](https://user-images.githubusercontent.com/62273292/166623723-a985c1da-6413-4160-b8dd-01ce3a0995f9.png)


Bây giờ chúng ta sẽ kiểm tra xem CSF có thực sự hoạt động trên máy chủ không. Chúng tôi sẽ làm một bài kiểm tra để xác minh.

```
cd /usr/local/csf/bin/
perl csftest.pl
```

![image](https://user-images.githubusercontent.com/62273292/166623803-9a1a70a4-d6a2-4fcb-b3d2-422f852e4e55.png)


Nếu bạn thấy kết quả như hiển thị như bên dưới thì CSF sẽ hoạt động mà không gặp sự cố nào trên máy chủ của bạn.

```
Testing ip_tables/iptable_filter...OK
Testing ipt_LOG...OK
Testing ipt_multiport/xt_multiport...OK
Testing ipt_REJECT...OK
Testing ipt_state/xt_state...OK
Testing ipt_limit/xt_limit...OK
Testing ipt_recent...OK
Testing xt_connlimit...OK
Testing ipt_owner/xt_owner...OK
Testing iptable_nat/ipt_REDIRECT...OK
Testing iptable_nat/ipt_DNAT...OK

RESULT: csf should function on this server
```

5. Bước 5: Cấu hình CSF

Tiếp theo, chúng ta sẽ cần cấu hình CSF bằng cách chỉnh sửa file /etc/csf/csf.confcsf.conf.

`nano /etc/csf/csf.conf`


Các bạn sẽ cần sửa một số thông số dưới đây

```
TESTING = "0"
RESTRICT_SYSLOG = "3"
```


```
systemctl enable csf
systemctl enable lfd
systemctl start csf
```

![image](https://user-images.githubusercontent.com/62273292/166624865-70bb2107-0df6-4d33-a2a9-b631e89398fb.png)


Để kiểm tra xem csf đã hoạt động hay chưa các bạn có thể sử dụng lệnh dưới đây

`systemctl status csf`

![image](https://user-images.githubusercontent.com/62273292/166625278-567be6c0-4ae9-47b7-b3bc-83b7f6f7da70.png)


6. Mở Port SMTP
Theo mặc định CSF sẽ không mở TCP_OUT với port 465, điều này có thể sẽ khiến bạn gặp lỗi khi sử dụng SMTP mail. Để mở port 465 các bạn mở file /etc/csf/csf.conf và tìm dòng sau

`TCP_OUT = "20,21,22,25,53,80,110,113,443,587,993,995"`

Sửa lại thành

`TCP_OUT = "20,21,22,25,53,80,110,113,443,587,465,993,995"`

Tiến hành khởi động lại CSF

```
csf -x
csf -e
```











