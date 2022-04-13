# File server là gì?

File server (hay máy chủ tập tin) là một máy tính nối mạng cung cấp không gian để lưu trữ và chia sẻ dữ liệu như văn bản, hình ảnh, âm thanh, video. Các dữ liệu này có thể được truy cập bởi các workstation (máy trạm). Workstation này có thể kết nối được tới máy chủ khi các máy này chia sẻ quyền truy cập thông qua một mạng máy tính.

File server là gì? Các kiểu file server, cấu trúc file server  

Trong lược đồ máy khách - máy chủ (client – server), các máy khách chính là các máy trạm sử dụng storage. Thông thường, một file server sẽ không thực hiện các nhiệm vụ máy tính và cũng không chạy các chương trình thay cho các client. Khi cấu hình máy chủ File server chủ yếu chỉ thiết lập cho lưu trữ và truy xuất dữ liệu trong khi nhiệm vụ tính toán được thực hiện bởi các workstation.




## Các kiểu File server

Một file server có thể là máy chủ chuyên dụng hoặc không chuyên dụng. Một máy chủ chuyên dụng sẽ được thiết kế đặc biệt để sử dụng như một file server với các máy trạm được kết nối để đọc, ghi các tập tin và cơ sở dữ liệu.

File server cũng có thể được phân loại theo phương thức truy cập:

- FTP: File Transfer Protocol

- HTTP: Hypertext Transfer Protocol

- SMB: Server Message Block / CIFC – Common In File System – Windows hoặc UNIX mà thường là cho UNIX

- NFS: Network File System – Chủ yếu là cho UNIX, hệ thống tương tự UNIX

Database servers, cung cấp quyền truy cập vào shared database thông qua 1 driver, và không được coi là file server vì chúng có thể yêu cầu Record locking.

banner test
Cloud Server - Giải pháp đám mây giúp vận hành website ổn định, nhanh chóng


Cấu trúc của file server

**Storage**

Vì chức năng quan trọng nhất trong file server là storage, nên hiện nay đã có các công nghệ được phát triển cho phép vận hành nhiều ổ đĩa theo nhóm, hình thành một disk array. 1 disk array điển hình sẽ chứa cache (bộ nhớ tạm thời có tốc độ nhanh hơn magnetic disk), cũng như các chức năng tiên tiến hơn như RAID hay ảo hóa lưu trữ. Bên cạnh đó, disk array cũng giúp nâng cao độ sẵn sàng nhờ các yếu tố dự phòng khác ngoài RAID như nguồn điện. Các disk array có thể được hợp nhất hoặc ảo hóa trong môi trường SAN.



Network-attached storage (NAS)

Network-attached storage (NAS) là máy tính lưu trữ dữ liệu cấp độ tệp tin được kết nối với mạng máy tính cho phép truy cập dữ liệu trên một nhóm máy khách không đồng nhất. NAS device – thiết bị lưu trữ gắn vào mạng (phân biệt với file server trong mạng NAS) là một thiết bị/máy tính chuyên dụng chỉ dùng để serve các tập tin thay vì dùng cho các mục đích chung.


Cho đến năm 2010, các thiết bị NAS đã dần trở nên phổ biến nhờ mang đến một phương thức tiện lợi để chia sẻ tệp giữa nhiều máy tính. Lợi ích của NAS so với các file server không chuyên dụng, bao gồm các tính năng như truy cập dữ liệu nhanh hơn, quản trị dễ dàng hơn và cấu hình đơn giản hơn.


Hệ thống NAS là các thiết bị nối mạng với 1 hay nhiều ổ cứng, thường được sắp xếp thành các storage container dự phòng hoặc các RAID array. Network Attached Storage loại bỏ việc phân phát tệp từ các máy chủ khác trên mạng. NAS thường cấp quyền truy cập files sử dụng các giao thức chia sẻ file qua mạng như NFS, SMB/CIFS (Server Message Block/Common Internet File System) hoặc AFP.

banner test
Cloud Server - Giải pháp đám mây giúp vận hành website ổn định, nhanh chóng


Bảo mật
Việc xây dựng hệ thống File server thường hỗ trợ một vài hình thức bảo mật hệ thống nhằm hạn chế quyền truy cập đối với người dùng hoặc nhóm người dùng cụ thể.

Trong các tổ chức lớn, nhiệm vụ này thường được phân cấp cho các directory service như openLDAP, eDirectory của Novell hoặc Active Directory của Microsoft.

Các server này hoạt động trong môi trường máy tính phân tầng; xử lý user, máy tính, ứng dụng và file như các thành phần riêng biệt nhưng có liên quan đến nhau trên mạng; cấp quyền truy cập thông qua xác thực người dùng hoặc nhóm người dùng.


## Các hình thức file server

Nói đến chia sẻ dữ liệu tập trung hay còn gọi là file server thì chúng ta có nhiều hình thái khác nhau như :

+ Xây dựng máy chủ chạy trên nền tảng Linux or Windows Server

+ Hệ thống NAS

+ Giải pháp SAN










