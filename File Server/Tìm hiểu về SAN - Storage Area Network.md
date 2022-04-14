# 

## Định nghĩa SAN

Lưu trữ mạng có thể được hiểu như một phương pháp truy cập dữ liệu ứng dụng trên nền tảng mạng mà quá trình truyền dữ liệu trên mạng tương tự như quá trình truyền dữ liệu từ các thiết bị quen thuộc trên máy chủ như Disks Drivers như ATA, SCSI.

Trong một mạng lưu trữ, một máy chủ sử dụng một yêu cầu cho một gói dữ liệu cụ thể hay một dữ liệu cụ thể, từ một đĩa lưu trữ và các yêu cầu được đáp ứng. Phương pháp này được biết là block storage. Các thiết bị được làm việc như một thiết bị lưu trữ bên trong máy chủ và được truy cập một cách bình thường thông qua các yêu cầu cụ thể và quá trình đáp ứng bằng cách gửi các yêu cầu và nhận được trên môi trường mạng mà thôi.

Theo truyền thống phương pháp truy cập vào file như SMB/CIFS hay NFS, một máy chủ sử dụng các yêu cầu cho một file như một thành phần của hệ thống file trên máy, và được quản lý bình thường với máy chủ. Quá trình điều khiển đó được quyết định từ tầng vật lý của dữ liệu, truy cập vào nó như một ổ đĩa bên trong máy chủ và được điều khiển và sử dụng trực tiếp trên máy chủ. Chỉ khác một điều dữ liệu bình thường thông qua hệ thống bus còn SAN dựa trên nền mạng. Các hệ thống lưu trữ mạng sử dụng giao thức SCSI cho quá trình truyền dữ liệu từ máy chủ đến các thiết bị lưu trữ, không thông qua các Bus hệ thống. Cụ thể tầng vật lý của SAN được sử dụng dựa trên các cổng quang để truyền dữ liệu: 1 Gbit Fiber Channel, 2Gbit Fiber Channel, 4Gbit Fiber Channel, và 1Gbit iSCSI. Giao thức SCSI thông tin được vận truyển trên một giao thức thấp dựa trên quá trình mapping layer. Hầu hết các hệ thống SANs hiện hay đều sử dụng SCSI dựa trên hệ thống cáp quang để truyền dữ liệu và quá trình chuyển đội (mapping layer) từ SCSI qua cáp quang và máy chủ vẫn hiểu như SCSI là (SCSI over Fiber Channel) và FCP được coi là một chuẩn trong quá trình chuyển đổi đó. iSCSI là một dạng truyển đổi tương tự với phương pháp thiết kế mang các thông tin SCSI trên nền IP

## Lợi ích khi sử dụng SAN

Dễ dàng chia sẻ lưu trữ và quản lý thông tin, mở rộng lưu trữ dễ dàng thông qua quá trình thêm các thiết bị lưu trữ vào mạng không cần phải thay đổi các thiết bị như máy chủ hay các thiết bị lưu trữ hiện có. Ứng dụng cho các hệ thống Data centrer và các Cluster. Và mỗi thiết bị lưu trữ trong mạng SAN được quản lý bởi một máy chủ cụ thể. Trong quá trình quản lý của SAN sử dụng Network Attached Storage (NAS) cho phép nhiều máy tính truy cập vào cùng một file trên một mạng. Và ngày nay có thể tích hợp giữa SAN và NAS tạo nên một hệ thống lưu trữ thông tin hoàn thiện.

SANs được thiết kế dễ dàng cho tận dụng các tính năng lưu trữ, cho phép nhiều máy chủ cùng chia sẻ một thiết bị lưu trữ.

Một ứng dụng khác của SAN là khả năng cho phép máy tính khởi động trực tiếp từ SAN mà chúng quản lý. Điều này cho phép dễ dàng thay các máy chủ bị lỗi khi đang sử dụng và có thể cấu hình lại cho phép thay đổi hay nâng cấp máy chủ một cách dễ dàng và dữ liệu không hề ảnh hưởng khi máy chủ bị lỗi. Và quá trình đó có thể chỉ cần nửa giờ để có một hệ thống Data Centers. Và được thiết kế với tốc độ truyền dữ liệu cực lớn và độ an toàn của hệ thống được coi là vấn đề hàng đầu.

