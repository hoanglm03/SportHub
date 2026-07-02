# payment-checkout

## 1. Wireframe

```
┌─────────────────────────┐
│  ←  Thanh toán          │
├─────────────────────────┤
│                         │
│  ┌─────────────────────┐│
│  │ Tóm tắt đặt sân     ││
│  │ Sân ABC — Sân A      ││
│  │ 18:00 - 19:00        ││
│  │ Ngày: 26/06/2026     ││
│  ├─────────────────────┤│
│  │ Tổng tiền: 150.000đ  ││
│  │ Commission (12%):    ││
│  │            -18.000đ  ││
│  │ Chủ sân nhận: 132k  ││
│  └─────────────────────┘│
│                         │
│  Chọn phương thức:      │
│                         │
│  ┌─────────────────────┐│
│  │ 💜 MoMo             ││
│  │    Ví MoMo / QR     ││
│  └─────────────────────┘│
│                         │
│  ┌─────────────────────┐│
│  │ 🔵 VNPay            ││
│  │    Thẻ ATM / QR     ││
│  └─────────────────────┘│
│                         │
│  ┌───────────────────┐  │
│  │  THANH TOÁN NGAY  │  │
│  └───────────────────┘  │
│                         │
│  🔒 Giao dịch được bảo  │
│     mật bởi SSL/TLS     │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Header + back | navigation | • "← Thanh toán"<br>• Back → booking-confirm |
| 2 | Tóm tắt booking | static card | • Tên sân + sân con + giờ + ngày<br>• Tổng tiền + commission 12% + chủ sân nhận |
| 3 | Option MoMo | radio button | • Icon + label "MoMo — Ví MoMo / QR"<br>• Tap: select, highlight border |
| 4 | Option VNPay | radio button | • Icon + label "VNPay — Thẻ ATM / QR"<br>• Tap: select, highlight border |
| 5 | Nút Thanh toán | button primary | • Active khi đã chọn cổng<br>• Tap: redirect deeplink MoMo/VNPay<br>• Loading state: spinner + "Đang xử lý..."<br>• E-sport-matching-022 nếu timeout 60s |
| 6 | SSL badge | static text | • "🔒 Giao dịch được bảo mật bởi SSL/TLS"<br>• Tăng trust, không tương tác |
| 7 | Empty state | — | • Không chọn cổng mà nhấn Thanh toán → shake button + "Vui lòng chọn phương thức" |
