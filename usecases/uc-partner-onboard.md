# UC: Onboarding chủ sân tự động

## a. Giới thiệu

Partner đăng ký trên app (thay vì KYC qua Zalo). 3 bước: thông tin cá nhân/DN → upload giấy tờ (CMND + giấy phép KD) → xác nhận điều khoản. Auto/manual verify. Approved → Partner role activated → có thể đăng sân.

## b. Actors

- **Primary:** Partner (người đăng ký)
- **Secondary:** Admin (review nếu auto verify fail)

## c. Pre-conditions

- User đã có tài khoản Player (đăng ký qua authentication).

## d. Expected Result

**Thành công:** Partner submit → pending → Admin/auto approve → Partner role activated → redirect venue-manage để đăng sân đầu tiên.

**Nhánh phụ:**
- Thiếu giấy tờ → E-019.
- Admin từ chối → gửi lý do, Partner sửa + submit lại.
- Chưa tick điều khoản → validate error.

## e. Activity Diagram

N/A.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| partner-onboard | Form 3 bước + status tracking |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-047 | Onboarding chủ sân tự động |

## h. Open Questions

Không có OQ.
