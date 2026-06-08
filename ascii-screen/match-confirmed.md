# match-confirmed

## 1. Wireframe

```
┌─────────────────────────┐
│                         │
│     ✓ TRẬN ĐÃ XÁC NHẬN│
│                         │
│  ┌─────────────────────┐│
│  │ Đối thủ: Minh T.    ││
│  │ ★ 4.2 | Trung bình  ││
│  ├─────────────────────┤│
│  │ Sân: ABC             ││
│  │ Địa chỉ: 123 Nguyễn││
│  │ Văn Linh, Q.7       ││
│  │ Giờ: 18:00 - 19:00  ││
│  │ Ngày: 04/06/2026    ││
│  ├─────────────────────┤│
│  │ ┌─────────────────┐ ││
│  │ │   [Bản đồ mini] │ ││
│  │ └─────────────────┘ ││
│  └─────────────────────┘│
│                         │
│  Thanh toán: Tại sân    │
│  Giá: 150.000đ          │
│                         │
│  ┌───────────────────┐  │
│  │   VỀ TRANG CHÍNH  │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Badge xác nhận | icon + text | • ✓ "Trận đã xác nhận"<br>• Color: green |
| 2 | Thông tin đối thủ | static card | • Tên + rating + trình độ |
| 3 | Thông tin sân | static card | • Tên sân + địa chỉ đầy đủ + giờ + ngày |
| 4 | Bản đồ mini | map embed | • Vị trí sân trên bản đồ nhỏ<br>• Tap: mở Google Maps navigation |
| 5 | Thanh toán + giá | static text | • v1.0: "Tại sân" + giá<br>• Ref: BR-sport-matching-011 |
| 6 | Nút Về trang chính | button primary | • Chuyển về map-search |
