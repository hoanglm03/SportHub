# Tìm sân

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Tìm sân            🔍  │
├─────────────────────────────┤
│ ┌─────┐ ┌─────┐ ┌────────┐ │
│ │Cầu  │ │Pickle│ │Tennis  │ │
│ │lông ✓│ │ball  │ │        │ │
│ └─────┘ └─────┘ └────────┘ │
├─────────────────────────────┤
│ 📍 Quận 1, 3km  📅 24/06   │
│ 💰 100k - 300k/h           │
├─────────────────────────────┤
│ ┌───────────────────────┐   │
│ │ 📷 Sân ABC            │   │
│ │ ⭐ 4.5 (120 đánh giá) │   │
│ │ 📍 1.2km • 150k/h     │   │
│ │ 🟢 5 slot trống hôm nay│   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ 📷 Sân XYZ            │   │
│ │ ⭐ 4.2 (85 đánh giá)  │   │
│ │ 📍 2.5km • 200k/h     │   │
│ │ 🟢 3 slot trống hôm nay│   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ 📷 Sân DEF            │   │
│ │ ⭐ 3.8 (42 đánh giá)  │   │
│ │ 📍 4.1km • 120k/h     │   │
│ │ 🔴 Hết slot hôm nay   │   │
│ └───────────────────────┘   │
├─────────────────────────────┤
│  🏠    🗺️    🔍    👤     │
│  Home  Map  Search Profile  │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Môn thể thao chips | Filter | Chip chọn môn (multi-select). Môn đang chọn có ✓ |
| 2 | Khu vực | Filter | Hiện vị trí GPS hiện tại + bán kính. Tap để đổi |
| 3 | Ngày | Filter | Mặc định hôm nay. Tap chọn ngày (max 14 ngày) |
| 4 | Khoảng giá | Filter | Slider hoặc preset ranges |
| 5 | Danh sách sân | List | Card mỗi sân: ảnh, tên, rating, khoảng cách, giá/h, slot trống.• Tap → venue-detail• Sân hết slot hiện 🔴, vẫn xem được chi tiết |
| 6 | Empty state | State | "Không tìm thấy sân phù hợp. Thử mở rộng bộ lọc hoặc chọn ngày khác" |
| 7 | Loading | State | Skeleton cards khi đang tải |
| 8 | Bottom nav | Nav | Tab chính app: Home, Map, Search, Profile |
