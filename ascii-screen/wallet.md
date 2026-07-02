# wallet

## 1. Wireframe

```
┌─────────────────────────┐
│  ←  Ví của tôi          │
├─────────────────────────┤
│                         │
│  ┌─────────────────────┐│
│  │   💰 Số dư ví        ││
│  │   125.000 đ          ││
│  │   + 850 điểm thưởng  ││
│  ├─────────────────────┤│
│  │  [NẠP TIỀN] [RÚT]  ││
│  └─────────────────────┘│
│                         │
│  Lịch sử giao dịch      │
│                         │
│  ┌─────────────────────┐│
│  │ ↑ Nạp tiền          ││
│  │ +200.000đ           ││
│  │ 25/06/2026 · MoMo   ││
│  ├─────────────────────┤│
│  │ ↓ Hoàn tiền         ││
│  │ +75.000đ            ││
│  │ 24/06/2026 · Hủy    ││
│  │   booking #B-042    ││
│  ├─────────────────────┤│
│  │ ↓ Thanh toán sân    ││
│  │ -150.000đ           ││
│  │ 23/06/2026 · Sân ABC││
│  ├─────────────────────┤│
│  │ ★ Điểm thưởng       ││
│  │ +50 điểm            ││
│  │ 22/06/2026 · Đánh   ││
│  │   giá sân ABC       ││
│  └─────────────────────┘│
│                         │
└─────────────────────────┘
```

## 2. Screen description

| # | Items | Data type | Description |
|---|-------|-----------|-------------|
| 1 | Header + back | navigation | • "← Ví của tôi"<br>• Back → settings |
| 2 | Số dư ví | balance card | • Số dư tiền (đ) bold lớn<br>• Điểm thưởng tích lũy (★ NNN điểm)<br>• Ref: FR-sport-matching-016, FR-041 |
| 3 | Nút Nạp tiền | button primary | • Tap → flow nạp: nhập số tiền → chọn cổng → thanh toán<br>• Phụ thuộc CAP-08 (thanh toán online P1) |
| 4 | Nút Rút tiền | button secondary | • Tap → flow rút: nhập số tiền + tài khoản nhận → xác nhận<br>• Disable nếu số dư = 0 |
| 5 | Danh sách giao dịch | list | • Mỗi item: loại (↑ nạp / ↓ rút/thanh toán / ★ điểm) + số tiền/điểm + ngày + nguồn<br>• Color: xanh lá = tiền vào, đỏ = tiền ra, vàng = điểm<br>• Vô hạn scroll (load more) |
| 6 | Empty state | state | • Khi ví mới tạo chưa có giao dịch: "Chưa có giao dịch nào. Nạp tiền để bắt đầu!" |
| 7 | Loading state | state | • Skeleton loader khi đang load lịch sử |
