# Notification Center

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Thông báo    Đọc tất cả│
├─────────────────────────────┤
│ 🔵 Chủ sân đã xác nhận     │
│    Sân ABC • 19:00 24/06    │
│                    10 phút  │
├─────────────────────────────┤
│ 🔵 Bạn có tin nhắn mới     │
│    Nguyễn Văn A             │
│                    30 phút  │
├─────────────────────────────┤
│ ⚪ Nhắc: trận đấu 1h nữa   │
│    vs Trần B • Sân XYZ 18h │
│                    2 giờ    │
├─────────────────────────────┤
│ ⚪ Đánh giá sân để nhận     │
│    điểm thưởng!             │
│                    Hôm qua  │
├─────────────────────────────┤
│ ⚪ Booking đã hủy           │
│    Hết 30p giữ chỗ         │
│                    2 ngày   │
├─────────────────────────────┤
│                             │
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Noti list | List | Sắp theo mới nhất. 🔵 chưa đọc, ⚪ đã đọc |
| 2 | Noti item | Card | Icon loại + title + subtitle + thời gian relative |
| 3 | Tap noti | Action | Deep link đến màn hình liên quan (booking-detail, chat-detail, rate-opponent...) |
| 4 | Đọc tất cả | Action | Mark all as read |
| 5 | Icon chuông header | Entry | 🔔 trên mọi screen header, badge đếm unread. Tap → notification-center |
| 6 | Empty state | State | "Chưa có thông báo nào" |
| 7 | Pull to refresh | Behavior | Kéo xuống để refresh |
