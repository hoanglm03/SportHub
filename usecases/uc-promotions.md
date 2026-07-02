# UC: Hệ thống khuyến mãi

## a. Giới thiệu

Player nhận/dùng voucher giảm giá khi đặt sân. Mã referral mời bạn — cả 2 nhận thưởng. Admin tạo chiến dịch hoặc system tự động trigger voucher theo rules.

## b. Actors

- **Primary:** Player (nhận + dùng voucher, share referral)
- **Secondary:** Admin (tạo + quản lý chiến dịch)

## c. Pre-conditions

- Player đã đăng nhập.
- Voucher còn hạn + còn lượt + đủ điều kiện.

## d. Expected Result

**Dùng voucher:** Giá booking giảm theo voucher. Voucher trừ 1 lượt.

**Referral:** Bạn đăng ký qua mã → người mời + người được mời nhận thưởng.

**Auto trigger:** System tự gửi voucher khi user đạt điều kiện (first booking, birthday, inactive...).

**Nhánh phụ:**
- Voucher không hợp lệ → E-029.
- Referral gian lận (cùng device) → E-030.
- Voucher hết lượt/hết hạn → E-029.

## e. Activity Diagram

N/A.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| voucher-list | Xem voucher + referral + nhập code |
| booking-confirm | Áp dụng voucher khi đặt sân |
| register | Nhập mã referral khi đăng ký |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-057 | Voucher giảm giá |
| FR-sport-matching-058 | Mã referral |
| FR-sport-matching-059 | Chiến dịch khuyến mãi tự động |

## h. Open Questions

- [ ] OQ-1: Voucher có stack được không (dùng 2 voucher + điểm thưởng cùng lúc)?
