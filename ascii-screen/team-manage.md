# Quản lý đội

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Đội của tôi         +  │
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │ 🏸 Đội Cầu Lông Pro   │   │
│ │ 👑 Captain: Bạn       │   │
│ │ 👥 3/4 thành viên     │   │
│ │ [Tìm trận] [Quản lý]  │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ 🏓 Pickleball Squad   │   │
│ │ 👤 Thành viên         │   │
│ │ 👥 2/2                │   │
│ │ [Rời đội]             │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│ Thành viên (Đội Cầu Lông): │
│  👑 Hoàng ⭐4.3 Nâng cao  │
│  👤 Minh   ⭐3.8 TB       │
│  👤 Lan    ⭐4.1 TB       │
│  [+ Mời thêm thành viên]   │
├─────────────────────────────┤
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Nút tạo đội (+) | Action | Nhập tên đội + chọn môn → tạo, mình là Captain |
| 2 | Danh sách đội | List | Đội mình là Captain (👑) hoặc thành viên (👤). Hiện số người |
| 3 | Nút Tìm trận | Action | Chỉ Captain. Ghép random vs đội khác. E-026 nếu < 2 người |
| 4 | Nút Quản lý | Action | Captain: mời/xóa thành viên, đổi tên, giải tán |
| 5 | Nút Rời đội | Action | Thành viên rời đội (không phải Captain) |
| 6 | Danh sách thành viên | List | Tên + rating + trình độ. Captain có icon 👑 |
| 7 | Mời thành viên | Action | Search player theo tên/ID → gửi invite vào đội |
| 8 | Empty state | State | "Bạn chưa có đội nào. Tạo đội mới!" |
