# UC: Đánh giá sân

## a. Giới thiệu

Sau buổi chơi (booking completed), Player đánh giá sân 1-5 sao + review text. Nhận điểm thưởng nếu trong 7 ngày. Đánh giá cập nhật rating trung bình sân.

## b. Actors

- **Primary:** Player

## c. Pre-conditions

- Booking trạng thái completed.
- Player chưa đánh giá sân cho booking này.

## d. Expected Result

**Thành công:** Đánh giá lưu, rating trung bình sân cập nhật, Player nhận điểm thưởng. "Cảm ơn đánh giá! Bạn nhận được {X} điểm thưởng".

**Nhánh phụ:**
- Quá 7 ngày → vẫn đánh giá được, không nhận điểm thưởng.
- Đã đánh giá → hiện read-only.

## e. Activity Diagram

N/A — flow tuyến tính.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| venue-rate | Chấm sao + review + gửi |
| booking-detail | Entry point (nút Đánh giá khi completed) |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-029 | Đánh giá sân 5 sao + review + điểm thưởng |

## h. Open Questions

Không có OQ.
