# Cài đặt & Profile

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│  ◀  Cài đặt                │
├─────────────────────────────┤
│                             │
│     [Avatar 📷]             │
│     Nguyễn Văn A            │
│     player@email.com        │
│     ⭐ 4.3 • 42 trận       │
│     [✏️ Sửa profile]       │
│                             │
├─────────────────────────────┤
│ Tài khoản                   │
│  > Đổi mật khẩu            │
│  > Đổi email               │
│                             │
│ Riêng tư                    │
│  > Ẩn profile    [  🔘 OFF]│
│  > Ẩn vị trí    [  🔘 OFF]│
│                             │
│ Thông báo                   │
│  > Booking       [🔘   ON ]│
│  > Match         [🔘   ON ]│
│  > Chat          [🔘   ON ]│
│  > Đánh giá      [🔘   ON ]│
│  > Khuyến mãi    [  🔘 OFF]│
│                             │
│ Ví & Điểm thưởng            │
│  > 🎁 250 điểm (25.000đ)  │
│  > Xem lịch sử điểm       │
│                             │
├─────────────────────────────┤
│ [🗑️ Xóa tài khoản]        │
│                             │
│  🏠    🗺️    💬    👤     │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Profile header | Info | Avatar (tap để upload mới), tên, email, rating, tổng trận |
| 2 | Sửa profile | Action | → edit-profile: sửa tên, avatar, môn + trình độ |
| 3 | Đổi mật khẩu | Action | → form: mật khẩu cũ + mới + confirm. E-016, E-017 |
| 4 | Đổi email | Action | Nhập email mới → gửi OTP verify → cập nhật |
| 5 | Toggle ẩn profile | Setting | OFF = hiện trên matching map. ON = ẩn |
| 6 | Toggle ẩn vị trí | Setting | OFF = GPS share. ON = ẩn vị trí (không matching được) |
| 7 | Toggle noti per loại | Setting | 5 loại: booking, match, chat, đánh giá, khuyến mãi |
| 8 | Ví & Điểm thưởng | Info | Hiện tổng điểm + quy đổi VND. Tap → lịch sử |
| 9 | Xóa tài khoản | Action | Confirm 2 bước: nhập mật khẩu + "Xóa sau 30 ngày". E-018 nếu có booking pending |
