# Cài đặt và sử dụng Mssql trên windows server

Link download: https://www.microsoft.com/en-us/sql-server/sql-server-downloads

![image](https://user-images.githubusercontent.com/62273292/161185558-1ef111cc-e8b3-4402-b8e5-069989c6a6fb.png)

Chọn custom

![image](https://user-images.githubusercontent.com/62273292/161185663-be0f044f-23b3-4bbf-a81a-e0b1d4ddb635.png)

Cài đặt

![image](https://user-images.githubusercontent.com/62273292/161186812-2b7663be-5717-4972-bd4c-061ed386cbe2.png)

Cài ssms

![image](https://user-images.githubusercontent.com/62273292/161187204-0c6aed17-661f-4e66-a018-e20119c599cd.png)

![image](https://user-images.githubusercontent.com/62273292/161188700-8ebae1ff-b79f-4396-8f83-f5ca260a5fe3.png)

![image](https://user-images.githubusercontent.com/62273292/161212254-df2083dd-ffdf-4518-827c-f26c6e7e3daa.png)


Có 2 chế độ xác thực chính là Windows Authentication và SQL Server Authentication

![image](https://user-images.githubusercontent.com/62273292/161212428-3c09c86a-ad58-4fce-ae4a-585a86a591e3.png)


  Chế độ Windows Authentication: Là chế độ xác thực người dùng windows, chỉ cần có user vào windows là được, không cần nhập Password.
  
  Chế độ SQL Server Authentication: Là chế độ xác thực người dùng mức SQL Server, do SQL server quản lý user và password, người dùng phải có user và password mới có thể  truy cập vào SQL Server
      - SQL Server có 1 user mặc định full quyền là security admin- viết tắt là sa.
      - Password của user sa do người dùng nhập vào khi cài đặt SQL Server
   


Khi đăng nhập vào thì sẽ có giao diện chính 

![image](https://user-images.githubusercontent.com/62273292/161212767-bec8cdda-244e-4aba-b6b0-49756e35e4a4.png)

Chọn new Query và bắt đầu thực hiện các câu lệnh cơ bản

Tạo 1 cơ sỡ dữ liệu mới

![image](https://user-images.githubusercontent.com/62273292/161213392-dbefd112-32c6-4502-8939-ea573000cd12.png)

Tạo bảng cho database

![image](https://user-images.githubusercontent.com/62273292/161214726-02dc067e-d80b-436a-b781-b1ebb46fbdbf.png)


Chèn dữ liệu vào trong bảng

![image](https://user-images.githubusercontent.com/62273292/161215525-ab8ff9b8-ebd8-440f-aed9-44037c6878c7.png)

Nối 2 bảng lại với nhau với trường id

![image](https://user-images.githubusercontent.com/62273292/161215839-06fe16ec-b75d-4829-936f-be9a3ace1b6a.png)


![image](https://user-images.githubusercontent.com/62273292/161216039-22008f75-bb2a-4ee3-962b-80308d66f494.png)

![image](https://user-images.githubusercontent.com/62273292/161216068-5f535e02-90c8-4f6c-af25-56f423b8fe3b.png)

Dùng lệnh select để xem dữ kiệu trong bảng

![image](https://user-images.githubusercontent.com/62273292/161216562-fd0ac15e-911c-4099-8aee-9037d60d8bdc.png)

Dùng lệnh update để cập nhật dữ liệu trong bảng

![image](https://user-images.githubusercontent.com/62273292/161217310-b141a5a2-22d0-431d-b340-a968def55725.png)

Sau khi update thành công thì sẽ hiển thị xem đã update đúng chưa

![image](https://user-images.githubusercontent.com/62273292/161217710-11b53c6e-27f9-411f-8014-3efc52381e48.png)


Lệnh delete: chúng ta có thể xóa dữ liệu,  xóa  database


![image](https://user-images.githubusercontent.com/62273292/161218447-54a2a0d1-5d1f-46a9-a79f-650fd035ce3d.png)


![image](https://user-images.githubusercontent.com/62273292/161218502-bc3ddcd1-0e9b-4518-ba27-f237a2a0a1ab.png)


![image](https://user-images.githubusercontent.com/62273292/161220943-af6f74bb-4b42-4e89-8e8a-7384c3b2e773.png)

![image](https://user-images.githubusercontent.com/62273292/161221065-52c29556-3e8d-4ba9-9f93-8d0021fa7ca5.png)























      
      
