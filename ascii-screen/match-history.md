# match-history

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Lịch sử trận đấu     │
│                         │
│  Tổng: 28 trận          │
│  Thắng: 18 | Thua: 10   │
│  Tỷ lệ: 64%            │
│                         │
│  Môn: [Tất cả ▼]        │
├─────────────────────────┤
│ 04/06 | Sân ABC | 18:00 │
│ vs Minh T. | ★4 | Thắng │
│ [Đánh giá]              │
├─────────────────────────┤
│ 02/06 | Sân XYZ | 19:00 │
│ vs Hà N.  | ★3 | Thua   │
│ Đã đánh giá ✓           │
├─────────────────────────┤
│ 30/05 | Sân DEF | 17:00 │
│ vs Long P. | ★5 | Thắng │
│ Đã đánh giá ✓           │
├─────────────────────────┤
│ ...xem thêm              │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Thống kê tổng | static card | • Tổng trận + Thắng + Thua + Tỷ lệ thắng %<br>• Tính theo filter môn hiện tại<br>• Ref: FR-sport-matching-012 |
| 2 | Filter môn | dropdown | • Options: Tất cả + danh sách môn Player đã chơi<br>• Default: Tất cả |
| 3 | Danh sách trận | scrollable list | • Mới nhất trước<br>• Mỗi row: ngày / sân / giờ / vs đối thủ / rating đã cho / kết quả (Thắng/Thua)<br>• Pagination hoặc infinite scroll |
| 4 | Nút Đánh giá | text link per row | • Hiện nếu chưa đánh giá trận đó<br>• Tap: chuyển rate-opponent<br>• Đã đánh giá: hiện "Đã đánh giá ✓" (disabled) |
| 5 | Empty state | illustration + text | • Khi chưa có trận: "Chưa có trận đấu nào. Hãy tìm đối thủ!" |
| 6 | Nút Quay lại | icon back | • Quay về map-search |
