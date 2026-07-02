# UC: Chat real-time

## a. Giới thiệu

Player chat 1-1 real-time với Player khác (sau match hoặc từ profile) và với chủ sân (từ venue-detail). Gửi text + ảnh. Lưu lịch sử.

## b. Actors

- **Primary:** Player
- **Secondary:** Partner (chủ sân nhận chat)

## c. Pre-conditions

- Player đã đăng nhập.
- Chat với Player: đã có match chung hoặc xem profile.
- Chat với chủ sân: từ venue-detail.

## d. Expected Result

**Thành công:** Tin nhắn gửi real-time, đối phương nhận ngay + push noti nếu offline. Ảnh hiển thị inline.

**Nhánh phụ:**
- Ảnh > 10MB → E-015.
- Đối phương offline → tin nhắn lưu, push noti, hiện khi online.

## e. Activity Diagram

N/A — flow tuyến tính.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| chat-list | Danh sách hội thoại |
| chat-detail | Chat 1-1 text + ảnh |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-033 | Chat 1-1 real-time |
| FR-sport-matching-034 | Danh sách hội thoại |

## h. Open Questions

Không có OQ.
