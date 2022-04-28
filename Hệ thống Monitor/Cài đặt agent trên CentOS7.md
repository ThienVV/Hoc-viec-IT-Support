# Hướng dẫn cài đặt agent của checkmk trên centos 7

![image](https://user-images.githubusercontent.com/62273292/165668536-1998ebc7-0fd0-4b12-bc0e-930ffdff7d56.png)


Thông số VM

Host name	IP	RAM	CPU	DISK
check_mk	192.168.176.145	1G	1	20G
client	192.168.176.146	1G	1	20G

**Các bước thực hiện với client centos 7**

1 Tìm agent phù hợp

![image](https://user-images.githubusercontent.com/62273292/165668705-4c185d1c-83d2-4799-9fe7-929ed35cfcf9.png)

Trên các website của check_mk server khi bạn cài đặt và đăng nhập vào nó sẽ hỗ trợ và hiển thị cho bạn các agent 3 loại agent. Việc của bạn là chọn agent phù hợp với hệ điều hành của mình. Ở đây tôi cài đặt agent trên centos 7 nên tôi sẽ chọn agent có đuôi là .rpm để tiến hành cài đặt

NOTE: Các bước dưới đây tất cả đều được thực hiện trên client mà bạn muốn được giám sát. Và các command line được chạy dưới quyền user sudo hoặc user root

2. Cài đặt gói wget

`yum install wget -y `

3. Dùng gói wget download agent đã chọn ở bước trên

`wget http://192.168.176.145/monitoring/check_mk/agents/check-mk-agent-2.0.0p23-1.noarch.rpm`

4. Cấp quyền thực thi cho file vừa download về

`chmod +x check-mk-agent-2.0.0p23-1.noarch.rpm`


5. Cài đặt agent

`rpm -ivh check-mk-agent-2.0.0p23-1.noarch.rpm`

6. Cài đặt xinetd

`yum install xinetd -y`

7. Khởi động xinetd

```
systemctl start xinetd
systemctl enable xinetd
```

8. Cài đặt gói net-tools để kiểm tra dễ dàng hơn

`yum install net-tools -y`

9. Mở port trên client để có thể giao tiếp với check_mk server

`vi /etc/xinetd.d/check_mk`

Sửa các thông số sau

```
only_from      = 192.168.80.222
disable        = 0
port           = 6556
```

![image](https://user-images.githubusercontent.com/62273292/165668999-2cd1270b-aad3-413c-a01f-616efa88be9b.png)


10. Kiểm tra port mặc định của check_mk sử dụng để giám sát được chưa

`netstat -npl | grep 6556`

![image](https://user-images.githubusercontent.com/62273292/165669047-3ebb8cad-6358-4b6f-9356-1595235cb253.png)

11. Mở port trên firewall

```
 firewall-cmd --add-port=6556/tcp --permanent
 firewall-cmd --reload
```
 
12. Tắt selinux

























