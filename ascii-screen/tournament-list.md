# Danh sách giải đấu

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Giải đấu            +  │
├─────────────────────────────┤
│ [Tất cả] [Đang mở] [Của tôi]│
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │ 🏆 Giải CL Quận 1     │   │
│ │ 🏸 Cầu lông • Bracket │   │
│ │ 📅 01/07 - 15/07      │   │
│ │ 👥 12/16 đã đăng ký   │   │
│ │ 💰 Đặt cọc: 100.000đ  │   │
│ │ 🟢 Đang mở đăng ký    │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ 🏆 Giải tự phát Thủ Đức│   │
│ │ 🏓 Pickleball • RR    │   │
│ │ 📅 28/06              │   │
│ │ 👥 6/8 đã đăng ký     │   │
│ │ 🆓 Miễn phí           │   │
│ │ 🟢 Đang mở            │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Nút tạo giải (+) | Action | → tournament-create |
| 2 | Tabs filter | Tab | Tất cả / Đang mở đăng ký / Giải của tôi (tạo hoặc tham gia) |
| 3 | Giải card | List | Tên, môn, format (Bracket/RR), ngày, số đăng ký/max, phí, status |
| 4 | Status badges | Info | 🟢 Đang mở / 🟡 Sắp diễn ra / 🔴 Đang đấu / ⚪ Kết thúc |
| 5 | Tap giải | Action | → tournament-detail |
| 6 | Empty state | State | "Chưa có giải đấu nào. Tạo giải đầu tiên!" |
