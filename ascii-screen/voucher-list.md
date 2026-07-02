# Voucher & Khuyến mãi

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Ưu đãi của tôi         │
├─────────────────────────────┤
│ Mã giới thiệu của bạn:     │
│ ┌───────────────────────┐   │
│ │  HOANG2026  [📋 Copy] │   │
│ │  Đã mời: 3 bạn        │   │
│ │  Thưởng: 30.000đ      │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│ Voucher khả dụng (2):      │
│ ┌───────────────────────┐   │
│ │ 🎫 Giảm 20% đặt sân   │   │
│ │ Code: WELCOME20        │   │
│ │ HSD: 30/07/2026        │   │
│ │ ĐK: booking ≥ 100.000đ │   │
│ │ [Dùng ngay]            │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ 🎫 Giảm 50.000đ       │   │
│ │ Code: BDAY2026         │   │
│ │ HSD: 15/07/2026        │   │
│ │ ĐK: không giới hạn    │   │
│ │ [Dùng ngay]            │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│ Nhập mã voucher:            │
│ ┌──────────────┐ [Áp dụng] │
│ │              │            │
│ └──────────────┘            │
├─────────────────────────────┤
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Mã referral | Card | Mã cá nhân + nút copy + stats (đã mời, thưởng nhận) |
| 2 | Voucher list | List | Voucher khả dụng: tên, code, HSD, điều kiện. Nút "Dùng ngay" → booking-confirm auto-fill code |
| 3 | Nhập mã | Input | Nhập code thủ công + nút Áp dụng. E-029 nếu không hợp lệ |
| 4 | Voucher đã dùng | Section | Collapse section: lịch sử voucher đã sử dụng |
| 5 | Empty state | State | "Chưa có voucher nào. Mời bạn bè để nhận thưởng!" |
