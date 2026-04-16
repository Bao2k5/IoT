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
Dự án **Smart Preservation Vault** kết hợp hoàn hảo giữa công nghệ **IoT (Internet of Things)**, **Cloud Computing** và **Edge AI** để tạo ra một không gian bảo quản an ninh đa lớp. Khác với các két sắt truyền thống thụ động, tủ hướng tới việc "Phòng vệ Chủ động" và điều hòa môi trường một cách tự động.

### 🌟 Tính năng nổi bật
*   **🛡️ An ninh Sinh trắc học (FaceID):** Mở cửa thông qua FaceID Edge AI nhận diện 512-chiều siêu chuẩn, chống mở sai.
*   **🚨 Chống trộm Tức thì (Zero-Latency):** Kiến trúc Multi-threading xử lý bật còi báo động ngay lập tức (< 0.5s) khi phát hiện chấn động (SW-420) hoặc cạy cửa (Reed Switch).
*   **🌡️ Điều hòa Khí hậu AIoT:** Tự động giám sát nhiệt/ẩm (DHT11) và bật/tắt khối tản nhiệt Sò lạnh Peltier thông qua Relay.
*   **📱 Giám sát Đám mây:** Kết hợp Server Web Socket và Blynk IoT để theo dõi, nhận Push Notification liên tục 24/7.

---

## 📂 Cấu trúc Mã nguồn (Source Code) Toàn Diện
Mã nguồn ứng dụng được chia làm Trạm vật lý (Firmware), Trạm biên (Edge AI) và Đám mây (Cloud Backend):

```
📁 IoT/ (root)
├── 📁 IoT-Firmware/
│   ├── 📁 ESP32CAM_Stream/
│   │   └── ESP32CAM_Stream.ino      # (C++) Đọc PIR, chụp và gởi ảnh lên Server FaceID (HTTP POST)
│   ├── 📁 Smart_Jewelry_IoT/
│   │   └── Smart_Jewelry_IoT.ino    # (C++) MCU Trung tâm (ESP32): Xử lý FreeRTOS quản lý Peltier, Khóa, Blynk, Cân bằng Rung/Nhiệt
│   └── AI_Face.py                   # (Python) Khối Edge AI phục vụ kiểm duyệt khuôn mặt (InsightFace + YOLOv11)
├── 📁 IoT-Backend/
│   └── 📁 src/                      # (Node.js) Web Socket Server & REST API
│       ├── 📁 models/               # Schema kết nối Cơ sở dữ liệu MongoDB Atlas (Security, TempLogs...)
│       ├── 📁 controllers/          # Nhận dữ liệu Telemetry từ ESP32 và đẩy lên Web/Dashboard
│       └── ...
└── README.md
```

---

## 🛠️ Trọn bộ Công nghệ Kỹ thuật (Tech Stack) Sử Dụng Trong Dự Án

### 💻 1. Vi điều khiển & Hệ điều hành Nhúng (Embedded Systems)
*   **Nền tảng MCU:** `ESP32-WROOM-32` (Lõi xử lý chính) & `ESP32-CAM` (Mắt thần Camera).
*   **Ngôn ngữ Lập trình:** `C/C++` (Biên dịch trực tiếp ra mã máy giúp độ trễ cực thấp).
*   **Multi-threading:** Ứng dụng hệ điều hành thời gian thực `FreeRTOS` để chia luồng (Core 0 cho WiFi, Core 1 cho điều khiển IO).
*   **Smart Time-Delay:** Kỹ thuật Non-blocking sử dụng hàm `millis()` để tránh treo vi xử lý khi đọc cảm biến liên tục.

### 🔌 2. Linh kiện Điện tử & Cơ cấu Chấp hành (Hardware & Actuators)
*   **Bảo mật:** Khóa điện từ Solenoid 12V siêu tốc, Cảm biến từ tính Reed Switch, Cảm biến Rung SW-420, Cảm biến PIR HC-SR501.
*   **Làm mát không gian kín:** Sò nóng lạnh bán dẫn `Peltier TEC1-12706` kết hợp mạng lưới Quạt `DC Fan`.
*   **Kiểm soát:** Mạch Relay cách ly quang, Mạch hạ áp `LM2596` (nắn dòng 12V xuống 5V an toàn), Màn hình `LCD I2C` hiển thị tại chỗ.

### 🌐 3. Mạng IoT & Cloud Server (Internet of Things & Cloud)
*   **Cấp mạng thông minh:** `WiFiManager` (Tạo Captive Portal cắm-là-chạy, không cần hardcode SSID).
*   **IoT Dashboard:** `Blynk IoT Cloud` (Vẽ biểu đồ nhiệt độ, điều khiển các chốt Relay từ xa qua Remote App).
*   **Web Server Middleware:** Xây dựng Backend nội bộ chuẩn `Node.js` (Lưu trữ lịch sử truy cập, tối ưu ping dưới 100ms thay vì AWS).
*   **Cơ sở Dữ liệu Đám mây:** `MongoDB Atlas` (NoSQL) lưu trữ Log mở cửa và Dữ liệu Cảnh báo (Telemetry Data) siêu tốc, không bị mất khi cúp điện.

### 🧠 4. Trí Tuệ Nhân Tạo Biên (Edge AI Computervision)
*   **Ngôn ngữ AI:** `Python`.
*   **Phát hiện hiện diện (Object Detection):** Mạng nơ-ron `YOLOv11` phối hợp thuật toán `ByteTrack` để tạo Virtual Fence siêu chính xác.
*   **Nhận diện khuôn mặt (Face Recognition):** Mô hình `InsightFace` sử dụng hàm `ArcFace Loss` tối ưu hóa khoảng cách không gian đa chiều (Vector 512-D), hoạt động cực kỳ ổn định trong môi trường ánh sáng phức tạp và kháng che khuất tốt (độ nhận diện thực tế >95% và tỷ lệ mở cửa sai (False Positive) gần như bằng không).

---
*Cảm ơn Thầy đã dành thời gian xem và đánh giá Đồ án của nhóm chúng em!*
