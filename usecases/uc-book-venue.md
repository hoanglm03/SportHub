# UC: Đặt sân thể thao

## a. Giới thiệu

Player đã chọn sân con + khung giờ từ uc-search-venue. Tiến hành đặt sân: thanh toán ngay hoặc giữ chỗ 30 phút. System tạm giữ slot 10 phút tránh concurrent. Sau thanh toán, chủ sân có 30 phút duyệt. Duyệt → confirmed. Từ chối/hết giờ → hoàn tiền auto.

## b. Actors

- **Primary:** Player
- **Secondary:** Partner (chủ sân duyệt)

## c. Pre-conditions

- Player đã đăng nhập.
- Player đã chọn sân con + khung giờ trống.
- Player chưa có 3 booking đồng thời (BR-019).
- Khung giờ >= 2h trước giờ chơi (BR-020).
- Ngày đặt <= 14 ngày tới (BR-020).

## d. Expected Result

**Thành công:** Booking confirmed. Player nhận noti: "Chủ sân đã xác nhận! Hẹn gặp bạn tại {tên sân} lúc {giờ}, {ngày}".

**Nhánh phụ:**
- Slot bị lock bởi người khác → E-010, chọn giờ khác.
- Player có 3 booking → E-013, quản lý booking hiện có.
- Đặt sát giờ (< 2h) → E-014.
- Giữ chỗ hết 30 phút chưa thanh toán → E-011, expired.
- Chủ sân từ chối → E-012, hoàn tiền auto.
- Chủ sân hết 30 phút không duyệt → auto hủy + hoàn tiền.
- Mất mạng giữa thanh toán → check lại trạng thái payment, nếu đã trừ tiền → paid.

## e. Activity Diagram

N/A — xem sequence diagram tại flows.md (sẽ bổ sung).

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| venue-detail | Chọn slot giờ |
| booking-confirm | Xác nhận + chọn thanh toán/giữ chỗ |
| booking-detail | Theo dõi trạng thái booking (pending/paid/confirmed) |
| venue-manage | Chủ sân duyệt/từ chối booking |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-024 | Đặt sân — thanh toán ngay |
| FR-sport-matching-025 | Đặt sân — giữ chỗ 30p |
| FR-sport-matching-026 | Chủ sân duyệt booking |

## h. Open Questions

Không có OQ.
