# map-search

## 1. Wireframe

```
┌─────────────────────────┐
│ [≡]  Sport Matching  [👤]│
├─────────────────────────┤
│ Môn:[Cầu lông ▼]        │
│ Trình độ:[Tất cả ▼]     │
│ Bán kính:[3km ▼]        │
├─────────────────────────┤
│                         │
│    ┌───┐                │
│    │ 📍│ ← Bạn          │
│    └───┘                │
│         ┌───┐           │
│  ┌───┐  │🏸 │           │
│  │🏸 │  └───┘           │
│  └───┘      ┌───┐       │
│             │🏟️ │       │
│             └───┘       │
│                         │
├─────────────────────────┤
│ Đối thủ gần bạn (3)     │
│ ┌─────────────────────┐ │
│ │ Minh T. | TB | ★4.2 │ │
│ │ 1.2km  | Cầu lông   │ │
│ ├─────────────────────┤ │
│ │ Hà N.  | MC | ★3.8  │ │
│ │ 2.5km  | Cầu lông   │ │
│ ├─────────────────────┤ │
│ │ Long P. | NC | ★4.5 │ │
│ │ 4.1km  | Cầu lông   │ │
│ └─────────────────────┘ │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Header | nav bar | • Logo/tên app giữa<br>• Hamburger menu trái (≡)<br>• Avatar profile phải (👤) chuyển player-profile |
| 2 | Filter: Môn | dropdown | • Danh sách môn Player đã đăng ký<br>• Bắt buộc chọn 1 môn<br>• Default: môn đầu tiên trong profile |
| 3 | Filter: Trình độ | dropdown | • Options: Tất cả / Mới chơi / Trung bình / Nâng cao<br>• Default: Tất cả<br>• Lọc đối thủ theo trình độ |
| 4 | Filter: Bán kính | dropdown | • Options: 3km / 5km / 10km / 20km / 50km<br>• Default: 3km (BR-sport-matching-001)<br>• Max: 50km |
| 5 | Bản đồ | map view | • Google Maps/Mapbox<br>• Center: vị trí GPS Player<br>• Markers: đối thủ (icon môn) + sân (icon sân)<br>• Tap marker: hiện mini popup (tên + trình độ + rating)<br>• Ref: FR-sport-matching-005 |
| 6 | Danh sách đối thủ | scrollable list | • Overlay bottom sheet (kéo lên/xuống)<br>• Mỗi row: **tên** / trình độ viết tắt (MC/TB/NC) / ★rating / khoảng cách / môn<br>• Sorted by Matching Score giảm dần<br>• Tap row: chuyển opponent-profile<br>• Ref: FR-sport-matching-004 |
| 7 | Error states | toast/modal | • GPS OFF: E-sport-matching-001 (modal yêu cầu bật)<br>• Không tìm thấy: E-sport-matching-006 (inline message + gợi ý filter)<br>• Match pending: E-sport-matching-004 (toast)<br>• Hết limit: E-sport-matching-005 (toast + link Premium)<br>• Cooldown hủy: E-sport-matching-009 (toast "Vui lòng đợi {mm:ss} trước khi tạo trận mới")<br>• Maps unavailable: E-sport-matching-021 (fallback list view) |
