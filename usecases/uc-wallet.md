# UC: Ví nội bộ (uc-wallet)

## a. Mục đích

Player quản lý In-app Wallet: xem số dư, nạp tiền, rút tiền, và nhận hoàn tiền dạng điểm thưởng khi hủy trận/booking. Mục tiêu: giữ tiền trong hệ thống, giảm refund fee qua ngân hàng.

## b. Actors

- **Player** — chủ sở hữu ví
- **System** — xử lý giao dịch, cập nhật số dư, hoàn tiền tự động
- **Payment Gateway** (MoMo/VNPay) — kênh nạp/rút tiền thực

## c. Pre-conditions

- Player đã đăng nhập (role: Player)
- Ví được khởi tạo tự động khi tạo account (số dư ban đầu = 0)
- CAP-11 (P1) đã active

## d. Expected result

**Luồng xem số dư:**
1. Player mở màn `wallet`, thấy số dư hiện tại + lịch sử giao dịch (nạp/rút/hoàn tiền/điểm thưởng)

**Luồng nạp tiền:**
1. Player nhấn "Nạp tiền", nhập số tiền, chọn MoMo/VNPay
2. Redirect sang cổng, thanh toán thành công
3. Số dư ví tăng đúng số tiền nạp, hiện giao dịch mới trong lịch sử

**Luồng rút tiền:**
1. Player nhấn "Rút tiền", nhập số tiền (≤ số dư), chọn tài khoản nhận
2. System xử lý, số dư giảm, tiền về tài khoản trong 1-3 ngày làm việc

**Luồng nhận hoàn tiền tự động:**
1. Khi hủy booking/trận đủ điều kiện, System tự chuyển tiền hoàn vào ví
2. Player thấy giao dịch "Hoàn tiền — Hủy booking #XYZ" trong lịch sử

## e. Activity diagram

Không bắt buộc.

## f. Screens involved

- `wallet` — màn hình ví chính: số dư + lịch sử + nạp/rút
- `settings` — entry point truy cập ví từ menu cài đặt

## g. FR map

| FR | Mô tả |
|----|-------|
| FR-sport-matching-016 | Ví điện tử nội bộ: số dư, nạp, rút, hoàn tiền dạng điểm thưởng |
| FR-sport-matching-041 | Điểm thưởng từ đánh giá dùng giảm giá — hiển thị trong ví |

## h. Open Questions

Không có OQ mở.