SAN cung cấp giải pháp khôi phục dữ liệu một cách nhanh chóng bằng cách thêm và các thiết bị lưu trữ và có khả năng khôi phục cực nhanh dữ liệu khi một thiết bị lưu trữ bị lỗi hay không truy cập được (secondary aray).

Các hệ thống SAN mới hiện nay cho phép (duplication) sao chép hay một tập tin được ghi tại hai vùng vật lý khác nhau (clone) cho phép khôi phục dữ liêu cực nhanh.

## Tính năng:

Lưu trữ được truy cập theo Block qua SCSI

Khả năng I/O với tốc độ cao

Tách biệt thiết bị lưu trữ và Server

Dễ dàng chia sẻ lưu trữ và quản lý thông tin.

Mở rộng lưu trữ dễ dàng thông qua quá trình thêm các thiết bị lưu trữ vào mạng không cần phải thay đổi các thiết bị như máy chủ hay các thiết bị lưu trữ hiện có.

Cho phép nhiều máy chủ cùng chia sẻ một thiết bị lưu trữ.

Cho phép thay đổi hay nâng cấp máy chủ một cách dễ dàng và dữ liệu không hề ảnh hưởng khi máy chủ bị lỗi.

## Điều khiển đĩa

Quá trình điều khiển cho SAN trong môi trường doanh nghiệp với sự phát triển nhanh chóng yêu cầu sự đáp ứng về truyền dữ liệu với tốc độ cực cao tới các ổ đĩa (như các dữ liệu truyền từ các hệ thống mail servers, máy chủ dữ liệu, và các máy chủ file server). Trong quá trình phát triển trước kia, với mạng doanh nghiệp dùng hệ thốg lưu trữ với khả năng đáp ứng cao sử dụng lưu trữ SCSI và RAIDs điều khiển các mảng đĩa cứng được tích hợp trực tiếp trên máy chủ. Và bây giờ với công nghệ Mạng trên nền tảng IP, và khi các ứng dụng dữ liệu sử dụng hết toàn bộ các ổ lưu trữ trên các máy chủ và các người dùng cuối yêu cầu phải thay máy chủ đáp ứng các yêu cầu công việc. Nhưng với SAN việc nâng cấp các thiết bị lưu trữ là rất đơn giản với việc thêm vào mạng các thiết bị lưu trữ mới.

Điều khiển đĩa sử dụng trong môi trường SAN được thiết kế cung cấp với tốc độ cao, độ tin cậy lớn “Visual Hard Driver” (hay LUNs). Thêm nữa mô hình SANs cho phép tích hợp lẫn các thiết bị FC SATA và FC SCSI (FC SATA là thiết bị lưu trữ sử dụng các ổ đĩa dạng SATA và sử dụng cáp quang để truyền dữ liệu tới môi trường mạng). SATA làm việc với khả năng thấp, có nhiều lỗi xảy ra nhưng lưu trữ lớn và giá thành rẻ hơn rất nhiều so với các ổ đĩa SCSI. Nó cho phép các mạng SANs sử dụng nó để như một thiết bị sao lưu dự phòng khi có lỗi xảy ra. Và hâu hết các SAN đều dử dụng FC SATA như một thiết bị backup với lưu trữ lớn và tốc độ nhanh hơn rất nhiều so với tape drivers.

## Các dạng SANs

SANs được xây dựng với thiết kế dành riêng cho việc lưu trữ và truyền thông tin. Nó cung cấp khả năng truyền dữ liệu với tốc độ lớn với độ an toàn cao hơn các giao thức khác như NAS. Hầu hết các công nghệ SAN là mạng cáp quang (Fiber Channel Networking) với các thiết bị lưu trữ sử dụng các ổ địa SCSI. Một dạng cụ thể là FiBre Channel SAN được xây dựng bởi Fibre Channel Switch được kết nối tới các thiết bị thông qua hệ thống cab quang. Ngày nay hầu hết các hệ thống SAN đều sử dụng giải pháp định tuyến Fibre Channel, và mang lại khả năng mở rộng lớn cho cấu trúc SAN cho phép kết hợp các hệ thống SAN lại với nhau. Tuy nhiên hầu hết quá trình đó đều với mục đích dữ liệu tập trung và truyền với tốc độ cực cao với khoảng cách xa hơn thông tầng vật lý là cáp quang, switch quang.

