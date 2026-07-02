# UC: Thanh toán online (uc-payment)

## a. Mục đích

Player thanh toán tiền đặt sân trực tiếp trên app qua MoMo hoặc VNPay thay vì trả tại sân. System thu commission 12% trên tổng giá trị, chuyển phần còn lại cho Partner.

## b. Actors

- **Player** — người thực hiện thanh toán
- **Payment Gateway** (MoMo / VNPay) — cổng thanh toán bên ngoài
- **System** — xử lý xác nhận giao dịch, cập nhật booking, idempotency

## c. Pre-conditions

- Player đã chọn sân + slot, booking ở trạng thái `pending_payment`
- Tích hợp MoMo/VNPay đã active (CAP-08, P1)
- Player có tài khoản MoMo hoặc VNPay (hoặc thẻ ngân hàng)

## d. Expected result

**Luồng chính:**
1. Player trên màn `payment-checkout`, chọn MoMo hoặc VNPay
2. System tạo payment request với idempotency key, redirect Player sang app/deeplink cổng thanh toán
3. Player hoàn tất thanh toán trên cổng
4. Cổng callback System xác nhận giao dịch thành công
5. System cập nhật booking → `paid`, trích commission 12%, gửi notification cho Player + Partner
6. Player redirect về `booking-detail` với badge "Đã thanh toán"

**Alternate — Thanh toán thất bại:**
- Cổng trả về failed → System giữ booking `pending_payment`, cho phép retry
- Nếu timeout 60s chưa có callback → E-sport-matching-022, Player có thể thử lại

**Alternate — Mất mạng giữa chừng:**
- System giữ slot locked, idempotency key đảm bảo không duplicate charge khi retry
- Khi mạng lại, Player có thể tiếp tục hoặc chọn lại cổng

## e. Activity diagram

Không bắt buộc (flow tuyến tính + 2 alternate paths — sequence diagram trong flows.md đủ).

## f. Screens involved

- `payment-checkout` — chọn cổng + xác nhận thanh toán
- `booking-detail` — kết quả sau thanh toán

## g. FR map

| FR | Mô tả |
|----|-------|
| FR-sport-matching-013 | Thanh toán online MoMo/VNPay, commission 12% |

## h. Open Questions

Không có OQ mở.
