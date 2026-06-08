# player-profile

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Hồ sơ cá nhân  [✏️]  │
│                         │
│       ┌─────┐           │
│       │ AVT │           │
│       └─────┘           │
│     Hoàng Lê            │
│     h***@gmail.com      │
│                         │
├─────────────────────────┤
│ Môn thể thao            │
│ ┌─────────────────────┐ │
│ │ Cầu lông   | TB     │ │
│ │ ★ 4.2 | 18W 10L     │ │
│ ├─────────────────────┤ │
│ │ Pickleball  | MC     │ │
│ │ ★ 3.5 | 5W 3L       │ │
│ └─────────────────────┘ │
├─────────────────────────┤
│ Rating tổng: ★ 4.0      │
│ Tổng trận: 36           │
├─────────────────────────┤
│ Thành viên từ: 01/2026  │
│                         │
│ [Đăng xuất]             │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Avatar | image | • Ảnh đại diện, tap để đổi (upload) |
| 2 | Tên + email | static text | • Tên hiển thị + email masked |
| 3 | Nút Sửa | icon edit (✏️) | • Tap: chuyển sang edit mode (sửa tên, avatar)<br>• Không cho sửa email (identifier chính) |
| 4 | Danh sách môn + trình độ | list card | • Mỗi row: **tên môn** / trình độ viết tắt (MC/TB/NC) / ★rating per môn / W-L record<br>• Tap row: option sửa trình độ (manual)<br>• Ref: FR-sport-matching-002 |
| 5 | Rating tổng | static text | • ★ X.X trung bình tất cả môn |
| 6 | Tổng trận | static text | • Tổng số trận đã chơi |
| 7 | Ngày tham gia | static text | • "Thành viên từ: MM/YYYY" |
| 8 | Nút Đăng xuất | text link (red) | • Tap: confirm dialog "Đăng xuất?", logout |
