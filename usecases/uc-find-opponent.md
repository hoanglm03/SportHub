# UC: Tìm đối thủ trên bản đồ

## a. Giới thiệu

Player mở app, hệ thống xác định vị trí GPS, hiện bản đồ khu vực gần với danh sách đối thủ phù hợp theo Matching Score (môn + trình độ + vị trí + rating). Player lọc và chọn đối thủ muốn mời đấu.

## b. Actors

- **Primary:** Player (đã có account + profile thể thao)

## c. Pre-conditions

- Player đã đăng ký + setup profile (≥1 môn + trình độ).
- GPS bật và quyền truy cập vị trí đã cấp.
- Internet khả dụng.

## d. Expected Result

**Thành công:** Player thấy danh sách đối thủ phù hợp trên bản đồ, xem được profile (trình độ, rating, win/loss) của từng đối thủ, sẵn sàng chọn để mời đấu.

**Nhánh phụ:**
- GPS tắt → E-sport-matching-001, dừng matching, yêu cầu bật GPS.
- Không tìm thấy đối thủ → E-sport-matching-006, gợi ý mở rộng bán kính/điều chỉnh trình độ.
- Player đang có match pending → E-sport-matching-004, chặn tạo match mới.

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| map-search | Bản đồ chính, filter bar, danh sách đối thủ overlay |
| opponent-profile | Xem chi tiết profile đối thủ (rating, trình độ, lịch sử) |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-003 | Xác định vị trí GPS |
| FR-sport-matching-004 | Tìm đối thủ theo Matching Score |
| FR-sport-matching-005 | Hiển thị bản đồ + filter |

## h. Open Questions

Không có OQ riêng cho UC này.
