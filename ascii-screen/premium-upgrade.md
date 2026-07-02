# premium-upgrade

## 1. Wireframe

```
┌─────────────────────────┐
│  ←  Nâng cấp Premium    │
├─────────────────────────┤
│                         │
│   ⭐ SPORT MATCHING     │
│      PREMIUM            │
│                         │
│  ┌─────────────────────┐│
│  │ ✓ Invite không giới ││
│  │   hạn mỗi ngày      ││
│  │ ✓ Ưu tiên hiển thị  ││
│  │   trong kết quả     ││
│  │ ✓ Badge Premium     ││
│  │   trên profile      ││
│  └─────────────────────┘│
│                         │
│  ┌─────────────────────┐│
│  │  49.000 đ / tháng   ││
│  │  Tự động gia hạn    ││
│  │  Hủy bất cứ lúc nào ││
│  └─────────────────────┘│
│                         │
│  ┌───────────────────┐  │
│  │  ĐĂNG KÝ PREMIUM  │  │
│  └───────────────────┘  │
│                         │
│  Chọn phương thức:      │
│  ○ MoMo  ○ VNPay        │
│                         │
│  Điều khoản sử dụng     │
│  Chính sách hoàn tiền   │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Header + back | navigation | • "← Nâng cấp Premium"<br>• Xuất hiện từ: map-search (E-005 banner) hoặc settings |
| 2 | Hero badge | static visual | • Icon ⭐ + "SPORT MATCHING PREMIUM"<br>• Tạo cảm giác premium, màu vàng/gradient |
| 3 | Danh sách quyền lợi | checklist | • ✓ Invite không giới hạn mỗi ngày<br>• ✓ Ưu tiên hiển thị trong kết quả matching<br>• ✓ Badge Premium trên profile<br>• Ref: FR-sport-matching-017 |
| 4 | Giá + điều kiện | pricing card | • "49.000đ / tháng" bold<br>• "Tự động gia hạn · Hủy bất cứ lúc nào"<br>• Ref: BR-sport-matching-004 |
| 5 | Nút Đăng ký | button primary | • "ĐĂNG KÝ PREMIUM"<br>• Tap: xử lý thanh toán qua cổng đã chọn<br>• Thành công → account Premium active, back về màn trước + toast "Bạn đã là Premium!" |
| 6 | Chọn cổng thanh toán | radio inline | • MoMo / VNPay (2 options)<br>• Default: MoMo |
| 7 | Links pháp lý | text link | • "Điều khoản sử dụng" + "Chính sách hoàn tiền"<br>• Mở webview |
| 8 | State: đã là Premium | conditional | • Nếu Player đã Premium: hiện "Đang dùng Premium — hết hạn DD/MM" + nút "Gia hạn" thay vì "Đăng ký" |
