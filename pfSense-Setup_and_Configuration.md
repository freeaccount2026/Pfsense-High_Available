1. CÀI ĐẶT VÀ CẤU HÌNH PFSENSE 2.7.2
1.1 tải file cài đặt ISO
1.2 Cài pfsense
1.3 Cấu hình ban đầu trên console
1.3.1 Cài IP tĩnh
   - Chọn 2
   - chọn Adapter LAN
   - DHCP : n
   - IP: 192.168.10.1
   - Subnet: 24
   - gateway upstream: bỏ qua
   - IP v6: bỏ qua
   - DHCP trên LAN: bỏ qua
   - HTTP: y
2. Truy cập Dashboard của pfsense
2.1 chạy 1 máy ảo khác trên VMnet2(cổng LAN) thiết lập IP cùng dãy và Default Gateway là IP LAN của Pfsense
<img width="888" height="596" alt="image" src="https://github.com/user-attachments/assets/532fead3-401b-4650-99d0-2daf67219217" />
- Ở đây mình dùng window 11 <br>
<img width="1023" height="815" alt="image" src="https://github.com/user-attachments/assets/366ecddc-9cfb-4a99-9f45-a6e79d26328e" /> <br>
-Thiết lập IP và default
<img width="1069" height="821" alt="image" src="https://github.com/user-attachments/assets/3bec5a53-5464-49f5-92cc-f75a8c9e5777" />
2.2 Đăng nhập
  Mặc định: admin/pfsense
- Mục General information: nhập primary dns - mình dùng 8.8.8.8
- Mục Time server: để mặc định
- Mục configure wan intf: tắt Block private network và Block non-internet routed vì mình đang dùng ip nội bộ
- Mục configure lan int để mặc định vì mình đã cấu hình lan rồi
2.3 Kiểm tra kết nối trên pfsense
- chọn Diagnostics -> ping
- Kiểm tra từ wan <br>
<img width="964" height="419" alt="image" src="https://github.com/user-attachments/assets/ae19665e-053c-4ade-9f03-c52be9b3dfa7" /><br>
- Kiểm tra từ lan <br>
<img width="971" height="626" alt="image" src="https://github.com/user-attachments/assets/01fe17a3-711f-45da-a5f1-fb0afbdfbcef" /> <br>
2.4 Cấu hình DNS Forwarded
  - Máy Management không ping được internet (do dùng DNS là IP của LAN)
    Vào cmd
    ping google.com: could not find
    ping 8.8.8.8: được
    => lỗi do DNS (do chức năng DNS Resolever trên pfsense) 

   -  Tắt tính năng DNS resolever (DNS resolever tự truy vấn root server thay vì hỏi DNS khác
    Trên pfsense: services -> DNS Resolver -> Tắt
<img width="955" height="616" alt="image" src="https://github.com/user-attachments/assets/7f57b878-1d89-4a26-9e33-3743c94bcbe1" />

   -  Bật tính năng DNS Forwarder
<img width="1021" height="652" alt="image" src="https://github.com/user-attachments/assets/44e2c5a9-7eb7-4614-bf6e-47402b6b99b2" />
   - Ping gg
<img width="771" height="182" alt="image" src="https://github.com/user-attachments/assets/8c3c5b16-5568-4dc3-a511-f0708c87b6c3" />
2.5 Cấu hình lớp mạng cho DMZ
   - DMZ(Demilitarized Zone) là gì?
Vùng mạng trung gian nằm giữa, vùng server public để cô lập các server, server truy cập được internet nhưng internet không truy cập trực tiếp dc mạng nội bộ
2.5.1 Cấu hình lớp mạng cho DMZ
     - Interface -> Assignments
     - Add em2: đây là VMnet 3
<img width="1007" height="717" alt="image" src="https://github.com/user-attachments/assets/bad87656-08cf-448f-aee3-bc0c23274a69" />
     - Chỉnh sửa OPT1
<img width="962" height="641" alt="image" src="https://github.com/user-attachments/assets/8ac22507-6b25-4bca-bd1f-08eae382a113" />

<img width="954" height="243" alt="image" src="https://github.com/user-attachments/assets/d994ab4b-9bbd-4de5-9224-7cf178eb7cfd" />
     - Kiểm tra trong pfsense sẽ thấy có thêm DMZ
<img width="818" height="966" alt="image" src="https://github.com/user-attachments/assets/e76e6adb-7a89-47a0-86f7-9375bf9dffbf" />
2.5.2 Cấu hình Firewall rules cho DMZ

     - 
3. 
    
