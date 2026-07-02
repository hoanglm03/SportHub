# UC: Notification Center (uc-notification)

## a. Mục đích

Player xem toàn bộ thông báo hệ thống tập trung tại một nơi, đánh dấu đã đọc, và cài đặt bật/tắt từng loại noti theo nhu cầu. Deep link từ noti đưa Player đến đúng màn hình liên quan.

## b. Actors

- **Player** — người nhận và quản lý thông báo
- **System** — push notification qua FCM, lưu lịch sử noti, quản lý badge

## c. Pre-conditions

- Player đã đăng nhập
- Quyền push notification đã được cấp (hoặc chưa — app nhắc cấp lần đầu)
- CAP-23 (P1) đã active

## d. Expected result

**Luồng xem notification:**
1. Badge số đỏ hiện trên icon chuông header (số noti chưa đọc)
2. Player tap icon chuông → `notification-center`, danh sách noti mới nhất trước
3. Tap từng noti → đánh dấu đã đọc + deep link đến màn hình liên quan
4. Nút "Đọc tất cả" → đánh dấu toàn bộ đã đọc, badge về 0

**Luồng cài đặt noti:**
1. Player vào Settings → "Thông báo"
2. Toggle bật/tắt từng loại: booking, match invite, chat, đánh giá, khuyến mãi
3. Mặc định tất cả ON

**Alternate — Không có noti:**
- Màn `notification-center` hiện empty state: "Chưa có thông báo nào"

## e. Activity diagram

Không bắt buộc.

## f. Screens involved

- `notification-center` — danh sách noti + đánh dấu đọc
- `settings` — cài đặt bật/tắt từng loại noti

## g. FR map

| FR | Mô tả |
|----|-------|
| FR-sport-matching-035 | Notification Center: icon chuông, badge, danh sách, deep link |
| FR-sport-matching-036 | Cài đặt notification: bật/tắt từng loại |

## h. Open Questions

Không có OQ mở.
