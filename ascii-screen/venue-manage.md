# Quản lý sân (Chủ sân)

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Quản lý sân            │
├─────────────────────────────┤
│                             │
│  ┌───────────────────────┐  │
│  │  + Đăng sân mới       │  │
│  └───────────────────────┘  │
│                             │
├─────────────────────────────┤
│ Sân của bạn:                │
│                             │
│ ┌───────────────────────┐   │
│ │ 🏸 Sân ABC            │   │
│ │ ✅ Đang hoạt động      │   │
│ │ 📅 Hôm nay: 3 booking  │   │
│ │ 🔔 1 chờ duyệt         │   │
│ └───────────────────────┘   │
│                             │
│ ┌───────────────────────┐   │
│ │ 🏸 Sân XYZ            │   │
│ │ 🟡 Chờ duyệt          │   │
│ │ Đã submit 2 ngày trước │   │
│ └───────────────────────┘   │
│                             │
├─────────────────────────────┤
│  Booking chờ duyệt (1)     │
│ ┌───────────────────────┐   │
│ │ Nguyễn Văn A          │   │
│ │ Sân B • 19:00 24/06   │   │
│ │ 200.000đ  ⏱️ 25:00    │   │
│ │ [✅ Duyệt] [❌ Từ chối]│   │
│ └───────────────────────┘   │
│                             │
├─────────────────────────────┤
│  🏠    🗺️    🔍    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Nút Đăng sân mới | Action | → venue-register (form đăng sân) |
| 2 | Danh sách sân | List | Card mỗi sân: tên, status (active/pending/suspended/inactive), số booking hôm nay, badge chờ duyệt.• Tap → chi tiết quản lý sân (lịch, block giờ, sửa thông tin) |
| 3 | Status badges | Info | • ✅ Đang hoạt động (active)• 🟡 Chờ duyệt (pending_review)• ❌ Bị từ chối (rejected) + lý do• 🔒 Tạm khóa (suspended)• ⏸️ Tạm đóng (inactive) |
| 4 | Booking chờ duyệt | Section | List booking paid chờ duyệt.• Mỗi card: tên player, sân con, giờ, giá, countdown 30p• Nút Duyệt / Từ chối• Countdown hết → auto hủy |
| 5 | Empty state | State | "Bạn chưa có sân nào. Đăng sân đầu tiên!" |
| 6 | Noti badge | Badge | Số booking chờ duyệt hiện trên icon 🔔 |
