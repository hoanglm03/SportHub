# Onboarding chủ sân

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Đăng ký chủ sân        │
├─────────────────────────────┤
│                             │
│  Bước 1/3: Thông tin        │
│  ┌───────────────────────┐  │
│  │ Tên doanh nghiệp/cá  │  │
│  │ nhân                  │  │
│  └───────────────────────┘  │
│  ┌───────────────────────┐  │
│  │ Số điện thoại         │  │
│  └───────────────────────┘  │
│  ┌───────────────────────┐  │
│  │ Địa chỉ               │  │
│  └───────────────────────┘  │
│                             │
│  Bước 2/3: Giấy tờ         │
│  ┌───────────────────────┐  │
│  │ 📷 Upload CMND/CCCD   │  │
│  │    (mặt trước + sau)  │  │
│  └───────────────────────┘  │
│  ┌───────────────────────┐  │
│  │ 📷 Giấy phép KD       │  │
│  │    (nếu có)           │  │
│  └───────────────────────┘  │
│                             │
│  Bước 3/3: Điều khoản      │
│  ☐ Tôi đồng ý Điều khoản  │
│    sử dụng và Chính sách   │
│    hoa hồng 12%             │
│                             │
│  ┌───────────────────────┐  │
│  │    Gửi đăng ký        │  │
│  └───────────────────────┘  │
│                             │
│  Status: Đang xét duyệt 🟡 │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Step indicator | Progress | 3 bước: Thông tin → Giấy tờ → Điều khoản |
| 2 | Thông tin cá nhân/DN | Form | Tên, SĐT, địa chỉ. Bắt buộc |
| 3 | Upload CMND/CCCD | Upload | Mặt trước + sau. Ảnh JPG/PNG, max 5MB |
| 4 | Upload giấy phép KD | Upload | Tùy chọn (cá nhân không cần). Ảnh JPG/PNG |
| 5 | Checkbox điều khoản | Confirm | Bắt buộc tick. Link xem full T&C |
| 6 | Nút Gửi | Action | Validate → submit → status pending. Noti Admin |
| 7 | Status tracking | Info | Đang xét duyệt 🟡 / Đã duyệt ✅ / Từ chối ❌ + lý do |
| 8 | Error: E-019 | State | Thiếu CMND hoặc giấy phép |
