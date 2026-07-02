# UC: Social Feed

## a. Giới thiệu

Player đăng bài tự do (text + ảnh + video), like/comment bài người khác, follow player. Feed timeline theo following. Chia sẻ kết quả trận. Admin moderate nội dung.

## b. Actors

- **Primary:** Player
- **Secondary:** Admin (moderate)

## c. Pre-conditions

- Player đã đăng nhập.

## d. Expected Result

**Đăng bài:** Bài hiện trên timeline followers.

**Like/Comment:** Cập nhật real-time. Notification cho author.

**Follow:** Feed cập nhật với bài từ người mới follow.

**Nhánh phụ:**
- Bài bị report → Admin review → E-028 nếu vi phạm.
- Video > 30s → validate error.
- Ảnh > 5 tấm → validate error.

## e. Activity Diagram

N/A.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| social-feed | Feed timeline + đăng bài + like/comment |
| opponent-profile | Follow/unfollow từ profile |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-053 | Đăng bài Social Feed |
| FR-sport-matching-054 | Like + Comment |
| FR-sport-matching-055 | Follow Player |
| FR-sport-matching-056 | Moderate Social Feed |

## h. Open Questions

- [ ] OQ-1: Video upload limit (file size)? Nén server-side hay client-side?
