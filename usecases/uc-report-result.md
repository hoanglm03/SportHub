# UC: Report kết quả trận đấu

## a. Giới thiệu

Sau khi trận đấu hoàn thành, cả 2 Player tự report kết quả (Thắng/Thua/Hòa). Hệ thống so khớp kết quả: nếu 2 bên report giống nhau thì ghi nhận, nếu conflict (cả 2 claim thắng) thì flag cho Admin review. Kết quả dùng cho thống kê win/loss và auto-adjust trình độ.

## b. Actors

- **Primary:** Player (cả 2 bên report)
- **Secondary:** Admin (review conflict)

## c. Pre-conditions

- Trận đấu đã hoàn thành (Match status: Completed).
- Player chưa report kết quả cho trận này.

## d. Expected Result

**Thành công (report khớp):** Cả 2 Player report cùng kết quả (vd: Player A chọn Thắng, Player B chọn Thua) → hệ thống ghi nhận kết quả, cập nhật thống kê win/loss (FR-012).

**Nhánh phụ:**
- **Conflict:** Cả 2 Player claim thắng hoặc kết quả không khớp → hệ thống flag cho Admin review. Kết quả tạm ghi "Đang xác minh".
- **Chỉ 1 Player report:** Chờ Player còn lại trong 24h. Quá 24h, kết quả của Player đã report được ghi nhận mặc định.
- **Không ai report:** Trận ghi nhận "Hoàn thành, không có kết quả" — không ảnh hưởng thống kê win/loss.

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Component | Vai trò trong UC |
|--------|-----------|-----------------|
| rate-opponent | #report-result-section | Phần trên: chọn Thắng/Thua/Hòa trước khi đánh giá sao |
| rate-opponent | #rating-section (read-only context) | Sau report → hiện form đánh giá sao (thuộc uc-rate-opponent) |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-021 | Report kết quả trận (Thắng/Thua/Hòa, conflict → Admin) |
| FR-sport-matching-012 | Lịch sử trận + thống kê win/loss (nhận data từ report) |

## h. Open Questions

- [x] OQ-1: Thời hạn chờ Player còn lại report là bao lâu? → **24h. Quá 24h chỉ 1 bên report → ghi nhận kết quả đó mặc định.**
