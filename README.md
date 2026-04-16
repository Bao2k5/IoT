# 📦 Tủ Bảo Quản Tài Sản Thông Minh AIoT (Smart Preservation Vault)

**Học viện Hàng không Việt Nam - Khoa Công nghệ Thông tin**
**Đề tài Báo cáo môn học:** Internet Vạn Vật (IoT)
**Giảng viên hướng dẫn:** Ths. Nguyễn Thái Sơn

---

## 👥 Danh sách Thành viên Nhóm 02

| STT | Họ và Tên | MSSV | Lớp | Vai trò |
| :---: | :--- | :---: | :---: | :--- |
| **1** | **Lê Dương Bảo** | `2331540071` | `23ĐHTT02` | **Nhóm Trưởng** |
| 2 | Nguyễn Lê Hưng | `2331540323` | `23ĐHTT05` | Thành viên |
| 3 | Giang Vạn Lộc | `2331540002` | `23ĐHTT01` | Thành viên |
| 4 | Nguyễn Thành Vinh | `2331540016` | `23ĐHTT01` | Thành viên |
| 5 | Dương Gia Quốc Bảo | `2331540017` | `23ĐHTT01` | Thành viên |

---

## 🚀 Giới thiệu Dự án
Dự án **Smart Preservation Vault** kết hợp hoàn hảo giữa công nghệ **IoT (Internet of Things)** và **Edge AI** để tạo ra một không gian bảo quản an ninh đa lớp. Khác với các két sắt truyền thống thụ động, tủ hướng tới việc "Phòng vệ Chủ động" và điều hòa môi trường một cách tự động.

### 🌟 Tính năng nổi bật
*   **🛡️ An ninh Sinh trắc học (FaceID):** Mở cửa từ xa hoặc thông qua FaceID Edge AI (InsightFace + YOLOv11) quét khuôn mặt siêu nhạy < 1.5s mà không chạm.
*   **🚨 Chống trộm Tức thì (Zero-Latency):** Báo động chuông ngay lập tức (< 0.5s) khi phát hiện chấn động (SW-420) hoặc cạy cửa (Reed Switch).
*   **🌡️ Điều hòa Khí hậu AIoT:** Tự động kích hoạt khối bán dẫn Sò lạnh Peltier và quạt tản nhiệt thông qua Rơ-le khi phát hiện nhiệt độ môi trường vượt mức thiết lập an toàn.
*   **📱 Giám sát Đám mây (Blynk):** Nhận cảnh báo theo thời gian thực (Push Notification) và theo dõi biểu đồ nhiệt độ ở bất kỳ đâu trên ứng dụng di động.

---

## 📂 Cấu trúc Mã nguồn (Source Code)
Mã nguồn ứng dụng nằm trong thư mục `IoT-Firmware`, chia làm 3 cụm logic chính:

```
📁 IoT-Firmware/
├── 📁 ESP32CAM_Stream/
│   └── ESP32CAM_Stream.ino      # (C++) Đọc PIR, Chụp khung hình Camera gởi Server FaceID qua giao thức HTTP
├── 📁 Smart_Jewelry_IoT/
│   └── Smart_Jewelry_IoT.ino    # (C++) Trạm Node trung tâm xài FreeRTOS quản lý: Peltier, Khóa, Blynk, Cân bằng Rung/Nhiệt
└── AI_Face.py                   # (Python) Khối Edge AI phục vụ kiểm duyệt, API chặn cửa nếu sai người
```

## 🛠️ Công nghệ Kỹ thuật áp dụng
*   **Vi điều khiển chính:** MCU ESP32-WROOM-32 & ESP32-CAM.
*   **Cơ cấu vận hành chịu tải (12V):** Khóa Solenoid điện từ, Sò Nóng lạnh TEC1-12706, DC Fan.
*   **Hệ điều hành nhúng:** FreeRTOS (Luồng Đa nhiệm), Non-blocking `millis()`.
*   **Kết nối vô tuyến:** WiFiManager (Captive Portal cấp WiFI tại chỗ).
*   **Giao thức Backend:** Mạng HTTP/REST API, TCP (Blynk Cloud).

---
*Cảm ơn Thầy đã dành thời gian xem và đánh giá Đồ án của nhóm chúng em!*
