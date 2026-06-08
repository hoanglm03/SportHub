# UC: Đăng ký + Setup Profile

## a. Giới thiệu

Player mới tạo tài khoản trên ứng dụng Sport Matching, xác thực email qua OTP, và thiết lập hồ sơ thể thao (chọn môn + trình độ) để sẵn sàng tìm đối thủ.

## b. Actors

- **Primary:** Player (người chơi mới, chưa có account)

## c. Pre-conditions

- Player đã cài app trên smartphone (Android/iOS).
- Player có email hợp lệ và truy cập được inbox.
- Internet khả dụng.

## d. Expected Result

**Thành công:** Account verified, profile thể thao hoàn tất (≥1 môn + trình độ), Player được chuyển tới màn hình chính (bản đồ).

**Nhánh phụ:**
- Email đã tồn tại → thông báo lỗi, gợi ý đăng nhập.
- OTP sai/hết hạn → cho phép gửi lại OTP.
- Player skip setup profile → account verified nhưng chưa thể matching (buộc quay lại setup).

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| register | Nhập email + mật khẩu + tên hiển thị |
| otp-verify | Nhập OTP 6 số xác thực email |
| profile-setup | Chọn môn thể thao + trình độ per môn |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-001 | Đăng ký tài khoản + OTP verify |
| FR-sport-matching-002 | Setup profile thể thao |

## h. Open Questions

Không có OQ riêng cho UC này.
