# invite-waiting

## 1. Wireframe

```
┌─────────────────────────┐
│  Đang chờ đối thủ...     │
│                         │
│  ┌─────────────────────┐│
│  │ Đối thủ: Minh T.    ││
│  │ ★ 4.2 | Trung bình  ││
│  ├─────────────────────┤│
│  │ Sân: ABC             ││
│  │ Giờ: 18:00 - 19:00  ││
│  │ Ngày: 07/06/2026    ││
│  └─────────────────────┘│
│                         │
│        ┌───────┐        │
│        │ 04:32 │        │
│        └───────┘        │
│     Đang chờ phản hồi   │
│                         │
│     ● ● ● (loading)     │
│                         │
│  ┌───────────────────┐  │
│  │   HỦY LỜI MỜI    │  │
│  └───────────────────┘  │
│                         │
│  Slot sân đang giữ      │
│  5 phút                 │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Thông tin đối thủ | static card | • Tên + rating + trình độ đối thủ được mời |
| 2 | Thông tin trận | static card | • Sân + giờ + ngày |
| 3 | Countdown timer | timer (mm:ss) | • Đếm ngược từ 5:00<br>• Update mỗi giây<br>• Font lớn, center screen<br>• Hết 0:00 → hiện E-sport-matching-002 |
| 4 | Loading indicator | animation | • Dots animation hoặc spinner<br>• Text "Đang chờ phản hồi" |
| 5 | Nút Hủy lời mời | button secondary (red) | • Tap: cancel invite + release slot + quay về map-search<br>• Confirm dialog "Hủy lời mời? Slot sân sẽ được giải phóng." |
| 6 | Info slot lock | static text | • "Slot sân đang giữ 5 phút"<br>• Ref: BR-sport-matching-003 |
| 7 | State: Đối thủ accept | auto transition | • Countdown dừng<br>• Hiện animation success ✓<br>• Auto chuyển match-confirmed sau 1.5s |
| 8 | State: Đối thủ reject | modal overlay | • E-sport-matching-003: "Đối thủ đã từ chối trận đấu..."<br>• Nút "Tìm đối thủ khác" → map-search<br>• Slot auto release |
| 9 | State: Timeout | modal overlay | • E-sport-matching-002: "Yêu cầu ghép đôi đã hết hạn..."<br>• Nút "Tìm đối thủ khác" → map-search<br>• Slot auto release |
