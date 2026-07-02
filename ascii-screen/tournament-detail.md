# Chi tiết giải đấu

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Giải CL Quận 1     ⋮  │
├─────────────────────────────┤
│ 🏆 Giải Cầu Lông Quận 1    │
│ 🏸 Cầu lông đôi            │
│ 📅 01/07 - 15/07/2026      │
│ 📍 Sân ABC, Q1             │
│ 🏅 Format: Bracket 16 đội  │
│ 💰 Đặt cọc: 100.000đ      │
│ 👤 Tổ chức: Admin SportHub │
│                             │
│ Mô tả: Giải giao lưu cầu  │
│ lông đôi khu vực Quận 1... │
├─────────────────────────────┤
│ [Bảng đấu] [Đăng ký] [BXH] │
├─────────────────────────────┤
│ Bảng đấu (Bracket):        │
│ ┌────┐                     │
│ │Đội A├──┐                  │
│ └────┘  ├──┐                │
│ ┌────┐  │  │                │
│ │Đội B├──┘  ├── 🏆          │
│ └────┘     │                │
│ ┌────┐  ┌──┘                │
│ │Đội C├──┤                  │
│ └────┘  │                   │
│ ┌────┐  │                   │
│ │Đội D├──┘                  │
│ └────┘                      │
├─────────────────────────────┤
│ Đã đăng ký (12/16):        │
│ 👥 Đội Pro • 👥 Đội Vui... │
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │   Đăng ký tham gia    │   │
│ └───────────────────────┘   │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Thông tin giải | Info | Tên, môn, ngày, địa điểm, format, phí, tổ chức, mô tả |
| 2 | Tabs | Tab | Bảng đấu / Đăng ký / Bảng xếp hạng |
| 3 | Bảng đấu | Visual | Bracket tree hoặc round-robin table tùy format |
| 4 | Danh sách đăng ký | List | Đội/cá nhân đã đăng ký + status (confirmed/pending cọc) |
| 5 | Nút Đăng ký | Action | → confirm đăng ký. Giải có phí → redirect payment đặt cọc. E-027 nếu đầy |
| 6 | BXH | Table | Bảng xếp hạng: thắng/thua/điểm (round-robin) hoặc progress (bracket) |
| 7 | Menu ⋮ (người tạo) | Action | Duyệt đăng ký, cập nhật kết quả, hủy giải |
| 8 | Loading | State | Skeleton khi tải bảng đấu |
