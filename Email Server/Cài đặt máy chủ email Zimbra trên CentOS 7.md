# Cài đặt máy chủ email Zimbra trên CentOS 7

Kiểm tra và cập nhật hệ thống

![image](https://user-images.githubusercontent.com/62273292/161475698-f4c0c469-442e-4cfa-b74d-da41ab11ab26.png)

Thực hiện stop postfix và remove postfix.


Postfix là một phầm mềm nguồn mở được dùng để gửi mail (Mail Transfer Agent-MTA). Được phát hành bởi IBM với mục tiêu thay thế trình gửi mail phổ biến là sendmail. Nó được trang bị trên hệ điều hành do đó bạn hãy xoá bỏ để sử dụng dịch vụ riêng của Zimbra.

![image](https://user-images.githubusercontent.com/62273292/161476051-2fc65c98-1ea3-4482-bfc5-a1d63f1c0213.png)

Kiểm tra và set hostname

![image](https://user-images.githubusercontent.com/62273292/161476432-78f166a5-2bca-4cf1-a905-9bb6cc624f2b.png)

Sau khi set hostname xong bạn thêm dòng sau vào file hosts bạn nhớ thay đổi IP bằng IP của bạn nha.

![image](https://user-images.githubusercontent.com/62273292/161476885-3c1987ce-7dfa-4ec4-abad-59400e2add55.png)

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

## Tạo domain thêm hostname

![image](https://user-images.githubusercontent.com/62273292/161525047-42e7f38b-eb0e-4e49-adca-8802514939e3.png)
















