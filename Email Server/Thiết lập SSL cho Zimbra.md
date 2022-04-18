# Cài đặt Let's Encrypt trong zimbra

Truy cập ssh vào server zimbra và stop hết các service bằng lệnh

`su - zimbra -c 'zmcontrol stop'`

![image](https://user-images.githubusercontent.com/62273292/163748581-e003af5f-c423-4793-af76-22d087cec6b5.png)

Tiếp theo chúng ta cài đặt git cho server bằng lệnh

`yum install git -y`