Một dạng khác của SAN là sử dụng giao thức iSCSI nó sử dụng giao thức SCSI trên nền tảng TCP/IP. Trong dạng này, các switch tương tự như Ethernet Switchs. Chuẩn iSCSI được giới thiệu năm 2003 và được triển khai rộng lớn trong quá trình lưu trữ mạng (lưu trữ không yêu cầu tốc độ lớn) và từ khi ứng dụng cáp quang trong quá trình truyền dữ liệu mang lại hiệu năng lớn cho iSCSI. Ngày nay hầu hết các hệ thống isSCSI sử dụng cáp quang trong quá trình truyền dữ liệu và sử dụng giao thức NAS như CIFS và NFS.

Một dạng khác của iSCSI là ATA-over-Ethernet hay giao thức AoE được xây dựng sử dụng giao thức ATA trên khung nền tảng Ethernet. Trong khi giao thức Ethernet như AoE không thể định tuyến và cung cấp các hiệu năng khác nhau.

Kết nối với SAN sẽ có một hay nhiều máy chủ và một hay nhiều các thiết bị lưu trữ khác nhau. Trong FC SAN máy chủ cũng sử dụng cáp quang để truyền dữ liệu (host bus adapter and Optical fibre). isSCSI SAN sử dụng giao thức Ethernet bình thường thông qua card mạng hay TOE card. SAN có hai dạng là: Centralized storage are networks và distributed storage area network.

## SAN trong môi trường làm việc

SAN được sử dụng trong môi trường yêu cầu mở rộng nhanh chóng các thiết bị lưu trữ, và yêu cầu đáp ứng công việc cao (truyền dữ liệu với tốc độ lớn). Nó cho phép các thiết bị FC disk driver kết nối trực tiếp đến SAN. SAN như các mạng bình thường của các thiết bị lưu trữ với dung lượng lớn. SAN là giải pháp đắt tiền với hệ thống Fibre Channel hay các card chuyên dụng cho các máy tính. Côn nghệ iSCSI SAN là giải pháp đáp ứng được với yêu cầu giá cả của SAN, nhưng không như công nghệ sử dụng cho mạng doanh nghiệp lớn Data Center. Các máy con có thể sử dụng giao thức NAS như CIFS hay NFS. Với khả năng truy cập từ xa và khôi phục dữ liệu nhanh chóng khi xảy ra lỗi. Đáp ứng tốt cho giải pháp Data Center. Và khả năng của iSCSI đáp ứng với các môi trường ứng dụng không đòi hỏi khả năng đáp ứng cực lớn. Với FC SAN đáp ứng các yêu cầu khắt khe nhất về ứng dụng.

## SAN trong ứng dụng ngày nay

Trong quá trình phát triển nhanh chóng các dữ liệu của doanh nghiệp hay tổ chức vừa và nhỏ đều yêu cầu có một thiết bị lưu trữ với dung lượng lớn và độ an toàn thông tin cao và SAN là một giải pháp đáp ứng các yêu cầu khắt khe nhất của doanh nghiệp.

Với tốc độ truyền dữ liệu từ 300Mbit/s đến 4Gbit/s sẽ đáp ứng được các ứng dụng về ghi và cung cấp dữ liệu cho nhu cầu hiện nay và trong tương lai

## iSCSI SAN là gì ?

iSCSI là Internet SCSI ( Small Computer System Interface ) là một chuẩn công nghiệp phát triển để cho phép truyền tải các lệnh SCSI qua mạng IP hiện có bằng cách sử dụng giao thức TCP/IP.

Các thiết bị iSCSI SAN (hay IP SAN) là các Server (chạy HĐH nào đó, Win Storage chẳng hạn) và có cài tính năng hỗ trợ iSCSI ở phía server (gọi là iSCSI target). Các máy truy cập đến thiết bị IP SAN bằng iSCSI sẽ phải hỗ trợ tính năng iSCSI client (gọi là iSCSI source). iSCSI source (client) được cài sẵn trong Win Vista/7 và 2008. Đối với iSCSI target, có nhiều Soft, ví dụ StarWind trên nền Win, và OpenFiler trên nền Linux.

iSCSI dễ dùng, linh hoạt, dễ mở rộng, vì hoạt động dựa trên nền IP và Ethernet / Internet, không đòi hỏi phần cứng đặc biệt. Đặc biệt hiệu quả khi mạng Ethernet 10G phổ biến.

