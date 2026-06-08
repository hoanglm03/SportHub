# UC: Đặt sân + Ghép đôi trận đấu

## a. Giới thiệu

Player đã chọn đối thủ, tiến hành chọn sân + slot giờ, hệ thống giữ chỗ tạm (Pessimistic Locking 5 phút), gửi invite cho đối thủ. Đối thủ nhận thông báo, xem thông tin trận, accept hoặc reject. Accept dẫn tới match confirmed — cả 2 nhận thông tin đầy đủ.

## b. Actors

- **Primary:** Player (người tạo trận)
- **Secondary:** Opponent (đối thủ được mời)

## c. Pre-conditions

- Player đã chọn đối thủ từ uc-find-opponent.
- Player không có match pending (BR-sport-matching-005).
- Player chưa vượt limit 10 invite/ngày/môn (BR-sport-matching-004).
- GPS ON, Internet khả dụng.

## d. Expected Result

**Thành công:** Match confirmed, cả 2 Player nhận notification với thông tin đối thủ + sân + giờ + vị trí bản đồ. Nhắc nhở trước trận 1 giờ.

**Nhánh phụ:**
- Slot đã bị lock bởi người khác → E-sport-matching-007, gợi ý slot/sân khác.
- Player đã có match pending → E-sport-matching-004, yêu cầu hủy cái cũ.
- Vượt limit invite → E-sport-matching-005, gợi ý Premium.
- Đối thủ reject → E-sport-matching-003, release slot, Player chọn đối thủ khác.
- Timeout 5 phút → E-sport-matching-002, auto hủy invite + release slot + tìm đối thủ tiếp theo Matching Score.
- 2 Player gửi invite cùng 1 đối thủ → First-come-first-served (BR-sport-matching-006).

## e. Activity Diagram

N/A — xem sequence diagram chi tiết tại [[docs/sport-matching/srs/flows.md|Flow: Matching + Booking + Invite]].

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| court-select | Browse sân gần + chọn slot giờ |
| invite-confirm | Xác nhận gửi invite (tóm tắt đối thủ + sân + giờ) |
| invite-waiting | Chờ đối thủ phản hồi (countdown 5p, cancel option, 3 states: accept/reject/timeout) |
| invite-receive | Đối thủ nhận invite, xem thông tin, Accept/Reject |
| match-confirmed | Trận xác nhận, hiện thông tin đầy đủ |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-006 | Chọn sân + slot giờ |
| FR-sport-matching-007 | Giữ chỗ tạm (Slot Lock 5 phút) |
| FR-sport-matching-008 | Gửi invite ghép đôi |
| FR-sport-matching-009 | Phản hồi invite (Accept/Reject/Timeout) |
| FR-sport-matching-010 | Xác nhận trận đấu + notification |

## h. Open Questions

Không có OQ riêng cho UC này.
