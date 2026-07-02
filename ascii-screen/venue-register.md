# Đăng sân mới (Chủ sân)

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Đăng sân mới           │
├─────────────────────────────┤
│                             │
│  Tên sân *                  │
│  ┌───────────────────────┐  │
│  │ VD: Sân cầu lông ABC │  │
│  └───────────────────────┘  │
│                             │
│  Địa chỉ *                  │
│  ┌───────────────────────┐  │
│  │ 123 Nguyễn Huệ, Q1   │  │
│  └───────────────────────┘  │
│  📍 Chọn vị trí trên bản đồ│
│                             │
│  Môn thể thao *             │
│  ☑ Cầu lông  ☑ Pickleball  │
│  ☐ Tennis    ☐ Bóng bàn    │
│                             │
│  Giá / giờ *                │
│  ┌───────────────────────┐  │
│  │ 150.000 VND           │  │
│  └───────────────────────┘  │
│                             │
│  Khung giờ hoạt động *      │
│  ┌──────┐ — ┌──────┐       │
│  │06:00 │   │22:00 │       │
│  └──────┘   └──────┘       │
│                             │
│  Tiện ích                   │
│  ☑ Bãi xe  ☑ Nước uống    │
│  ☑ Phòng thay đồ  ☐ Wifi  │
│                             │
│  Hình ảnh * (tối thiểu 3)  │
│  ┌────┐ ┌────┐ ┌────┐     │
│  │ 📷 │ │ 📷 │ │ +  │     │
│  │ 1  │ │ 2  │ │add │     │
│  └────┘ └────┘ └────┘     │
│  2/3 tối thiểu             │
│                             │
│  Sân con *                  │
│  ┌───────────────────────┐  │
│  │ + Thêm sân con        │  │
│  │ Sân A  [✏️] [🗑️]      │  │
│  │ Sân B  [✏️] [🗑️]      │  │
│  └───────────────────────┘  │
│                             │
│  ┌───────────────────────┐  │
│  │    Gửi đăng ký sân    │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Tên sân | Input | Bắt buộc, 5-100 ký tự |
| 2 | Địa chỉ + bản đồ | Input + Map | Nhập text + chọn pin trên bản đồ (lấy tọa độ) |
| 3 | Môn thể thao | Checkbox | Multi-select, ≥1 bắt buộc |
| 4 | Giá/giờ | Input number | Bắt buộc, số dương, VND |
| 5 | Khung giờ | Time picker | Giờ mở - giờ đóng |
| 6 | Tiện ích | Checkbox | Multi-select, optional |
| 7 | Hình ảnh | Upload | Min 3, max 10, max 5MB/tấm. Counter hiện X/3 tối thiểu. Validate trước submit |
| 8 | Sân con | List + Add | ≥1 sân con bắt buộc. Thêm/sửa tên/xóa |
| 9 | Nút Submit | Action | Validate tất cả → submit → pending_review. Noti Admin |
| 10 | Loading | State | Spinner khi upload ảnh + submit |
| 11 | Validation errors | State | Inline per field: thiếu field bắt buộc, < 3 ảnh, giá <= 0 |
