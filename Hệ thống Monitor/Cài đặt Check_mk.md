 1 Cài đặt gói wget
 
 `yum install wget -y`
 
 ![image](https://user-images.githubusercontent.com/62273292/165048130-71026762-526a-40cc-9e0f-06b09d69b6ef.png)

 
 2. Khai báo repo

`yum install epel-release -y`

![image](https://user-images.githubusercontent.com/62273292/165048400-f4c169c9-900e-481a-8951-ec7cc39894b5.png)


3. Sử dụng wget để download check_mk

wget https://mathias-kettner.de/support/1.5.0p12/check-mk-raw-1.5.0p12-el7-38.x86_64.rpm

4. Cài đặt check_mk bằng link vừa download. Ở đây tôi lấy link của tôi đã download về. Hãy lấy link của các bạn nhé

`yum install check-mk-raw-1.5.0p12-el7-38.x86_64.rpm -y `

5. Mở port 80 để sử dụng dịch vụ httpd

`firewall-cmd --permanent --add-port=80/tcp`

`firewall-cmd --reload`

6. Tắt selinux

`setenforce 0 `

7. Tạo và khởi động site

`omd create monitoring`

`omd start monitoring`

8. Đặt mật khẩu cho site

`su - monitoring`

`htpasswd -m ~/etc/htpasswd omdadmin`

9. Đăng nhập vào trang web bằng tài khoản admin

http://192.168.80.222/monitoring/check_mk
