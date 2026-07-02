# Admin Dashboard

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Admin Dashboard         │
├─────────────────────────────┤
│ 👥 1.200   🏸 450   🏟️ 52  │
│ Users     Matches   Venues  │
│                             │
│ 💰 12.5M   📊 72%          │
│ Revenue    Occupancy        │
├─────────────────────────────┤
│ ⏰ Cần xử lý               │
│ ┌───────────────────────┐   │
│ │ 🟡 3 sân chờ duyệt    │   │
│ │ 🔴 2 dispute chờ xử lý│   │
│ │ ⚠️ 5 đánh giá bị report│   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│ Menu quản lý:               │
│  > 👥 Quản lý User         │
│  > 🏟️ Quản lý Sân         │
│  > 📋 Quản lý Booking      │
│  > 💰 Doanh thu & Báo cáo  │
│  > ⭐ Moderate đánh giá    │
│  > 🔍 Xử lý tranh chấp    │
├─────────────────────────────┤
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | KPI cards | Dashboard | Users active, matches tháng, venues active, revenue, occupancy rate.• Loading: skeleton placeholder per card• Error: "—" + retry icon per card |
| 2 | Action queue | Alerts | Sân chờ duyệt, disputes, đánh giá bị report — tap → danh sách |
| 3 | Quản lý User | Menu | Danh sách user, search, filter role/status, xem chi tiết, khóa/mở |
| 4 | Quản lý Sân | Menu | Danh sách sân, duyệt/từ chối pending, khóa/mở, xem đánh giá |
| 5 | Quản lý Booking | Menu | Danh sách booking, filter status/date/sân, xem chi tiết, xử lý dispute |
| 6 | Doanh thu | Menu | Revenue chart (commission + premium), filter thời gian, export |
| 7 | Moderate | Menu | Đánh giá flagged/reported, ẩn/xóa, cảnh báo user |
| 8 | Tranh chấp | Menu | Result conflict, booking dispute — review + quyết định |
