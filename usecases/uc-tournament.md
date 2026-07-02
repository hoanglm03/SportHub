# UC: Giải đấu (Tournament)

## a. Giới thiệu

Player/Admin/Partner tạo giải đấu. Format bracket hoặc round-robin. Giải tự phát miễn phí, giải cộng đồng có phí đặt cọc. Quản lý đăng ký, bảng đấu, kết quả, BXH.

## b. Actors

- **Primary:** Player (tạo giải tự phát + tham gia), Admin/Partner (tạo giải chính thức)
- **Secondary:** Player (người tham gia)

## c. Pre-conditions

- Người tạo đã đăng nhập.
- Giải cần ≥4 đội/người đăng ký để bắt đầu.

## d. Expected Result

**Tạo giải thành công:** Giải hiển thị trong danh sách, mở đăng ký.

**Đăng ký thành công:** Người tham gia confirmed (+ đặt cọc nếu có phí).

**Diễn ra:** Bảng đấu tự động, kết quả cập nhật, BXH real-time.

**Nhánh phụ:**
- Giải đầy slot → E-027.
- Bỏ giải → mất cọc (nếu có phí).
- Không đủ đăng ký → người tạo quyết định hủy hoặc gia hạn.

## e. Activity Diagram

N/A.

## f. Screens Involved

| Screen | Vai trò |
|--------|---------|
| tournament-list | Browse + tạo giải |
| tournament-detail | Chi tiết + đăng ký + bảng đấu + BXH |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-050 | Tạo giải đấu |
| FR-sport-matching-051 | Quản lý giải đấu |
| FR-sport-matching-052 | Phí đặt cọc giải |

## h. Open Questions

- [ ] OQ-1: Giải tự phát Player tạo — có cần Admin duyệt trước không hay publish trực tiếp?
- [ ] OQ-2: Giải thưởng (nếu có) xử lý qua Wallet hay ngoài hệ thống?
