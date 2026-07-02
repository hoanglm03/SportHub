# UC: Quản lý sân (Partner)

## a. Giới thiệu

Partner (chủ sân) đăng ký thông tin sân thể thao lên hệ thống. Bao gồm thông tin cơ bản (tên, địa chỉ, tọa độ), môn hỗ trợ, slot giờ khả dụng và giá. Xác thực đối tác qua Manual KYC (Zalo). Staff hỗ trợ quá trình onboard.

## b. Actors

- **Primary:** Partner (chủ sân)
- **Secondary:** Staff (nhân viên đối tác hỗ trợ), Admin (phê duyệt KYC)

## c. Pre-conditions

- Partner đã có account trên app (role: Partner).
- Internet khả dụng.

## d. Expected Result

**Thành công:** Sân đăng ký thành công, KYC verified, slot giờ hiển thị cho Player tìm kiếm và đặt chỗ. Partner có thể quản lý slot (thêm/sửa/xóa).

**Nhánh phụ:**
- KYC chưa duyệt → sân ở trạng thái pending, chưa hiển thị cho Player.
- Thông tin sân không hợp lệ (thiếu địa chỉ, tọa độ) → yêu cầu bổ sung.
- Partner cập nhật slot giờ/giá → cập nhật realtime cho Player đang browse.

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

Screens cho Partner flow là P1, chưa thiết kế trong v1.0.

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-015 | Partner đăng ký sân + Manual KYC |

## h. Open Questions

- [ ] OQ-1: Screens cụ thể cho Partner management flow (P1) — cần thiết kế khi dev v1.1.
- [ ] OQ-2: FR-015 (Manual KYC qua Zalo) và FR-047 (Auto KYC trên app, uc-partner-onboard) — concurrent paths hay migration? FR-047 thay thế FR-015 khi P1 ready? Resolve trước khi implement.
