# UC: Admin Dashboard & Quản lý

## a. Giới thiệu

Admin quản lý toàn hệ thống: user, sân, booking, doanh thu, moderate đánh giá, xử lý tranh chấp.

## b. Actors

- **Primary:** Admin

## c. Pre-conditions

- Admin đã đăng nhập với role admin.

## d. Expected Result

**Quản lý user:** Xem/khóa/mở user. Tìm kiếm, filter.
**Quản lý sân:** Duyệt/từ chối sân pending. Khóa/mở sân.
**Quản lý booking:** Xem chi tiết, xử lý dispute.
**Doanh thu:** Dashboard KPI, revenue chart, export.
**Moderate:** Ẩn/xóa đánh giá vi phạm. Cảnh báo user.

## e. Activity Diagram

N/A.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| admin-dashboard | Dashboard tổng quan + menu quản lý |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-042 | Quản lý user |
| FR-sport-matching-043 | Quản lý sân |
| FR-sport-matching-044 | Quản lý booking |
| FR-sport-matching-045 | Dashboard doanh thu |
| FR-sport-matching-046 | Moderate đánh giá |
| FR-sport-matching-021 | Xử lý conflict kết quả trận (flag từ uc-report-result → Admin review + quyết định) |

## h. Open Questions

Không có OQ.
