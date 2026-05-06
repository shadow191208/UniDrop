# 🚀 UniDrop – Local File Sharing App (Android ↔ Windows)

## 📌 Overview

**UniDrop** là ứng dụng chia sẻ file đa thiết bị hoạt động **offline-first**, cho phép gửi file giữa:

* 📱 Android
* 🖥️ Windows

Không cần internet, không cần cloud.

---

## 🎯 Goal

Thay thế workflow rườm rà như:

* gửi qua Zalo
* dùng cáp USB
* upload cloud

👉 bằng trải nghiệm:

> ⚡ “Chọn file → gửi → tất cả thiết bị nhận ngay”

---

## 🧠 Core Features

* 📂 Gửi mọi loại file (ảnh, video, docx, excel, zip…)
* 👥 Multi-device (room)
* 🔄 Auto sync (tất cả thiết bị tự download)
* ⚡ LAN tốc độ cao
* 🔵 Bluetooth fallback

---

## ⚙️ Architecture

### 🧩 Model

* 1 Host (Windows)
* Nhiều Client (Android)

```text
Client → Upload → Host
Host → Broadcast → Clients
Clients → Auto Download
```

---

## 📶 Connectivity

### 1. Wi-Fi (LAN)

* HTTP + WebSocket
* tốc độ cao
* multi-device

---

### 2. Bluetooth

* fallback khi không có Wi-Fi
* chỉ dùng file nhỏ

---

## 👥 Room System

### Create Room

* Host tạo room
* Add device bằng danh sách nearby

---

### Join Room

* Device nhận request
* Accept → join ngay

---

## 📂 File Sync (Hub Model)

### Flow

```text
Upload → Host → Broadcast → Auto Download
```

---

### Rules

* chỉ host broadcast
* client không broadcast lại
* chỉ sync khi file hoàn tất

---

## 📦 File States

* uploading
* ready
* downloading
* synced

---

## 🔄 Concurrent Transfer

* Upload + Download đồng thời

### Queue:

* uploadQueue
* downloadQueue

---

## 🧠 Room Lifecycle

* tồn tại khi còn member
* xoá khi tất cả rời
* timeout 1h nếu không activity

### Activity gồm:

* upload
* download
* join
* heartbeat

---

## 💾 Storage

* file lưu trên host
* xoá khi room kết thúc

---

## 🧱 Tech Stack

### 📱 Android

* Flutter

### 🖥️ Windows

* Node.js (Express + WebSocket)

---

## 📁 Project Structure

### Server

```text
server/
 ├── server.js
 ├── routes/
 ├── sockets/
 ├── rooms/
 └── uploads/
```

---

### Flutter

```text
lib/
 ├── screens/
 ├── services/
 ├── models/
 └── widgets/
```

---

## 🚀 Getting Started

### 1. Clone repo

```bash
git clone https://github.com/shadow191208/UniDrop.git
```

---

### 2. Run server

```bash
cd server
npm install
node server.js
```

---

### 3. Run Android app

```bash
flutter pub get
flutter run
```

---

## 🗺️ Roadmap

### v1

* LAN connection
* file upload

### v2

* room + multi-device

### v3

* auto sync

### v4

* Bluetooth

---

## ⚠️ Known Limitations

* chưa tối ưu file lớn
* Bluetooth chậm
* chưa có resume download

---

## 💡 Future Ideas

* WebRTC (P2P)
* multi-host
* file versioning
* UI nâng cao

---

## 👨‍💻 Author

* Personal project
* Focus: simple, fast, offline-first

---
