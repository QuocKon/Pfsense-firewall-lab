# 🛡️ Pfsense Firewall Lab – Enterprise Network Simulation

## 📌 Giới thiệu
Đây là bài thực hành số 5 môn **Thực tập cơ sở**, với nội dung:
- Cài đặt và cấu hình mạng doanh nghiệp trên **VMware/VirtualBox**
- Thiết lập **tường lửa pfSense**
- Kiểm tra kết nối giữa các máy trong mạng Internal & External
- Cấu hình firewall rule cho ICMP và port forwarding SSH

## 📂 Cấu trúc repo
- `report/` – Báo cáo gốc (DOCX/PDF)
- `docs/` – Hình ảnh sơ đồ mạng, ảnh chụp cấu hình
- `configs/` – File cấu hình pfSense (nếu export)
- `lab-guide.md` – Tóm tắt hướng dẫn từng bước

## 🌐 Topology
![Network Topology](docs/topology.png)

## ⚙️ Nội dung chính
- **Cấu hình mạng trong VMware/VirtualBox**
- **Cài đặt pfSense (WAN & LAN)**
- **Firewall rule cho ICMP**
- **Port forwarding SSH vào máy Ubuntu Internal**

## ✅ Kết quả đạt được
- Các máy trong mạng Internal ping được nhau.
- Cho phép ICMP từ External tới Internal theo rule định nghĩa.
- Cấu hình port forwarding để SSH vào máy Ubuntu từ bên ngoài thành công.

---

👨‍💻 Sinh viên: **Đỗ Quốc Tuân**  
📘 Mã số sinh viên: **B21DCAT201**  
📅 Thời gian: *03/2024*
