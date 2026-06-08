# invite-confirm

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Xác nhận lời mời     │
│                         │
│  ┌─────────────────────┐│
│  │ Đối thủ: Minh T.    ││
│  │ ★ 4.2 | Trung bình  ││
│  ├─────────────────────┤│
│  │ Sân: ABC             ││
│  │ Giờ: 18:00 - 19:00  ││
│  │ Ngày: 04/06/2026    ││
│  │ Giá: 150.000đ       ││
│  ├─────────────────────┤│
│  │ Thanh toán: Tại sân ││
│  └─────────────────────┘│
│                         │
│  ⚠️ Slot giữ 5 phút     │
│  sau khi gửi lời mời    │
│                         │
│  ┌───────────────────┐  │
│  │  GỬI LỜI MỜI     │  │
│  └───────────────────┘  │
│                         │
│  [Hủy]                  │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Thông tin đối thủ | static card | • Tên + rating + trình độ |
| 2 | Thông tin sân | static card | • Tên sân + giờ + ngày + giá |
| 3 | Phương thức thanh toán | static text | • v1.0: "Tại sân"<br>• v1.1: MoMo/VNPay selector<br>• Ref: BR-sport-matching-011 |
| 4 | Cảnh báo slot lock | info text | • "Slot giữ 5 phút sau khi gửi lời mời"<br>• Ref: BR-sport-matching-003 |
| 5 | Nút Gửi lời mời | button primary | • Tap: lock slot + tạo match + gửi invite FCM<br>• Chuyển sang waiting state (countdown 5 phút)<br>• Error: E-sport-matching-004 (match pending), E-sport-matching-005 (hết limit) |
| 6 | Nút Hủy | text link | • Quay về court-select, không lock slot |
