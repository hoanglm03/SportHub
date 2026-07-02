# UC: Đánh giá đối thủ sau trận

## a. Giới thiệu

Sau khi trận đấu hoàn thành, hệ thống gửi nhắc nhở đánh giá. Player chấm rating (1-5 sao) và nhận xét (optional) cho đối thủ. Hệ thống cập nhật rating trung bình và kiểm tra auto-adjust trình độ qua ELO.

## b. Actors

- **Primary:** Player (người đánh giá)

## c. Pre-conditions

- Trận đấu đã hoàn thành (Match status: Completed).
- Player chưa đánh giá đối thủ cho trận này.

## d. Expected Result

**Thành công:** Rating gửi thành công, rating trung bình đối thủ được cập nhật. Nếu rating pattern cho thấy trình độ thực tế khác khai báo, hệ thống auto-adjust Matching Score (P1 — ELO-based).

**Nhánh phụ:**
- Player bỏ qua đánh giá → hệ thống nhắc lại sau, không ép buộc.
- Đánh giá bị nghi ngờ ác ý (P2) → thuật toán flag, Admin review.

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Component | Vai trò trong UC |
|--------|-----------|-----------------|
| rate-opponent | #rating-section | Chấm sao (1-5) + nhận xét text + nút Gửi (hiện sau report kết quả) |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-011 | Đánh giá đối thủ (rating + comment) |
| FR-sport-matching-014 | Auto-adjust trình độ ELO (P1) |

## h. Open Questions

Không có OQ riêng cho UC này.
