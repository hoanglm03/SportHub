# rate-opponent

## 1. Wireframe

```
┌─────────────────────────┐
│  ← Đánh giá đối thủ     │
│                         │
│       ┌─────┐           │
│       │ AVT │           │
│       └─────┘           │
│     Minh Trần           │
│  Trận: 04/06 18:00      │
│  Sân ABC | Cầu lông     │
│                         │
│  Đánh giá:              │
│  ★ ★ ★ ★ ☆              │
│                         │
│  ┌───────────────────┐  │
│  │ Nhận xét (tuỳ     │  │
│  │ chọn)...           │  │
│  │                    │  │
│  └───────────────────┘  │
│                         │
│  ┌───────────────────┐  │
│  │  GỬI ĐÁNH GIÁ    │  │
│  └───────────────────┘  │
│                         │
│  [Bỏ qua]               │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Thông tin đối thủ | static card | • Avatar + tên đối thủ<br>• Thông tin trận: ngày/giờ + sân + môn |
| 2 | Rating stars | star picker (1-5) | • Bắt buộc chọn ≥1 sao<br>• Tap sao thứ N: chọn N sao<br>• Ref: FR-sport-matching-011 |
| 3 | Nhận xét | textarea | • Optional<br>• Placeholder: "Nhận xét (tuỳ chọn)..."<br>• Max 500 ký tự |
| 4 | Nút Gửi đánh giá | button primary | • Disabled khi chưa chọn star<br>• Tap: submit rating, hiện toast "Cảm ơn bạn đã đánh giá!"<br>• Quay về match-history |
| 5 | Link Bỏ qua | text link | • Skip đánh giá, quay về match-history<br>• Hệ thống nhắc lại sau |
| 6 | Nút Quay lại | icon back | • Quay về match-history |
