# profile-setup

## 1. Wireframe

```
┌─────────────────────────┐
│  Thiết lập hồ sơ        │
│                         │
│  Chọn môn yêu thích:    │
│  ┌─────────────────────┐│
│  │ [✓] Cầu lông        ││
│  │ [ ] Pickleball       ││
│  │ [ ] Tennis           ││
│  │ [ ] Bóng bàn         ││
│  │ [ ] Bóng đá          ││
│  │ ...xem thêm          ││
│  └─────────────────────┘│
│                         │
│  Trình độ Cầu lông:     │
│  (●) Mới chơi           │
│  ( ) Trung bình          │
│  ( ) Nâng cao            │
│                         │
│  ┌───────────────────┐  │
│  │    HOÀN TẤT       │  │
│  └───────────────────┘  │
│                         │
│  Đã chọn: 1/5 môn      │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Danh sách môn | checkbox list | • Hiện tất cả môn trong hệ thống<br>• Bắt buộc chọn ≥1<br>• Tối đa 5 môn ưu tiên hiển thị trên profile<br>• Ref: FR-sport-matching-002 |
| 2 | Trình độ per môn | radio group (3 options) | • Hiện cho mỗi môn đã chọn<br>• 3 bậc: **Mới chơi** / **Trung bình** / **Nâng cao**<br>• Bắt buộc chọn 1 bậc per môn<br>• Ref: BR-sport-matching-007 |
| 3 | Counter môn đã chọn | static text | • Hiện "Đã chọn: X/5 môn"<br>• Warn khi vượt 5: "Chỉ 5 môn đầu hiển thị nổi bật" |
| 4 | Nút Hoàn tất | button primary | • Disabled khi chưa chọn ≥1 môn + trình độ<br>• Tap: save profile, chuyển map-search |
| 5 | Loading state | state | • Nút Hoàn tất hiện spinner khi save profile |
