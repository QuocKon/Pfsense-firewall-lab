# 🧪 Lab Guide – Pfsense Firewall Lab

## Mục tiêu
- Xây dựng mô hình mạng doanh nghiệp gồm 2 subnet **Internal** và **External**.
- Cài đặt và cấu hình **pfSense Firewall**.
- Kiểm tra kết nối, triển khai **firewall rule** và **port forwarding**.

---

## Chuẩn bị môi trường
- **Phần mềm:** VMware Workstation / VirtualBox  
- **Máy ảo sử dụng:**
  - pfSense Firewall
  - Kali Linux (Internal & External)
  - Windows Server (Internal & External)
  - Ubuntu (Internal)

---


 ## Cấu hình Topo mạng
 Tạo thêm 2 Subnet trên Vmware vmnet11 có địa chỉ 10.10.19.0/24 cho mạng External và vmnet10 có địa chỉ 192.168.100.0/24 cho mạng Internal.
 
 ![img](images/Picture1.png)

 ## Cấu hình địa chỉ IP cho các máy
  - Mạng Internal
   Cấu hình IP tĩnh cho máy Kali Attank Internal
 
 ![img](images/Picture2.png)


 Cấu hình máy Windows Server Internal. IP :192.168.100.201
 
 ![img](images/Picture3.png)

   Cấu hình máy Ubuntu Internal. IP: 192.168.100.147
 
 ![img](images/Picture4.png)

 -Mạng External
 Cấu hình IP cho máy Kali Attank External
 
 
 ![img](images/Picture5.png)

 Cấu hình máy Window Server mạng External. IP: 10.10.19.202
 
 ![img](images/Picture6.png)

## Cấu hình máy Pfsense
 Chọn Install để cài đặt

 ![img](images/Picture7.png)

Cài đặt thành công. Chọn lựa chọn 2 để cấu hình cho mạng WAN và LAN

 ![img](images/Picture8.png)

Sau khi cấu hình xong, ta được kết quả như sau:

 ![img](images/Picture9.png)

## Kiểm tra kết nối giữa các máy
# Kiểm tra kết nối giữa các máy Internal
Ping từ máy Windows Server đến máy Kali và máy Ubuntu trong mạng Internal.

 ![img](images/Picture10.png)

Ping từ máy Kali đến máy Windows server và máy Ubuntu trong mạng Internal.

 ![img](images/Picture11.png)

Ping từ máy Ubuntu đến máy Windows Server và Kali trong mạng Internal.

 ![img](images/Picture12.png)

# Kiểm tra kết nối giữa các máy External.
Máy Kali External ping tới Windows Server External

 ![img](images/Picture13.png)

Máy Kali External ping tới Window Sever External

 ![img](images/Picture14.png)

# Kiểm tra kết nối giữa các máy Internal, External và máy Pfsense.
Máy Ubuntu Internal ping tới máy Pfsense

 ![img](images/Picture15.png)

Máy Pfsense ping tới máy Ubuntu Internal

 ![img](images/Picture16.png)

Máy Pfsense ping tới máy Kali External

 ![img](images/Picture17.png)

## Máy Pfsense ping tới máy Kali External
- Trên máy Linux victim ở mạng trong, vào trình duyệt gõ http://192.168.100.1 để cấu hình pfsense qua giao diện web.
-> Đăng nhập với username: admin & passwork: pfsense

 ![img](images/Picture18.png)

Cấu hình thành công pfsense qua giao diện web

 ![img](images/Picture19.png)

Cấu hình luật firewall để cho phép luồng ICMP ở mạng External ping được tới giao diện 10.10.19.1.
Tại FireWall trên thanh công cụ, chọn Rules.Sau đó nhấn Add để thêm luật. Chỉnh sửa các mục như các ảnh bên dưới.

 ![img](images/Picture20.png)

 ![img](images/Picture21.png)

Chọn Apply Changes để lưu thay đổi.

 ![img](images/Picture22.png)

Kiểm tra bằng các ping tới 10.10.19.1 từ máy Kali attank ở mạng External

 ![img](images/Picture23.png)

Máy Ubuntu Internal có thể ping từ mạng Internal ra máy Kali External ở mạng ngoài

 ![img](images/Picture24.png)

Quét các cổng mở ở mạng Internal

 ![img](images/Picture25.png)

Quét các cổng mở ở mạng External

 ![img](images/Picture26.png)

- Theo mặc định, có bao nhiêu cổng TCP mở trên giao diện mạng của pfSense?
+ Trong giao diện mạng Internal, theo mặc định có 2 cổng TCP được mở: Cổng 80(HTTP), Cổng 53(domain)
+ Trong giao diện mạng External không có cổng TCP nào được mở

## Cài đặt cấu hình pfsense firewall cho phép chuyển hướng lưu lượng tới các máy trong mạng Internal
- Cấu hình cho phép cổng SSH trên IP 192.168.100.147 (Máy Ubuntu Linux victim mạng Internal) được truy cập từ bên ngoài thông qua port forwarding. Nghĩa là khi các máy khách từ mạng 10.10.19.0/24 kết nối với địa chỉ IP của tường lửa pfSense của 10.10.19.1, chúng sẽ được chuyển hướng đến máy Linux victim trong mạng Internal.

 ![img](images/Picture27.png)


 ![img](images/Picture28.png)

Nhấn Apply Change để lưu thay đổi.

 ![img](images/Picture29.png)

Kiểm tra bằng cách truy cập ssh tới 10.10.19.1 từ máy Kali External.

 ![img](images/Picture30.png)
 ## Kết luận
- Xây dựng topo mạng và cài đặt, cấu hình địa chỉ IP thành công, các máy trong mạng ping được nhau
- Cài đặt, cấu hình thành công ICMP cho phép các máy trong mạng Internal ping được ra các máy ở mạng External, không cho phép ping vào trong mạng Internal.
- Cài đặt thành công cấu hình pfsense firewall cho phép chuyển hướng lưu lượng tới các máy trong mạng Internal.



