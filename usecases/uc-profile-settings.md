# UC: Profile & Settings

## a. Giới thiệu

Player xem/sửa profile, đổi mật khẩu, cài đặt riêng tư (ẩn profile, ẩn GPS), cài đặt notification, xem ví/điểm thưởng, xóa tài khoản.

## b. Actors

- **Primary:** Player

## c. Pre-conditions

- Player đã đăng nhập.

## d. Expected Result

**Sửa profile:** Cập nhật tên/avatar/email thành công. Email mới cần verify OTP.

**Đổi mật khẩu:** Nhập mật khẩu cũ đúng + mới hợp lệ → cập nhật.

**Cài đặt riêng tư:** Toggle ẩn profile → không xuất hiện trên matching map.

**Xóa tài khoản:** Confirm 2 bước → grace period 30 ngày → xóa vĩnh viễn.

**Nhánh phụ:**
- Mật khẩu cũ sai → E-016.
- Mật khẩu mới yếu → E-017.
- Còn booking pending → E-018, yêu cầu hủy trước.

## e. Activity Diagram

N/A.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| settings | Tất cả cài đặt + profile |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-037 | Xem/sửa profile |
| FR-sport-matching-038 | Đổi mật khẩu |
| FR-sport-matching-039 | Cài đặt riêng tư |
| FR-sport-matching-040 | Xóa tài khoản |
| FR-sport-matching-036 | Cài đặt notification |
| FR-sport-matching-041 | Ví — điểm thưởng giảm giá |
| FR-sport-matching-035 | Notification Center (xem danh sách noti, đánh dấu đã đọc) |

## h. Open Questions

Không có OQ.
