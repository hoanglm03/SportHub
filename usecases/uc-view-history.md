# UC: Xem lịch sử trận + thống kê

## a. Giới thiệu

Player xem danh sách các trận đấu đã chơi, bao gồm thông tin sân, giờ, đối thủ và kết quả. Player cũng xem thống kê tổng hợp win/loss per môn và rating nhận từ đối thủ để theo dõi tiến bộ.

## b. Actors

- **Primary:** Player

## c. Pre-conditions

- Player đã có ≥1 trận đấu hoàn thành.

## d. Expected Result

**Thành công:** Player thấy danh sách trận (mới nhất trước), mỗi trận hiện sân + giờ + đối thủ + kết quả. Thống kê tổng: tổng trận, win/loss per môn, rating trung bình nhận được. Filter theo môn thể thao.

**Nhánh phụ:**
- Chưa có trận nào → hiện empty state "Chưa có trận đấu nào. Hãy tìm đối thủ!"

## e. Activity Diagram

N/A — flow tuyến tính, xem Mục d.

## f. Screens Involved

| Screen | Vai trò trong UC |
|--------|-----------------|
| match-history | Danh sách trận + thống kê tổng + filter môn |

## g. FR Mapping

| FR | Vai trò |
|----|---------|
| FR-sport-matching-012 | Lịch sử trận + thống kê win/loss + rating |

## h. Open Questions

Không có OQ riêng cho UC này.
