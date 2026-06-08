---
type: screen-index
feature: sport-matching
status: draft
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-04
links:
  - docs/sport-matching/srs/spec.md
  - docs/sport-matching/usecases/_index.md
tags: [screens, sport-matching]
stale_reason: ""
changelog:
  - 2026-06-07 | /review | [invite-waiting] added screen post-review: countdown 5p + cancel + 3 states
  - 2026-06-04 | /srs | initial 12 screens scaffolded
---

# Sport Matching — Screens Index

## Screens

| Slug | Status | Used by UC | Figma | HTML prototype | Updated |
|------|--------|-----------|-------|----------------|---------|
| register | draft | uc-register | — | — | 2026-06-04 |
| otp-verify | draft | uc-register | — | — | 2026-06-04 |
| profile-setup | draft | uc-register | — | — | 2026-06-04 |
| map-search | draft | uc-find-opponent | — | — | 2026-06-04 |
| opponent-profile | draft | uc-find-opponent | — | — | 2026-06-04 |
| court-select | draft | uc-book-match | — | — | 2026-06-04 |
| invite-confirm | draft | uc-book-match | — | — | 2026-06-04 |
| invite-waiting | draft | uc-book-match | — | — | 2026-06-07 |
| invite-receive | draft | uc-book-match | — | — | 2026-06-04 |
| match-confirmed | draft | uc-book-match | — | — | 2026-06-04 |
| match-history | draft | uc-view-history | — | — | 2026-06-04 |
| rate-opponent | draft | uc-rate-opponent | — | — | 2026-06-04 |
| player-profile | draft | cross-UC | — | — | 2026-06-04 |

## Descriptions

### register
Màn hình đăng ký tài khoản mới. Player nhập email, mật khẩu, tên hiển thị và nhấn Đăng ký để nhận OTP.

### otp-verify
Màn hình xác thực OTP 6 số gửi qua email. Có countdown thời gian hết hạn và option gửi lại OTP.

### profile-setup
Màn hình thiết lập hồ sơ thể thao sau đăng ký. Player chọn môn yêu thích và tự đánh giá trình độ per môn.

### map-search
Màn hình chính của app. Bản đồ GPS hiện vị trí Player + đối thủ gần + sân. Filter bar lọc theo môn/trình độ/bán kính. Overlay danh sách đối thủ phù hợp.

### opponent-profile
Xem chi tiết profile đối thủ trước khi mời đấu. Hiện avatar, tên, môn, trình độ, rating, thống kê win/loss, nút Mời đấu.

### court-select
Browse sân gần theo vị trí + môn hỗ trợ. Hiện danh sách sân kèm khoảng cách, grid slot giờ trống với giá, nút Chọn.

### invite-confirm
Xác nhận trước khi gửi invite. Tóm tắt thông tin: đối thủ + sân + giờ + giá. Nút Gửi lời mời.

### invite-waiting
Chờ đối thủ phản hồi sau khi gửi invite. Countdown 5 phút, hiện thông tin trận, nút Hủy lời mời. 3 states: accept (→ match-confirmed), reject (E-003), timeout (E-002).

### invite-receive
Đối thủ nhận invite ghép đôi. Hiện thông tin người mời + sân + giờ, countdown 5 phút, nút Accept + Reject.

### match-confirmed
Trận đấu đã xác nhận thành công. Hiện thông tin đầy đủ: đối thủ + sân + giờ + vị trí bản đồ mini.

### match-history
Danh sách trận đã chơi (mới nhất trước). Mỗi trận hiện sân/giờ/đối thủ/kết quả. Thống kê tổng win/loss per môn. Filter theo môn.

### rate-opponent
Đánh giá đối thủ sau trận. Chấm sao 1-5, nhận xét text optional, nút Gửi đánh giá.

### player-profile
Xem và sửa hồ sơ cá nhân. Hiện tên, avatar, danh sách môn + trình độ per môn, rating tổng, nút Sửa.
