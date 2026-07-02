# invite-receive

## 1. Wireframe

```
┌─────────────────────────┐
│  Lời mời đấu!           │
│                         │
│  ┌─────────────────────┐│
│  │ Từ: Long P.         ││
│  │ ★ 4.5 | Nâng cao    ││
│  ├─────────────────────┤│
│  │ Môn: Cầu lông       ││
│  │ Sân: ABC             ││
│  │ Giờ: 18:00 - 19:00  ││
│  │ Ngày: 04/06/2026    ││
│  │ Giá: 150.000đ       ││
│  └─────────────────────┘│
│                         │
│     ⏱️ Còn 04:32        │
│                         │
│  ┌──────┐  ┌──────────┐│
│  │ TỪ   │  │ CHẤP     ││
│  │ CHỐI │  │ NHẬN     ││
│  └──────┘  └──────────┘│
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Thông tin người mời | static card | • Tên + rating + trình độ môn matching |
| 2 | Thông tin trận | static card | • Môn + sân + giờ + ngày + giá |
| 3 | Countdown | timer | • Đếm ngược từ 5:00<br>• Hết hạn: auto chuyển về map-search với toast "Lời mời đã hết hạn"<br>• Nếu mở từ push noti (background): vẫn navigate về map-search (không drop về OS home)<br>• Ref: BR-sport-matching-002 |
| 4 | Nút Chấp nhận | button primary (green) | • Tap: accept invite, match confirmed<br>• Chuyển match-confirmed |
| 5 | Nút Từ chối | button secondary (red) | • Tap: reject invite<br>• Người mời nhận E-sport-matching-003<br>• Slot release |
