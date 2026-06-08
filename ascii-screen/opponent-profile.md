# opponent-profile

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Quay lại             │
│                         │
│       ┌─────┐           │
│       │ AVT │           │
│       └─────┘           │
│     Minh Trần           │
│     ★ 4.2 (28 trận)    │
│                         │
├─────────────────────────┤
│ Môn       Trình độ      │
│ Cầu lông  Trung bình    │
│ Pickleball Mới chơi     │
├─────────────────────────┤
│ Thống kê                │
│ Thắng: 18  Thua: 10     │
│ Tỷ lệ thắng: 64%       │
├─────────────────────────┤
│ Khoảng cách: 1.2 km     │
│ Matching Score: 87%     │
├─────────────────────────┤
│                         │
│  ┌───────────────────┐  │
│  │   MỜI ĐẤU        │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Avatar | image | • Ảnh đại diện đối thủ<br>• Default avatar nếu chưa upload |
| 2 | Tên hiển thị | static text | • Tên đối thủ |
| 3 | Rating tổng | static text | • ★ X.X (N trận)<br>• Rating trung bình từ tất cả đối thủ đã đánh giá |
| 4 | Danh sách môn + trình độ | table/list | • Mỗi row: tên môn + trình độ (Mới chơi / Trung bình / Nâng cao)<br>• Chỉ hiện môn trùng với Player (matching) |
| 5 | Thống kê win/loss | static text | • Thắng: N, Thua: M<br>• Tỷ lệ thắng: X%<br>• Ref: FR-sport-matching-012 |
| 6 | Khoảng cách | static text | • X.X km từ vị trí Player hiện tại |
| 7 | Matching Score | static text | • X% tương thích<br>• Ref: BR-sport-matching-001 |
| 8 | Nút Mời đấu | button primary | • Tap: chuyển court-select<br>• Disabled nếu có match pending (E-sport-matching-004)<br>• Disabled nếu hết limit invite (E-sport-matching-005) |
| 9 | Nút Quay lại | icon back | • Quay về map-search |
