# 🚀 UniDrop – Local File Sharing App (Android ↔ Windows)

## 📌 Giới thiệu

**UniDrop** là ứng dụng chia sẻ file đa thiết bị (Android ↔ Windows) hoạt động trong mạng nội bộ (LAN) hoặc Bluetooth, với mục tiêu:

* Gửi **mọi loại file**: ảnh, video, audio, docx, excel, zip, ...
* Không cần internet
* Hỗ trợ **multi-device (room)**
* Tự động **đồng bộ file (auto-sync)** giữa các thiết bị
* Trải nghiệm đơn giản như AirDrop

---

## 🎯 Mục tiêu

* Thay thế workflow thủ công (Zalo, cáp USB…)
* Tạo hệ thống:

  > 🔥 “Shared folder real-time giữa nhiều thiết bị”

---

## 🧠 Core Concept

* Tạo **Room (phòng tạm thời)**
* Nhiều thiết bị join vào room
* Khi có file mới:

  * tất cả thiết bị **tự động download**

---

## ⚙️ Kiến trúc tổng thể

### 🧩 Mô hình

* 1 **Host (Windows)**
* Nhiều **Client (Android)**

```
Android → Upload → Host (Node.js)
Host → Broadcast → Clients
Clients → Auto Download
```

---

## 📶 Kết nối

### 1. Wi-Fi (LAN) – chính

* Dùng HTTP + WebSocket
* Tốc độ cao
* Hỗ trợ nhiều thiết bị

---

### 2. Bluetooth – phụ

* Dùng khi không có Wi-Fi
* Chỉ nên dùng:

  * 1–1 hoặc file nhỏ
* Không hỗ trợ sync toàn room tốt

---

## 👥 UX Flow

### Tạo Room

1. User 1 tạo room
2. Nhấn "+"
3. Chọn thiết bị gần

---

### Join Room

1. Device khác nhận request
2. Nhấn “Accept”
3. Vào room ngay

---

## 📂 Cơ chế chia sẻ file

### 🔥 Auto Sync (Hub Model)

* Khi 1 device upload:

  * Host nhận file
  * Broadcast metadata
  * Tất cả device tự download

---

### Flow

```
Upload → Host → Broadcast → Download
```

---

### ⚠️ Rule quan trọng

* Chỉ **host broadcast**
* Client **không broadcast lại**
  → tránh loop

---

## 📦 Trạng thái file

* `uploading`
* `ready`
* `downloading`
* `synced`

---

## 🔄 Upload & Download đồng thời

* Hỗ trợ full-duplex:

  * vừa upload
  * vừa download

---

### Queue

* Upload Queue
* Download Queue

---

### Giới hạn

* Upload: 1–2 file
* Download: 2–3 file

---

## 🧠 Room Lifecycle

### Room tồn tại khi:

* còn ít nhất 1 member

---

### Xoá Room khi:

* tất cả rời → xoá ngay

---

### Timeout

* 1h không activity → xoá

---

### Activity gồm:

* upload
* download
* join
* heartbeat

---

### Heartbeat

* mỗi 10–20s gửi ping
* mất ping → remove device

---

## 💾 Lưu trữ

* File lưu trên **host**
* Khi room xoá → file xoá

---

## 🔒 Bảo mật (basic)

* xác nhận khi join
* không cần cloud
* không lưu lâu dài

---

## ⚠️ Giới hạn chấp nhận

* Không tối ưu băng thông
* Không P2P
* Bluetooth hạn chế
* Không sync cloud

---

## 💡 Tối ưu nên có

* progress bar
* retry khi lỗi
* cảnh báo file lớn (>100MB)
* setting auto-download

---

## 🧱 Tech Stack

### 📱 Android

* Flutter (Dart)

### 🖥️ Windows

* Node.js (Express + WebSocket)

---

## 📡 Networking

* HTTP (upload/download)
* WebSocket (real-time event)

---

## 📁 Cấu trúc project

### Server (Node.js)

```
server/
 ├── server.js
 ├── routes/
 ├── sockets/
 ├── rooms/
 └── uploads/
```

---

### Flutter

```
lib/
 ├── screens/
 ├── services/
 ├── models/
 └── widgets/
```

---

## 🗺️ Roadmap phát triển

### ✅ Phase 1 – Kết nối

* Android gọi được server

---

### ✅ Phase 2 – Gửi file

* Upload file thành công

---

### ✅ Phase 3 – Room

* Multi-device
* WebSocket

---

### ✅ Phase 4 – Auto Sync

* Broadcast file
* Auto download

---

### ✅ Phase 5 – Hoàn thiện

* Queue
* Progress
* Lifecycle
* Bluetooth

---

## ⏱️ Timeline

| Phase | Thời gian |
| ----- | --------- |
| 1     | 1–2 ngày  |
| 2     | 2–3 ngày  |
| 3     | 3–5 ngày  |
| 4     | 4–7 ngày  |
| 5     | 5–10 ngày |

---

## ❗ Những lỗi cần tránh

* Broadcast từ client → gây loop
* Download file chưa upload xong
* Không giới hạn số file chạy đồng thời
* Không xử lý disconnect

---

## 🧠 Insight

Bạn đang build:

> 🔥 Mini distributed file sync system (local)

Không phải:

* chat app
* cloud storage

---

## 🎯 Kết luận

**UniDrop =**

> AirDrop + USB + Shared Folder (offline)

---

## 🚀 Future (optional)

* WebRTC (P2P)
* Multi-host
* Resume download
* File versioning

---

## 👨‍💻 Author

* Personal project
* Focus: simplicity, speed, offline-first

---
