# Đăng nhập

## 1. Wireframe ASCII

```
┌─────────────────────────────┐
│                             │
│       🏸 SportHub           │
│                             │
├─────────────────────────────┤
│                             │
│  Email                      │
│  ┌───────────────────────┐  │
│  │ player@email.com      │  │
│  └───────────────────────┘  │
│                             │
│  Mật khẩu                   │
│  ┌───────────────────────┐  │
│  │ ••••••••          👁  │  │
│  └───────────────────────┘  │
│                             │
│  ┌───────────────────────┐  │
│  │      Đăng nhập        │  │
│  └───────────────────────┘  │
│                             │
│  Quên mật khẩu?            │
│                             │
│  ─── hoặc ───               │
│                             │
│  ┌───────────────────────┐  │
│  │  🔵 Đăng nhập Google  │  │
│  └───────────────────────┘  │
│                             │
│  Chưa có tài khoản?        │
│  Đăng ký ngay →             │
│                             │
└─────────────────────────────┘
```

## 2. Screen Description

| # | Element | Type | Mô tả |
|---|---------|------|-------|
| 1 | Logo app | Branding | Logo SportHub |
| 2 | Email input | Input | Email đã đăng ký. Validate format |
| 3 | Mật khẩu input | Input | Toggle show/hide 👁 |
| 4 | Nút Đăng nhập | Action | Validate → call API → thành công: redirect map-search. Sai: "Email hoặc mật khẩu không đúng" |
| 5 | Quên mật khẩu | Link | → flow reset password (dùng chung authentication feature) |
| 6 | Đăng nhập Google | Action | OAuth Google → thành công: redirect map-search |
| 7 | Link Đăng ký | Link | → register screen |
| 8 | Loading state | State | Nút Đăng nhập hiện spinner, form disabled |
| 9 | Error: sai credentials | State | "Email hoặc mật khẩu không đúng". Max 5 lần/15p (NFR-012) |
| 10 | Error: tài khoản bị khóa | State | "Tài khoản đã bị tạm khóa. Liên hệ hỗ trợ" |
