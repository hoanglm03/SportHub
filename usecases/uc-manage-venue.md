# UC: Đăng & Quản lý sân (Chủ sân)

## a. Giới thiệu

Chủ sân (Partner) đăng sân mới lên hệ thống, quản lý thông tin, block khung giờ, duyệt booking. Admin duyệt sân trước khi hiển thị cho Player.

## b. Actors

- **Primary:** Partner (Chủ sân)
- **Secondary:** Admin (duyệt sân mới), Staff (hỗ trợ quản lý)

## c. Pre-conditions

- Partner đã đăng nhập với role chủ sân.

## d. Expected Result

**Đăng sân thành công:** Sân pending_review → Admin duyệt → active, hiển thị cho Player.

**Quản lý thành công:** Block/unblock giờ, sửa thông tin, xem đánh giá.

**Nhánh phụ:**
- Admin từ chối → gửi lý do, Partner chỉnh sửa + submit lại.
- Thiếu ảnh (< 3 tấm) → validate error, yêu cầu upload thêm.
- Không duyệt booking 3 lần → cảnh báo.
- Không duyệt 5 lần → tạm khóa sân (suspended).

## e. Activity Diagram

N/A — flow tuyến tính.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| venue-manage | Danh sách sân + booking chờ duyệt + nút Đăng mới |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-030 | Đăng sân mới (thông tin + ảnh + sân con) |
| FR-sport-matching-031 | Block khung giờ |
| FR-sport-matching-032 | Cảnh báo/khóa chủ sân không duyệt |
| FR-sport-matching-026 | Duyệt/từ chối booking |

## h. Open Questions

Không có OQ.
