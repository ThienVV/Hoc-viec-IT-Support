# Danh sách lệnh command line quản lý dịch vụ tường lửa CSF

![image](https://user-images.githubusercontent.com/62273292/166857598-bdd1e75f-5abc-44cd-9a9e-a0da30dde8da.png)

![image](https://user-images.githubusercontent.com/62273292/166857505-503f13cb-a84f-4a8d-b7e6-261af66776c4.png)

![image](https://user-images.githubusercontent.com/62273292/166857557-109fc67e-aadb-4b63-94bb-f30be23f90da.png)


1. Khởi động “csf” và “lfd” nếu chưa khởi động

```
# csf -e
# csf --enable
```
![image](https://user-images.githubusercontent.com/62273292/166857744-6b7001e9-9b32-4cd3-90cf-a66ebe757d00.png)

![image](https://user-images.githubusercontent.com/62273292/166858090-ba6266f6-a146-4b5b-8c9d-a77da9440ac2.png)

Sau khi tắt và bật lại

![image](https://user-images.githubusercontent.com/62273292/166857954-e1d84a72-bed4-4439-bf2f-7d98929ed143.png)

![image](https://user-images.githubusercontent.com/62273292/166858056-a7013f59-c965-4a78-b80c-27260ec3740d.png)

![image](https://user-images.githubusercontent.com/62273292/166858112-56ab8296-97f7-45cb-ba3e-6609427b5633.png)

2. Tắt “csf” và “lfd”

```
# csf -x
# csf --disable
```

![image](https://user-images.githubusercontent.com/62273292/166857809-50752af2-33a3-4df9-bf3c-4a63bed7ce30.png)

![image](https://user-images.githubusercontent.com/62273292/166857862-360d66c8-04ef-411a-82bb-a4dd0d9cbd84.png)


3. Khởi động lại các rule tường lửa

```
# csf -r
# csf --restart
```

![image](https://user-images.githubusercontent.com/62273292/166858241-8283b596-d23e-437e-bfd8-5563fc7f5c0a.png)

![image](https://user-images.githubusercontent.com/62273292/166858260-ae73ea86-d41c-4f7f-b04d-7e95694324a3.png)

![image](https://user-images.githubusercontent.com/62273292/166860663-6eea11a4-00ff-4ad8-9012-e83a7ab431be.png)

![image](https://user-images.githubusercontent.com/62273292/166860719-b28f2690-9676-42af-ba16-87b8d3a22fd4.png)

![image](https://user-images.githubusercontent.com/62273292/166860736-f310aef1-d9aa-426d-99d2-b0a12699579f.png)


4. Khởi động rule tường lửa

```
# csf -s
# csf --start
```

![image](https://user-images.githubusercontent.com/62273292/166860826-b746d306-2528-47d2-a81e-80b2b7de476c.png)

5. Xoá toàn bộ rule tường lửa

```
# csf -f
# csf --stop
```

6. Liệt kê cấu hình rule IPv4 Iptables

```
# csf -l
# csf --status
```
![image](https://user-images.githubusercontent.com/62273292/166861952-e086464b-f62d-45c4-b05d-e0ce174e8f24.png)

![image](https://user-images.githubusercontent.com/62273292/166864472-fbf89ad6-f04f-4c9a-9966-31b33a868745.png)


7. Liệt kê cấu hình rule IPv6 Iptables

```
# csf -l6
# csf --status6
```
![image](https://user-images.githubusercontent.com/62273292/166864538-33357a53-3e4e-4727-b054-8296d869a5a4.png)


8. Cho phép (allow) 1 IP và thêm IP đó vào file /etc/csf/csf.allow

```
# csf -a ip [comment]
# csf --add ip [comment]
```

![image](https://user-images.githubusercontent.com/62273292/166864798-b3d5f8cc-e2a5-4a33-9482-0fa8640b1601.png)

![image](https://user-images.githubusercontent.com/62273292/166864901-6426183c-f2e0-4bd1-9724-410a9556a033.png)


Ví dụ :

```
# csf -d 192.168.1.110 DDOS IP
Adding 192.168.1.110 to csf.deny and iptables DROP...
```

![image](https://user-images.githubusercontent.com/62273292/166864985-f4ca9f79-3c32-445c-9de6-254b5d2518ee.png)


9. Gỡ bỏ IP khỏi danh sách cho phép, bỏ IP đó khỏi file /etc/csf/csf.allow

```
# csf -ar ip
# csf --addrm ip
```

![image](https://user-images.githubusercontent.com/62273292/166865317-b121c1cc-8107-4f16-8f28-2fa0bc8e3711.png)

![image](https://user-images.githubusercontent.com/62273292/166865341-05fb275e-f098-452f-9a97-0467f5f428ca.png)


10. Chặn (deny) 1 IP và thêm IP đó vào file /etc/csf/csf.deny

```
# csf -d ip [comment]
# csf --deny ip [comment]
Ví dụ :
# csf -d 192.168.1.110 DDOS IP
Adding 192.168.1.110 to csf.deny and iptables DROP...
```

11. Chặn 1 IP vĩnh viễn không bị xoá khỏi danh sách IP trong /etc/csf/csf.deny


– Số lượng IP chặn cũng như số lượng IP entry có thể chứa trong file /etc/csf/csf.deny được quy định bởi cấu hình giá trị “DENY_IP_LIMIT” trong /etc/csf/csf.conf. Nên khi số lượng IP bị deny đạt ngưỡng này thì CSF sẽ tuần tự xoá các IP cũ nhất khỏi danh sách IP bị chặn để thêm 1 IP mới vào danh sách chặn.
– Trong trường hợp đó ta muốn 1 IP đã thêm vào danh sách chặn sẽ không bị CSF gỡ bỏ để phục vụ nhu cầu lấy khoảng trống cho IP mới bị chặn, thì ta sẽ thêm dòng comment “do not delete” khi gõ lệnh chặn IP.

```
# csf -d ip do not delete
# csf --deny ip do not delete
```

12. Gỡ bỏ IP khỏi danh sách bị chặn, bỏ IP đó khỏi file /etc/csf/csf.deny

```
# csf -dr ip
# csf --denyrm ip
```

13. Xoá toàn bộ các IP bị chặn cũng như là xoá bộ IP thông tin trong file /etc/csf/csf.deny

```
# csf -df
# csf --denyf
```

14. Tìm thông tin về IP trong danh sách rule tường lửa chặn

– Áp dụng cho cả việc tìm kiếm trong các rule IPv4 và IPv6, giúp xác định IP cần kiểm tra có bị chặn tạm thời, chặn vĩnh viễn hay đang được cho phép như thế nào.

```
# csf -g ip
```
Ví dụ :
![image](https://user-images.githubusercontent.com/62273292/166865499-8e9a6590-08c6-430d-8667-81a81a76aba7.png)

15. Thêm IP vào danh sách IP tạm thời được cho phép

```
# csf -ta ip ttl [-p port] [-d direction] [comment]
# csf --tempallow ip ttl [-p port] [-d direction] [comment]
Ví dụ :
# csf -ta 192.168.1.100
ACCEPT  all opt -- in !lo out *  192.168.1.100  -> 0.0.0.0/0
ACCEPT  all opt -- in * out !lo  0.0.0.0/0  -> 192.168.1.100
csf: 192.168.1.100 allowed on port * for 3600 seconds in and outbound
```

16. Thêm IP vào danh sách IP tạm thời bị chặn

```
# csf -td ip ttl [-p port] [-d direction] [comment]
# csf --tempdeny ip ttl [-p port] [-d direction] [comment]
Ví dụ :
# csf -td 192.168.1.100
DROP  all opt -- in !lo out *  192.168.1.100  -> 0.0.0.0/0
csf: 192.168.1.100 blocked on port * for 3600 seconds inbound
```

17. Liệt kê các IP đang nằm trong danh sách IP tạm thời bị chặn hoặc tạm thời cho phép

```
# csf -t 
# csf --temp
Ví dụ :
# csf -t
A/D   IP address                               Port   Dir   Time To Live     Comment
DENY  192.168.1.100                              *    in    59m 48s          Manually added: 192.168.1.100 (-/-/-)
ALLOW 192.168.1.110                              *    inout 59m 56s          Manually added: 192.168.1.110 (-/-/-)
```

18. Gỡ bỏ IP khỏi danh sách IP tạm thời bị chặn hoặc tạm thời cho phép

```
# csf -tr ip
# csf -temprm ip
```

19. Xoá toàn bộ danh sách IP đang nằm trong danh sách tạm thời

```
# csf -tf
# csf --tempf
```

Một số lệnh CSF khác

20. Xem phiên bản CSF hiện tại trên hệ thống

```
# csf -v
# csf --version
```

21. Kiểm tra phiên bản cập nhật, nhưng không tiến hành cập nhật

```
# csf -c
# csf --check
```

22. Danh sách các options hỗ trợ

```
# csf -h
# csf --help
```


Link tham khảo https://cuongquach.com/danh-sach-lenh-command-line-quan-ly-dich-vu-tuong-lua-csf.html




































