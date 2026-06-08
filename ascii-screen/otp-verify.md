# otp-verify

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Quay lại             │
│                         │
│   Xác thực Email        │
│   OTP đã gửi tới        │
│   h***@gmail.com        │
│                         │
│  ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐│
│  │  │ │  │ │  │ │  │ │  │ │  ││
│  └──┘ └──┘ └──┘ └──┘ └──┘ └──┘│
│                         │
│   Hết hạn sau: 04:32    │
│                         │
│  ┌───────────────────┐  │
│  │    XÁC NHẬN       │  │
│  └───────────────────┘  │
│                         │
│  Chưa nhận? [Gửi lại]  │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Email masked | static text | • Hiện email đã đăng ký, mask giữa (vd: h***@gmail.com)<br>• Không editable |
| 2 | OTP input | 6 digit boxes | • Bắt buộc, 6 ô số<br>• Auto-focus ô tiếp theo khi nhập<br>• Ref: FR-sport-matching-001 |
| 3 | Countdown timer | static text | • Đếm ngược từ 5:00<br>• Hết hạn: disable nút Xác nhận, enable Gửi lại |
| 4 | Nút Xác nhận | button primary | • Disabled khi chưa fill đủ 6 số<br>• Tap: verify OTP, thành công chuyển profile-setup<br>• OTP sai: hiện toast "OTP không đúng" |
| 5 | Link Gửi lại | text link | • Disabled trong countdown<br>• Enable khi hết hạn hoặc sau 60s<br>• Tap: gửi OTP mới, reset countdown |
| 6 | Nút Quay lại | icon back | • Quay về register, giữ data đã nhập |
