# Chi tiết booking

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Booking #1234           │
├─────────────────────────────┤
│                             │
│  Status: ✅ Đã xác nhận     │
│                             │
│  🏸 Sân ABC — Sân B        │
│  📍 123 Nguyễn Huệ, Q1     │
│  📅 Thứ 3, 24/06/2026      │
│  ⏰ 19:00 - 20:00           │
│  💰 200.000đ (đã thanh toán)│
│                             │
├─────────────────────────────┤
│  Chính sách hoàn tiền:      │
│  Hủy trước 18:00 ngày 23/06│
│  → Hoàn 100% (200.000đ)    │
│                             │
├─────────────────────────────┤
│                             │
│  ┌───────────────────────┐  │
│  │  🔄 Đổi giờ/sân      │  │
│  └───────────────────────┘  │
│                             │
│  ┌───────────────────────┐  │
│  │  ❌ Hủy booking       │  │
│  └───────────────────────┘  │
│                             │
│  ┌───────────────────────┐  │
│  │  🗺️ Chỉ đường         │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Status badge | Info | • 🟡 Đang giữ chỗ (pending) + countdown 30p• 🟠 Chờ duyệt (paid) + countdown 30p• ✅ Đã xác nhận (confirmed)• ✅ Hoàn thành (completed) + nút Đánh giá• ❌ Đã hủy (cancelled/rejected/expired) + lý do |
| 2 | Thông tin booking | Info | Sân, địa chỉ, ngày, giờ, giá, trạng thái thanh toán |
| 3 | Chính sách hoàn tiền | Info | Tính toán realtime: mốc giờ cụ thể + số tiền hoàn |
| 4 | Nút Đổi giờ/sân | Action | Chỉ hiện khi confirmed + trước 24h + chưa đổi.• Tap → venue-detail với pre-select sân hiện tại |
| 5 | Nút Hủy booking | Action | Confirm dialog hiện số tiền hoàn cụ thể.• E-011 nếu pending hết giờ |
| 6 | Nút Chỉ đường | Action | Mở Google Maps directions |
| 7 | Nút Đánh giá sân | Action | Chỉ hiện khi completed. → venue-rate |
| 8 | Nút Thanh toán | Action | Chỉ hiện khi pending. Countdown 30p |
| 9 | Error: E-011 | State | "Đã hết 30 phút giữ chỗ, booking đã được hủy" |
| 10 | Error: E-012 | State | "Chủ sân đã từ chối booking, tiền sẽ được hoàn trong 24h" |
