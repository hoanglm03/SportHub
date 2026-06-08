# court-select

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Chọn sân + giờ       │
│                         │
│  Đối thủ: Minh T. (TB)  │
│  Môn: Cầu lông          │
│                         │
│ ┌─────────────────────┐ │
│ │ 🏟️ Sân ABC          │ │
│ │ 0.8km | Cầu lông    │ │
│ │                     │ │
│ │ 17:00 18:00 19:00   │ │
│ │ [150k] [150k] [---] │ │
│ │ 20:00 21:00         │ │
│ │ [200k] [200k]       │ │
│ ├─────────────────────┤ │
│ │ 🏟️ Sân XYZ          │ │
│ │ 2.1km | Cầu lông    │ │
│ │                     │ │
│ │ 17:00 18:00 19:00   │ │
│ │ [120k] [---] [120k] │ │
│ └─────────────────────┘ │
│                         │
│  Đã chọn: Sân ABC 18:00 │
│  Giá: 150.000đ          │
│                         │
│  ┌───────────────────┐  │
│  │    TIẾP TỤC       │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Thông tin đối thủ | static text | • Tên + trình độ đối thủ đã chọn<br>• Môn thể thao |
| 2 | Danh sách sân | scrollable list | • Sân gần nhất trước, filter theo môn hỗ trợ<br>• Mỗi sân: **tên** + khoảng cách + môn<br>• Ref: FR-sport-matching-006 |
| 3 | Grid slot giờ | button grid | • Hiện slot theo giờ (17:00, 18:00...)<br>• Slot trống: hiện giá, tap chọn<br>• Slot hết: hiện `---`, disabled<br>• Slot đang lock: hiện `---`, disabled<br>• Highlight slot đã chọn |
| 4 | Tóm tắt đã chọn | static text | • Sân + giờ + giá<br>• Hiện sau khi Player chọn slot |
| 5 | Nút Tiếp tục | button primary | • Disabled khi chưa chọn slot<br>• Tap: chuyển invite-confirm<br>• Slot bị lock bởi người khác: E-sport-matching-007 |
| 6 | Nút Quay lại | icon back | • Quay về opponent-profile |
