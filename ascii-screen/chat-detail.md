# Chat chi tiết

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Nguyễn Văn A   🟢 Online│
├─────────────────────────────┤
│                             │
│         Hôm nay 14:20       │
│                             │
│  ┌─────────────────┐        │
│  │ Chơi cầu lông   │        │
│  │ chiều nay k?     │  14:20│
│  └─────────────────┘        │
│                             │
│        ┌─────────────────┐  │
│        │ OK, 17h nhé!    │  │
│  14:22 │                 │  │
│        └─────────────────┘  │
│                             │
│  ┌─────────────────┐        │
│  │ [📷 Ảnh sân]    │        │
│  │ Sân này đẹp     │  14:25│
│  └─────────────────┘        │
│                             │
│        ┌─────────────────┐  │
│        │ Đặt sân đi 👍  │  │
│  14:26 │                 │  │
│        └─────────────────┘  │
│                             │
├─────────────────────────────┤
│ 📷  [Nhập tin nhắn...] [▶] │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Header | Info | Tên + avatar + online status. Tap → profile |
| 2 | Message bubbles | Chat | Bên trái (họ) / bên phải (mình). Timestamp. Ảnh inline |
| 3 | Input bar | Input | Text input + nút gửi ảnh 📷 + nút gửi ▶ |
| 4 | Ảnh gửi | Media | Tap 📷 → chọn từ gallery hoặc chụp. Max 10MB, JPG/PNG |
| 5 | Real-time | Behavior | Tin nhắn mới hiện ngay không cần refresh. Typing indicator |
| 6 | Error: E-015 | State | Ảnh > 10MB hoặc format sai |
