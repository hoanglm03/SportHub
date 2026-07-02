# Danh sách hội thoại

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Tin nhắn            ✏️  │
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │ 🟢 Nguyễn Văn A       │   │
│ │ Sân ABC hôm nay ok... │   │
│ │              14:30  2  │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ ⚪ Sân XYZ (Chủ sân)  │   │
│ │ Slot 19h còn trống... │   │
│ │              Hôm qua   │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ ⚪ Trần Thị B          │   │
│ │ GG trận đẹp!          │   │
│ │              T2         │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│  🏠    🗺️    💬    👤     │
│  Home  Map  Chat  Profile   │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Chat thread list | List | Sắp theo tin nhắn mới nhất. Avatar + tên + preview tin cuối + thời gian + badge unread |
| 2 | Online indicator | Status | 🟢 online, ⚪ offline |
| 3 | Unread badge | Badge | Số tin chưa đọc per thread |
| 4 | Nút tạo chat mới | Action | ✏️ → chọn từ contacts (Player đã match / chủ sân đã book) |
| 5 | Empty state | State | "Chưa có tin nhắn nào. Chat sẽ xuất hiện sau khi bạn match hoặc đặt sân" |