Nếu như giao thức iSCSI hoạt động trên nền IP, và từ lớp Internet trở lên, thì giao thức Fiber Channel (1 loại SAN khác) hoạt động ở mức Physical layer, nên phụ thuộc nhiều vào phần cứng, cần đến phần cứng riêng biệt, bao gồm các Switch, NIC (HBA) và thiết bị lưu trữ/cáp hỗ trợ Fiber channel. Vì không hoạt động trên nền IP nên không linh động và khó mở rộng, so với IP SAN. Dù khó dùng và đắt tiền, Fiber Channel SAN đã và đang là giải pháp SAN chính của nhiều hệ thống lớn.

Storage Area Network (SAN) là một mạng được thiết kế cho việc thêm các thiết bị lưu trữ cho máy chủ một cách dễ dàng như: Disk Aray Controllers, hay Tape Libraries

Với những ưu điểm nổi chội SANs đã trở thành một giải pháp rất tốt cho lưu trữ thông tin cho doanh nghiệp hay tổ chức. SAN cho phép kết nối từ xa tới các thiết bị lưu trữ trên mạng như: Disks và Tape drivers. Các thiết bị lưu trữ trên mạng, hay các ứng dụng chạy trên đó được thể hiện trên máy chủ như một thiết bị của máy chủ (as locally attached divices)

## Có hai sự khác nhau cơ bản trong các thành phần của SANs

1. Mạng (network) có tác dụng truyền thông tin giữa thiết bị lưu trữ và hệ thống máy tính. Một SAN bao gồm một cấu trúc truyền tin, nó cung cấp kết nối vật lý, và quản lý các lớp, tổ chức các kết nối, các thiết bị lưu trữ, và hệ thống máy tính sao cho dữ liệu truyền trên đó với tốc độ cao và tính bảo mật. Giới hạn của SAN thường được nhận biết với dịch vụ Block I/O đúng hơn là với dịch vụ File Access.

2. Một hệ thống lưu trữ bao gồm các thiết bị lưu trữ, hệ thống máy tính, hay các ứng dụng chạy trên nó, và một phần rất quan trọng là các phần mềm điều khiển, quá trình truyền thông tin qua mạng

## GIẢI PHÁP LƯU TRỮ - SAN

SAN (Storage Area Network) là một mạng quang riêng tốc độ cao dùng cho việc truyền dữ liệu giữa các máy chủ tham gia vào hệ thống lưu trữ cũng như giữa các thiết bị lưu trữ với nhau. SAN cho phép thực hiện quản lý tập trung và cung cấp khả năng chia sẻ dữ liệu và tài nguyên lưu trữ. Hầu hết mạng SAN hiện nay dựa trên công nghệ kênh cáp quang, cung cấp cho người sử dụng khả năng mở rộng, hiệu năng và tính sẵn sàng cao.

Hệ thống SAN được chia làm hai mức: mức vật lý và logic

Mức vật lý: mô tả sự liên kết các thành phần của mạng tạo ra một hệ thống lưu trữ đồng nhất và có thể sử dụng đồng thời cho nhiều ứng dụng và người dùng.

Mức logic: bao gồm các ứng dụng, các công cụ quản lý và dịch vụ được xây dựng trên nền tảng của các thiết bị lớp vật lý, cung cấp khả năng quản lý hệ thống SAN.

![image](https://user-images.githubusercontent.com/62273292/163315486-c333b53f-a26c-4f17-9c2b-cb0c493ba83d.png)

Ưu điểm của hệ thống SAN

Có khả năng sao lưu dữ liệu với dung lượng lớn và thường xuyên mà không làm ảnh hưởng đến lưu lượng thông tin trên mạng.

SAN đặc biệt thích hợp với các ứng dụng cần tốc độ và độ trễ nhỏ.

Dữ liệu luôn ở mức độ sẵn sàng cao.

Dữ liệu được lưu trữ thống nhất, tập trung và có khả năng quản lý cao. Có khả năng khôi phục dữ liệu nếu có xảy ra sự cố.

Hỗ trợ nhiều giao thức, chuẩn lưu trữ khác nhau như: iSCSI, FCIP, DWDM...

Có khả năng mở rộng tốt trên cả phương diện số lượng thiết bị, dung lượng hệ thống cũng như khoảng cách vật lý.






















