# Xác nhận đặt sân

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Xác nhận đặt sân       │
├─────────────────────────────┤
│                             │
│  🏸 Sân ABC — Sân B        │
│  📍 123 Nguyễn Huệ, Q1     │
│  📅 Thứ 3, 24/06/2026      │
│  ⏰ 19:00 - 20:00           │
│  💰 200.000đ                │
│                             │
├─────────────────────────────┤
│                             │
│  Chính sách hủy:            │
│  • Trước 24h: hoàn 100%    │
│  • 12-24h: hoàn 75%        │
│  • 2-12h: hoàn 50%         │
│  • Dưới 2h: không hoàn     │
│                             │
├─────────────────────────────┤
│                             │
│  ┌───────────────────────┐  │
│  │  💳 Thanh toán ngay   │  │
│  └───────────────────────┘  │
│                             │
│  ┌───────────────────────┐  │
│  │  🕐 Giữ chỗ 30 phút  │  │
│  └───────────────────────┘  │
│                             │
│  ⏱️ Slot tạm giữ: 09:45    │
│                             │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Thông tin sân | Info | Tên sân + sân con, địa chỉ, ngày, giờ, giá |
| 2 | Chính sách hủy | Info | Hiện 3 mức hoàn tiền rõ ràng |
| 3 | Nút Thanh toán ngay | Action | Chuyển sang payment flow (premium-payment).• Thành công → booking paid → chờ duyệt |
| 4 | Nút Giữ chỗ 30 phút | Action | Tạo booking pending, đếm ngược 30p.• Thành công → "Đã giữ chỗ thành công! Bạn có 30 phút để thanh toán" |
| 5 | Countdown tạm giữ | Timer | Đếm ngược **10 phút** tạm giữ slot (BR-014). Hết 10p chưa chọn action → slot giải phóng, quay lại venue-detail. Nếu chọn "Giữ chỗ 30p" → timer đổi sang 30p trên booking-detail |
| 6 | Loading state | State | Spinner khi đang xử lý |
