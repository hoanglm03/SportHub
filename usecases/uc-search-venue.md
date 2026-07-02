# UC: Tìm sân thể thao

## a. Giới thiệu

Player tìm sân thể thao độc lập (không cần ghép đối thủ). Tìm theo môn, khu vực, ngày, giá. Xem chi tiết sân: hình ảnh, giá, lịch trống real-time, đánh giá, tiện ích, vị trí bản đồ. Chọn sân con + khung giờ để đặt.

## b. Actors

- **Primary:** Player

## c. Pre-conditions

- Player đã đăng nhập (guest xem được danh sách sân, nhưng chọn slot phải đăng nhập).
- GPS ON hoặc Player chọn khu vực thủ công.

## d. Expected Result

**Thành công:** Player tìm được sân phù hợp, xem chi tiết, chọn sân con + khung giờ trống → chuyển sang uc-book-venue.

**Nhánh phụ:**
- Không có sân phù hợp → hiện gợi ý mở rộng bộ lọc hoặc chọn ngày khác.
- Sân hết slot hôm nay → hiện 🔴, vẫn xem chi tiết + chọn ngày khác.
- Guest chọn slot → redirect đăng nhập → quay lại flow.

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| venue-search | Bộ lọc + danh sách kết quả sân |
| venue-detail | Chi tiết sân + chọn sân con + slot giờ |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-022 | Tìm sân theo bộ lọc, real-time |
| FR-sport-matching-023 | Xem chi tiết sân, chọn sân con |

## h. Open Questions

Không có OQ.
