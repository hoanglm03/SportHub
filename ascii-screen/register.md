# register

## 1. Wireframe

```
┌─────────────────────────┐
│      SPORT MATCHING     │
│                         │
│  ┌───────────────────┐  │
│  │ Email             │  │
│  └───────────────────┘  │
│                         │
│  ┌───────────────────┐  │
│  │ Mật khẩu     [👁] │  │
│  └───────────────────┘  │
│                         │
│  ┌───────────────────┐  │
│  │ Tên hiển thị      │  │
│  └───────────────────┘  │
│                         │
│  ┌───────────────────┐  │
│  │    ĐĂNG KÝ        │  │
│  └───────────────────┘  │
│                         │
│  Đã có tài khoản?      │
│  [Đăng nhập]            │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Email | text input | • Bắt buộc<br>• Format email hợp lệ<br>• Placeholder: "Nhập email"<br>• Ref: FR-sport-matching-001 |
| 2 | Mật khẩu | password input | • Bắt buộc<br>• Toggle hiện/ẩn (icon mắt)<br>• Placeholder: "Nhập mật khẩu" |
| 3 | Tên hiển thị | text input | • Bắt buộc<br>• Placeholder: "Tên hiển thị trên app" |
| 4 | Nút Đăng ký | button primary | • Disabled khi chưa fill đủ 3 trường<br>• Tap: gửi POST /register, chuyển otp-verify<br>• Error email trùng: hiện toast lỗi |
| 5 | Link Đăng nhập | text link | • Chuyển sang màn đăng nhập (nếu đã có account) |
