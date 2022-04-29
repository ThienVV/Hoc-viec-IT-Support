# Hướng dẫn cài đặt Zabbix 5.0 trên CentOS 7

Hướng dẫn chi tiết cách cài đặt Zabbix 5.0 trên CentOS 7 giúp giám sát dịch vụ hệ thống với nhiều tính năng độc đáo và khả năng tùy biến cao

1. Cài đặt Zabbix Server trên CentOS 7

**Cài đặt Zabbix repository**

```
# rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
# yum clean all
```

**Cài đặt Zabbix Server và Zabbix Agent**

`# yum install zabbix-server-mysql zabbix-agent`

**Cài đặt Zabbix frontend**

`yum install -y centos-release-scl`

Chỉnh sửa tập tin zabbix.repo để bật cho phép cài zabbix-frontend từ repository.

`vi /etc/yum.repos.d/zabbix.repo`

Đặt giá trị enable=1 vào [zabbix-frontend]

![image](https://user-images.githubusercontent.com/62273292/165876253-b3f4f928-f93d-4d55-b008-a3fc6f4390c2.png)

Sau đó tiến hành cài đặt Zabbix frontend từ repository.

`# yum install zabbix-web-mysql-scl zabbix-apache-conf-scl`

2. Cài đặt MariaDB


Bước 1: update hệ thống 

![image](https://user-images.githubusercontent.com/62273292/160348938-8663e20e-d80e-4885-82df-2bc14337a428.png)

Bước 2: Cài đặt MariaDB

`apt install -y software-properties-common mariadb-server mariadb-client`

![image](https://user-images.githubusercontent.com/62273292/160349325-f6ea7a7c-9cbd-47f9-844e-1b044d456a78.png)


Bước 3: Khởi động dịch vụ MariaDB

![image](https://user-images.githubusercontent.com/62273292/160349505-243b27e2-e6e0-4764-8781-8fab3c3254d0.png)

Bước 4: Kiểm tra trạng thái của MariaDB

`systemctl status mariadb`

![image](https://user-images.githubusercontent.com/62273292/160349846-04c87961-a329-41d2-ba59-75740cd04fcf.png)


4. Cấu hình PHP

Mở tập tin zabbix.conf uncomment ; php_value[date.timezone] = Europe/Riga và sửa thành Asia/Ho_Chi_Minh

`vi /etc/opt/rh/rh-php72/php-fpm.d/zabbix.conf`

![image](https://user-images.githubusercontent.com/62273292/165876781-9a963bcb-08df-42bb-a2f9-54e1452dfbe6.png)

5. Khởi động Zabbix server và agent

```
# systemctl restart zabbix-server zabbix-agent httpd rh-php72-php-fpm
# systemctl enable zabbix-server zabbix-agent httpd rh-php72-php-fpm
```

6. Thiết lập tường lửa

```
firewall-cmd --add-service={http,https} --permanent
firewall-cmd --add-port={10051/tcp,10050/tcp} --permanent
firewall-cmd --reload
```

7. Thiết lập Zabbix Dashboard

Sau khi hoàn tất các bước trên, bạn tiến hành mở trình duyệt và nhập địa chỉ http://ip_server_cua_ban/zabbix.

Ví dụ ip của tôi là 192.168.176.147 tôi sẽ nhập trên trình duyệt http://192.168.176.147/zabbix.

![image](https://user-images.githubusercontent.com/62273292/165876894-50edb817-5ea7-4e86-9e46-93bb7fe42b95.png)

![image](https://user-images.githubusercontent.com/62273292/165876905-4e80f77f-4b41-41b3-a8d0-1e85c8d690d8.png)

![image](https://user-images.githubusercontent.com/62273292/165876912-99aacb4e-3ae1-47ea-9f9e-8ec22f629a55.png)

Đặt tên cho name server

![image](https://user-images.githubusercontent.com/62273292/165876978-f1c3596f-a0de-42ff-9a86-b989b087e880.png)


![image](https://user-images.githubusercontent.com/62273292/165876988-bd8b656b-5be5-4155-9bde-a1b3e2f66b42.png)

![image](https://user-images.githubusercontent.com/62273292/165876991-6aabe07f-c2ff-4b5d-93af-0be353ad9506.png)

![image](https://user-images.githubusercontent.com/62273292/165877000-5903e70d-bcf5-4aea-bca1-97bb6ffeed79.png)

![image](https://user-images.githubusercontent.com/62273292/165877026-1c1043da-4be7-4f54-b8fb-2ca4ddcb40cf.png)












