# Cài đặt và mở File Server Resource Manager trong

## Cách cài đặt File Server Resource Manager

Bước 1 - Vào Server Manager > Manage > Add Roles and Features > Next. Chọn Role-based or feature-based installation, rồi chọn Select a server from the server pool. Bấm Next.

Sau đó, tại danh sách, tìm File and Storage Services và mở rộng nó. Sau đó, mở rộng Files and iSCSI Services, chọn File Server Resource Manager và sau đó một cửa sổ sẽ mở ra.

Bước 2 - Nhấp vào Add features và sau đó bấm Next.

Nhấp vào nút Install.

## Cách mở File Server Resource Manager

Bước 1 - Nhấp vào Server Manager > Tools > File Server Resource Manager

![image](https://user-images.githubusercontent.com/62273292/163294277-9d3d07f5-1772-44dd-9b66-d5a34b133b1a.png)

Bước 2 - Trên bảng điều khiển bên trái nhấp vào Quota Management, rồi mở rộng phần Create Quota Template, sao đó nhấp vào Create Quota Template… trên bảng điều khiển bên phải như được hiển thị trong ảnh chụp màn hình bên dưới.

Bước 3 - Một bảng mới sẽ được mở ra, trong đó khía cạnh quan trọng nhất cần đặt là Space Limit, tùy theo nhu cầu của bạn. Ở đây, ví dụ này sẽ đặt 2GB và sau đó bấm OK.

![image](https://user-images.githubusercontent.com/62273292/163294544-1e7fa81b-7460-4f7e-9f5f-aa6030d77950.png)

![image](https://user-images.githubusercontent.com/62273292/163294835-f031b9e0-4861-4dd8-8613-3c142f6d1ca4.png)


Bước 4 - Bạn phải đặt một định mức định cho nó và một khi thư mục đạt đến định mức đó, nó sẽ gửi cho bạn một thông báo về nơi bạn sẽ có tùy chọn để đặt email.

![image](https://user-images.githubusercontent.com/62273292/163295666-9dd672d2-ef25-4673-854f-7585e6e0bed1.png)

Bước 5 - Nhấp vào Ok.

Bước 6 - Sau đó, để đính kèm định mức này vào một thư mục, nhấp chuột phải vào template rồi kích vào Create Quota from Template…

![image](https://user-images.githubusercontent.com/62273292/163295823-b698df11-ac37-4edf-991b-7828b58e1885.png)

Bước 7 - Nhấn vào Browse… và sau đó chọn thư mục của bạn. Bấm Create.

![image](https://user-images.githubusercontent.com/62273292/163295966-22a42393-e77a-4567-9f19-c6716c722f34.png)

Bước 8 - Để đặt hạn chế cho các thư mục của bạn, bạn có thể chuyển đến cửa sổ bên trái File Screening Management > File screening templates, rồi nhấp vào bảng điều khiển bên trái Create File Screen Template…

![image](https://user-images.githubusercontent.com/62273292/163296705-619c03f2-ebc1-45db-8c5a-52e02e0d43d0.png)

Bước 9 - Nhấp vào Browse… và tìm thư mục bạn muốn chọn. Cuối cùng hãy bấm Create.

![image](https://user-images.githubusercontent.com/62273292/163302301-9c29f703-ad1f-45e9-8260-ab33fcf866d2.png)





























