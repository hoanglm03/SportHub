# Social Feed

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Cộng đồng           ✏️ │
├─────────────────────────────┤
│ [Following] [Khám phá]      │
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │ 👤 Hoàng • 2 giờ trước│   │
│ │                       │   │
│ │ Trận đẹp hôm nay!    │   │
│ │ 🏸 Thắng 21-15 vs Minh│   │
│ │ ┌─────────────────┐   │   │
│ │ │ [📷 Ảnh trận]   │   │   │
│ │ └─────────────────┘   │   │
│ │ ❤️ 24  💬 5  🔗 Share │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ 👤 Lan • Hôm qua      │   │
│ │                       │   │
│ │ Sân mới khu Thủ Đức   │   │
│ │ rất đẹp, recommend!   │   │
│ │ ┌─────────────────┐   │   │
│ │ │ [🎥 Video 0:25] │   │   │
│ │ └─────────────────┘   │   │
│ │ ❤️ 42  💬 12  🔗      │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Nút đăng bài (✏️) | Action | → post-create: text + ảnh (max 5) + video (max 1, ≤30s) |
| 2 | Tabs | Tab | Following (bài từ người mình follow) / Khám phá (trending/gợi ý) |
| 3 | Post card | Card | Avatar + tên + thời gian + nội dung text + media + like/comment count |
| 4 | Match result card | Card | Auto-generate từ kết quả trận: môn, score, đối thủ. Player chọn share |
| 5 | Like | Action | ❤️ toggle like/unlike. Count update real-time |
| 6 | Comment | Action | 💬 tap → expand comment list. Nhập comment (max 500). Reply |
| 7 | Follow indicator | Info | Tap avatar/tên → opponent-profile. Nút Follow/Unfollow |
| 8 | Report bài | Action | Long press hoặc menu ⋮ → "Báo cáo bài viết". E-028 nếu bị ẩn |
| 9 | Empty state | State | Following empty: "Follow người chơi khác để xem bài viết!" |
| 10 | Loading | State | Skeleton cards khi tải feed |
