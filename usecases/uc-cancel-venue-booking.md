# UC: Hủy / Đổi booking sân

## a. Giới thiệu

Player hủy booking đã confirmed hoặc đổi giờ/sân. Hủy theo chính sách hoàn tiền 3 mức. Đổi giờ/sân tối đa 1 lần nếu trước 24h.

## b. Actors

- **Primary:** Player

## c. Pre-conditions

- Booking trạng thái confirmed (hoặc paid chờ duyệt).
- Player là người tạo booking.

## d. Expected Result

**Hủy thành công:** Booking cancelled, hoàn tiền theo chính sách (>24h: 100%, 12-24h: 75%, 2-12h: 50%, <2h: 0%). Gửi noti chủ sân.

**Đổi thành công:** Booking cập nhật giờ/sân mới, gửi noti chủ sân.

**Nhánh phụ:**
- Đổi trong 24h hoặc đã đổi 1 lần → từ chối, hướng dẫn hủy + đặt mới.
- Giờ mới không còn trống → E-010.

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| booking-detail | Xem chi tiết + nút Hủy / Đổi giờ |
| venue-detail | Chọn giờ/sân mới khi đổi |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-027 | Hủy booking sân + hoàn tiền |
| FR-sport-matching-028 | Đổi giờ/sân 1 lần trước 24h |

## h. Open Questions

Không có OQ.
