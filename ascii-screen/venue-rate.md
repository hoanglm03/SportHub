# Đánh giá sân

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Đánh giá sân           │
├─────────────────────────────┤
│                             │
│  🏸 Sân ABC — Sân B        │
│  📅 24/06/2026 • 19:00     │
│                             │
├─────────────────────────────┤
│                             │
│  Đánh giá của bạn:          │
│                             │
│     ☆  ☆  ☆  ☆  ☆         │
│     1  2  3  4  5           │
│                             │
├─────────────────────────────┤
│                             │
│  Nhận xét (tùy chọn):      │
│  ┌───────────────────────┐  │
│  │                       │  │
│  │                       │  │
│  │              0/500    │  │
│  └───────────────────────┘  │
│                             │
├─────────────────────────────┤
│  🎁 +10 điểm thưởng        │
│  (còn 5 ngày để nhận thưởng)│
│                             │
├─────────────────────────────┤
│                             │
│  ┌───────────────────────┐  │
│  │    Gửi đánh giá       │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Thông tin booking | Info | Sân + sân con + ngày giờ đã chơi |
| 2 | Rating stars | Input | Tap chọn 1-5 sao. Bắt buộc |
| 3 | Review text | Input | Textarea optional, max 500 ký tự, counter |
| 4 | Điểm thưởng | Info | Hiện số điểm sẽ nhận.• Trong 7 ngày: hiện số điểm + countdown• Quá 7 ngày: "Đã hết hạn nhận thưởng" (vẫn đánh giá được) |
| 5 | Nút Gửi | Action | Validate sao đã chọn → submit.• Success: "Cảm ơn đánh giá! Bạn nhận được {X} điểm thưởng" |
| 6 | Đã đánh giá | State | Nếu đã đánh giá booking này → hiện read-only review + sao + "Bạn đã đánh giá" |
