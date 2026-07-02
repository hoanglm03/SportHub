# UC: Ghép đội (Team Matching)

## a. Giới thiệu

Captain tạo đội, mời thành viên. System ghép random 2 đội theo Team Matching Score. Flow slot lock + invite tương tự 1v1 nhưng Captain đại diện confirm.

## b. Actors

- **Primary:** Player (Captain)
- **Secondary:** Player (thành viên đội), Opponent team Captain

## c. Pre-conditions

- Captain đã tạo đội với ≥2 thành viên.
- Đội chưa có match pending.
- Môn của đội hỗ trợ ≥2 người/đội.

## d. Expected Result

**Thành công:** 2 đội ghép thành công, match confirmed. Tất cả thành viên cả 2 đội nhận noti.

**Nhánh phụ:**
- Đội < 2 người → E-026.
- Không tìm thấy đội phù hợp → gợi ý mở rộng bán kính/trình độ.
- Đội đối thủ từ chối → release slot, tìm đội khác.

## e. Activity Diagram

N/A — tương tự flow 1v1, Captain thay Player.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| team-manage | Tạo/quản lý đội + tìm trận |
| court-select | Chọn sân (Captain) |
| match-confirmed | Kết quả ghép đội |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-048 | Tạo đội |
| FR-sport-matching-049 | Ghép đội vs đội |

## h. Open Questions

- [ ] OQ-1: Team Matching Score tính trung bình hay weighted (Captain weight cao hơn)?
