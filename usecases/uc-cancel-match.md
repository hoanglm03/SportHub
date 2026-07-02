# UC: Hủy trận + Hoàn tiền (uc-cancel-match)

## a. Mục đích

Player hủy trận đấu đã confirm. System áp dụng ma trận hoàn tiền 3 bậc theo thời gian còn lại trước giờ chơi và chuyển tiền hoàn vào Ví nội bộ. Giới hạn 3 lần hủy/tháng, cooldown 15 phút nếu hủy liên tiếp.

## b. Actors

- **Player** — người yêu cầu hủy trận
- **System** — kiểm tra điều kiện, tính hoàn tiền, cập nhật match + slot, notify
- **Partner (chủ sân)** — nhận đền bù theo ma trận

## c. Pre-conditions

- Match đang ở trạng thái `confirmed`
- Player chưa vượt 3 lần hủy/tháng (BR-010)
- CAP-13 (P2) đã active; Ví nội bộ (CAP-11) đã active để nhận hoàn tiền

## d. Expected result

**Luồng chính (hủy >24h — hoàn 100%):**
1. Player mở `match-confirmed`, nhấn "Hủy trận"
2. System hiện confirm dialog: "Hủy trận? Còn {N}/3 lượt tháng này. Hoàn 100% vào Ví."
3. Player xác nhận → System hủy match, release slot, hoàn 100% vào Ví Player
4. Đối thủ nhận notification "Đối thủ đã hủy trận"

**Alternate — Hủy 6–24h (hoàn 50%):**
- Confirm dialog hiện: "Hoàn 50% vào Ví. Chủ sân nhận đền bù 40%."
- Kết quả: Player nhận 50%, Partner nhận 40%, 10% hệ thống giữ

**Alternate — Hủy <6h (không hoàn):**
- Confirm dialog hiện: "Không hoàn tiền. Chủ sân nhận đền bù 90%."
- Kết quả: Player không nhận, Partner nhận 90%

**Alternate — Vượt 3 lượt/tháng:**
- Nút Hủy disabled + tooltip E-sport-matching-008 "Đã đạt giới hạn hủy tháng này"

**Alternate — Cooldown 15 phút:**
- Sau 2 lần hủy trong 1 giờ, System block tạo match mới, hiện E-sport-matching-009 với countdown

## e. Activity diagram

Không bắt buộc (3 alternate paths — đã đủ trong prose).

## f. Screens involved

- `match-confirmed` — nút Hủy trận + confirm dialog + trạng thái sau hủy

## g. FR map

| FR | Mô tả |
|----|-------|
| FR-sport-matching-018 | Hủy trận: ma trận hoàn tiền 3 bậc, max 3/tháng, cooldown 15p |

## h. Open Questions

Không có OQ mở.
