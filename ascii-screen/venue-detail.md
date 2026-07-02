# Chi tiết sân

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Sân ABC             ♡  │
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │                       │   │
│ │   [Ảnh sân carousel]  │   │
│ │     1/5  ● ○ ○ ○ ○    │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│ ⭐ 4.5 (120 đánh giá)      │
│ 📍 123 Nguyễn Huệ, Q1      │
│    1.2km từ bạn             │
│ 🏸 Cầu lông • Pickleball   │
│ 💰 150.000đ/h               │
│ ⏰ 6:00 - 22:00             │
│ 🅿️ Bãi xe • Nước uống •    │
│    Phòng thay đồ            │
├─────────────────────────────┤
│ Chọn sân con:               │
│ ┌──────┐ ┌──────┐ ┌──────┐ │
│ │Sân A │ │Sân B✓│ │Sân C │ │
│ └──────┘ └──────┘ └──────┘ │
├─────────────────────────────┤
│ 📅 Thứ 3, 24/06     ◀  ▶  │
├─────────────────────────────┤
│ 06:00  ░░░░  Đã đặt        │
│ 07:00  ▓▓▓▓  150k  [Chọn]  │
│ 08:00  ▓▓▓▓  150k  [Chọn]  │
│ 09:00  ░░░░  Đã đặt        │
│ 10:00  ▓▓▓▓  150k  [Chọn]  │
│ ...                         │
│ 19:00  ▓▓▓▓  200k  [Chọn]  │
│ 20:00  ░░░░  Đã đặt        │
├─────────────────────────────┤
│ Đánh giá (120)         Xem ▶│
│ ⭐⭐⭐⭐⭐ "Sân đẹp..."   │
│ ⭐⭐⭐⭐☆ "Tốt nhưng..."  │
├─────────────────────────────┤
│ [    🗺️ Xem trên bản đồ   ]│
├─────────────────────────────┤
│  🏠    🗺️    🔍    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Ảnh carousel | Media | Swipe ảnh sân (min 3, max 10) |
| 2 | Rating + reviews count | Info | Tap → scroll xuống phần đánh giá |
| 3 | Địa chỉ + khoảng cách | Info | Tọa độ GPS, tính khoảng cách từ user |
| 4 | Môn hỗ trợ | Info | Danh sách môn thể thao sân hỗ trợ |
| 5 | Giá/giờ | Info | Giá có thể khác theo peak/off-peak |
| 6 | Khung giờ hoạt động | Info | Giờ mở - đóng cửa |
| 7 | Tiện ích | Info | Icons + label: bãi xe, nước, phòng thay đồ... |
| 8 | Sân con chips | Selector | Chọn 1 sân con. Default sân đầu tiên |
| 9 | Ngày picker | Selector | Mặc định hôm nay, swipe ◀▶ (max 14 ngày) |
| 10 | Grid slot giờ | List | • ▓▓▓▓ Trống: giá + nút [Chọn]• ░░░░ Đã đặt: disabled, hiện "Đã đặt"• Real-time cập nhật |
| 11 | Đánh giá preview | Section | 2 review gần nhất. "Xem" → full list |
| 12 | Bản đồ link | Action | Mở Google Maps / in-app map |
| 13 | Error: E-010 | State | "Khung giờ này đã có người đặt" khi slot vừa bị lock |
| 14 | Error: E-014 | State | "Chỉ có thể đặt sân trước tối thiểu 2 giờ" |
| 15 | Error: E-013 | State | "Bạn đang có 3 booking..." |
