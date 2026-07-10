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
  - '2026-06-26 | /gap | added 3 P1 screens: payment-checkout, wallet, premium-upgrade (gap fix)'
  - '2026-06-25 | /srs | added 5 P2 screens: team-manage, tournament-list, tournament-detail, social-feed, voucher-list'
  - '2026-06-23 | /review | fix uxui findings: login.md + venue-register.md created, booking-confirm countdown fixed, match-confirmed cancel+E008/E009, loading states register/otp/profile, invite-receive exit path, otp-verify context variant, admin loading'
  - '2026-06-23 | /srs | added 6 P1 screens: chat-list, chat-detail, notification-center, settings, admin-dashboard, partner-onboard'
  - '2026-06-23 | /srs | added 6 venue-booking screens: venue-search, venue-detail, booking-confirm, booking-detail, venue-rate, venue-manage'
  - '2026-06-07 | /review | [invite-waiting] added screen post-review: countdown 5p + cancel + 3 states'
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
| venue-search | draft | uc-search-venue | — | — | 2026-06-23 |
| venue-detail | draft | uc-search-venue, uc-book-venue | — | — | 2026-06-23 |
| booking-confirm | draft | uc-book-venue | — | — | 2026-06-23 |
| booking-detail | draft | uc-book-venue, uc-cancel-venue-booking | — | — | 2026-06-23 |
| venue-rate | draft | uc-rate-venue | — | — | 2026-06-23 |
| venue-manage | draft | uc-manage-venue | — | — | 2026-06-23 |
| chat-list | draft | uc-chat | — | — | 2026-06-23 |
| chat-detail | draft | uc-chat | — | — | 2026-06-23 |
| notification-center | draft | cross-UC | — | — | 2026-06-23 |
| settings | draft | uc-profile-settings | — | — | 2026-06-23 |
| admin-dashboard | draft | uc-admin | — | — | 2026-06-23 |
| partner-onboard | draft | uc-partner-onboard | — | — | 2026-06-23 |
| login | draft | uc-register (auth) | — | — | 2026-06-23 |
| venue-register | draft | uc-manage-venue | — | — | 2026-06-23 |
| payment-checkout | draft | uc-payment | — | — | 2026-06-26 |
| wallet | draft | uc-wallet | — | — | 2026-06-26 |
| premium-upgrade | draft | uc-premium | — | — | 2026-06-26 |
| team-manage | draft | uc-team-matching | — | — | 2026-06-25 |
| tournament-list | draft | uc-tournament | — | — | 2026-06-25 |
| tournament-detail | draft | uc-tournament | — | — | 2026-06-25 |
| social-feed | draft | uc-social-feed | — | — | 2026-06-25 |
| voucher-list | draft | uc-promotions | — | — | 2026-06-25 |

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

### venue-search
Tìm sân thể thao. Filter theo môn, khu vực, ngày, giá. Danh sách sân card (ảnh, rating, giá, slot trống).

### venue-detail
Chi tiết sân: ảnh carousel, rating, địa chỉ, tiện ích, chọn sân con, grid slot giờ real-time, đánh giá.

### booking-confirm
Xác nhận đặt sân. Tóm tắt sân + giờ + giá, chính sách hủy, 2 nút: Thanh toán ngay / Giữ chỗ 30p.

### booking-detail
Chi tiết booking. Status badge, thông tin sân/giờ/giá, chính sách hoàn tiền realtime, nút Đổi/Hủy/Chỉ đường.

### venue-rate
Đánh giá sân sau buổi chơi. Rating 1-5 sao + review text + thông báo điểm thưởng.

### venue-manage
Quản lý sân cho chủ sân. Danh sách sân + status, booking chờ duyệt với countdown, nút Đăng sân mới.

### chat-list
Danh sách hội thoại. Sắp theo tin mới nhất. Badge unread. Online/offline status.

### chat-detail
Chat 1-1. Bubble text + ảnh. Input bar. Real-time. Typing indicator.

### notification-center
Trung tâm thông báo. List noti mới nhất, đánh dấu đã đọc, deep link.

### settings
Cài đặt & Profile. Sửa profile, đổi mật khẩu, riêng tư, noti settings, ví/điểm, xóa tài khoản.

### admin-dashboard
Dashboard quản trị. KPI cards, action queue, menu quản lý user/sân/booking/doanh thu/moderate.

### partner-onboard
Đăng ký chủ sân. 3 bước: thông tin → giấy tờ → điều khoản. Status tracking.

### login
Đăng nhập cho user đã có tài khoản. Email + mật khẩu + Google OAuth. Link Quên mật khẩu + Đăng ký.

### venue-register
Form đăng sân mới cho chủ sân. Nhập thông tin + ảnh + sân con + submit → admin duyệt.

### payment-checkout
Màn hình thanh toán online. Player chọn cổng MoMo hoặc VNPay, xem tóm tắt booking + commission, nhấn thanh toán để redirect sang cổng.

### wallet
Màn hình Ví nội bộ. Hiện số dư tiền + điểm thưởng, lịch sử giao dịch (nạp/rút/hoàn tiền/điểm), nút Nạp và Rút.

### premium-upgrade
Màn hình mua gói Premium 49.000đ/tháng. Hiện quyền lợi, giá, chọn cổng thanh toán, trạng thái đã Premium nếu đang active.

### team-manage
Quản lý đội. Tạo đội, mời thành viên, Captain quản lý, tìm trận đội vs đội.

### tournament-list
Danh sách giải đấu. Filter tabs, card giải (môn/format/ngày/slot/phí), tạo giải mới.

### tournament-detail
Chi tiết giải: thông tin, bảng đấu bracket/round-robin, đăng ký, BXH, quản lý (người tạo).

### social-feed
Cộng đồng. Feed bài viết (text + ảnh + video), like/comment, follow, match result cards.

### voucher-list
Ưu đãi. Mã referral cá nhân, voucher khả dụng, nhập code thủ công, lịch sử.
