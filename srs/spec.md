---
type: srs
feature: sport-matching
status: in-review
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-07
links:
  - docs/sport-matching/prd.md
  - docs/sport-matching/urd.md
  - docs/sport-matching/brd.md
  - docs/sport-matching/brainstorms/geo-skill-matching.md
tags: [srs, sport-matching]
stale_reason: ""
changelog:
  - '2026-06-26 | /gap | fix G4: thêm E-031 "Đội đối phương không phản hồi" vào Error Matrix (FR-049 error path)'
  - '2026-06-25 | /review | fix BLOCKING: Mục 1 Boundary align P2 scope; fix W5: FR-050 ambiguous; fix W6: FR-052 edge case hủy giải; fix S3: FR-055 note algorithm TBD'
  - '2026-06-25 | /srs | thêm FR-048→059 P2 (ghép đội, giải đấu, social feed, khuyến mãi), E-026→030'
  - '2026-06-23 | /review | fix 5 BLOCKING + 6 WARNING: gap hoàn tiền 12-24h, NFR payment/chat/GPS/auth, OQ-1+OQ-2 resolved, FR-024 align BR-011, FR-040 edge cases, FR-033 moderation, sync sections 6/7/8, auth matrix BR-025/026, errors E-020→023'
  - '2026-06-23 | /srs | thêm FR-033→047 (chat, noti, profile, wallet, admin, onboarding), E-015→019'
  - '2026-06-23 | /srs | thêm FR-022→032 (tìm đặt sân), E-010→014, BR-014→024 từ brainstorm venue-search-booking'
  - '2026-06-07 | /review | round 2 by @senior-ba: approve, 2 warnings applied (FR-021 source→CAP-16, Match entity +result fields). Status revisions→in-review'
  - '2026-06-07 | /review | round 1 by 6 agents: 1 blocking applied (FR-021), 7 warnings applied. Status draft→revisions'
  - '2026-06-04 | /srs | [states] initial 3 entity state machines: Match, Slot, Invite'
  - '2026-06-04 | /srs | [flows] initial 3 sequence flows: Registration, Matching+Booking, Rating'
  - '2026-06-04 | /srs | [erd] initial 12 entities, 14 relationships'
  - '2026-06-04 | /srs | initial spec: 20 FR, 7 NFR, 12 BR, 9 errors, 6 UCs, 12 screens'
---

# Sport Matching — Software Requirements Specification

> Kỹ thuật hoá scope đã chốt trong PRD. FR/NFR/business rules/error cụ thể.

## 1. Scope

SRS này cover toàn bộ tính năng Sport Matching: hệ thống matching thể thao 1v1 theo GPS + trình độ, tích hợp đặt sân, mô hình freemium, mobile-only cho thị trường Việt Nam.

Bao gồm: đăng ký/profile, matching algorithm (Matching Score), bản đồ trực quan, đặt sân (Pessimistic Slot Locking), invite ghép đôi, đánh giá đối thủ, lịch sử trận, thanh toán (P1), ví nội bộ (P1), premium subscription (P1), hủy trận + hoàn tiền (P2), phát hiện gian lận (P2), báo cáo quản trị (P2).

Boundary v1.0: không cover mạng xã hội, giải đấu, marketplace dụng cụ, web version, offline mode. P2 roadmap bao gồm ghép đội (CAP-27), giải đấu (CAP-28), social feed (CAP-29), khuyến mãi (CAP-30) — được spec trong FR-048→059 nhưng nằm ngoài phạm vi v1.0 launch.

## 2. Functional Requirements (FR)

| ID | Title | Description | Priority | Source |
|----|-------|-------------|----------|--------|
| FR-sport-matching-001 | Đăng ký tài khoản | Player nhập email + mật khẩu (min 8 ký tự, ≥1 chữ hoa + ≥1 số) + tên hiển thị. System gửi OTP qua email. Player nhập OTP để verify. Account tạo thành công. | P0 | CAP-01 |
| FR-sport-matching-002 | Setup profile thể thao | Player chọn ≥1 môn thể thao (tối đa 5 ưu tiên hiển thị), tự đánh giá trình độ 3 bậc (Mới chơi / Trung bình / Nâng cao) cho từng môn. Profile sẵn sàng sau setup. | P0 | CAP-01 |
| FR-sport-matching-003 | Xác định vị trí GPS | System tự động detect vị trí Player qua GPS khi mở app. Dùng vị trí làm tâm điểm quét đối thủ/sân. Nếu GPS tắt, hiện thông báo E-sport-matching-001. | P0 | CAP-02 |
| FR-sport-matching-004 | Tìm đối thủ (Matching) | System quét đối thủ theo Matching Score: môn thể thao (100% hard filter, phải khớp) + vị trí (40%) + trình độ (40%) + rating (20%). Bán kính mặc định 3km, tối đa 50km. Kết quả sắp xếp theo Score giảm dần. | P0 | CAP-02 |
| FR-sport-matching-005 | Hiển thị bản đồ | Bản đồ (Google Maps/Mapbox) hiện vị trí Player + đối thủ gần + sân. Filter bar cho phép lọc theo môn/trình độ/bán kính. Overlay danh sách đối thủ phù hợp. | P0 | CAP-03 |
| FR-sport-matching-006 | Chọn sân + slot giờ | Player browse sân theo vị trí + môn hỗ trợ. Hiển thị slot giờ trống kèm giá. Player chọn slot. Nếu hết slot, gợi ý sân/giờ khác (E-sport-matching-007). | P0 | CAP-04 |
| FR-sport-matching-007 | Giữ chỗ tạm (Slot Lock) | System lock slot sân đã chọn trong 5 phút (Pessimistic Locking). Nếu hết 5 phút chưa confirm match, auto release slot về trạng thái Trống. Concurrent lock: chỉ 1 Player lock được, người sau nhận thông báo slot hết. | P0 | CAP-04 |
| FR-sport-matching-008 | Gửi invite ghép đôi | Player gửi invite cho đối thủ đã chọn. System gửi push notification qua FCM. Invite có timeout 5 phút. Free player giới hạn 10 invite/ngày/môn (reset 00:00). Vượt limit hiện E-sport-matching-005. | P0 | CAP-05 |
| FR-sport-matching-009 | Phản hồi invite | Đối thủ nhận invite, xem thông tin (người mời + sân + giờ), chọn Accept hoặc Reject. Accept dẫn tới confirm match. Reject dẫn tới thông báo Player gốc (E-sport-matching-003) + release slot. Timeout 5 phút dẫn tới auto hủy + release slot + system tìm đối thủ tiếp theo Matching Score. Nếu không còn đối thủ phù hợp → E-sport-matching-006 + release slot. | P0 | CAP-05 |
| FR-sport-matching-010 | Xác nhận trận đấu | Khi đối thủ Accept, system tạo Match (status: Đã confirm). Cả 2 Player nhận notification: thông tin đối thủ + sân + giờ + vị trí bản đồ. Nhắc nhở trước trận 1 giờ. Nếu match confirmed < 1 giờ trước giờ chơi → gửi nhắc nhở ngay lập tức. | P0 | CAP-05 |
| FR-sport-matching-011 | Đánh giá đối thủ | Sau trận hoàn thành, system gửi nhắc nhở đánh giá. Player chấm rating (1-5 sao) + nhận xét text (optional). System cập nhật rating trung bình đối thủ. | P0 | CAP-06 |
| FR-sport-matching-012 | Lịch sử trận + thống kê | Player xem danh sách trận đã chơi (sân, giờ, đối thủ, kết quả). Thống kê tổng: win/loss per môn, rating nhận từ đối thủ. Filter theo môn thể thao. | P0 | CAP-07 |
| FR-sport-matching-013 | Thanh toán online | Tích hợp MoMo + VNPay. Player thanh toán đặt sân qua app. System thu commission 12% cố định trên tổng giá trị đặt chỗ. Thay thế thanh toán tại sân (v1.0). | P1 | CAP-08 |
| FR-sport-matching-014 | Auto-adjust trình độ | Hệ thống ELO-based: nếu Player cấp Trung bình liên tục thắng/nhận rating cao từ đối thủ cùng bậc, tự động chuyển sang Nâng cao. Ngược lại tương tự. Cập nhật hồ sơ + Matching Score. | P1 | CAP-09 |
| FR-sport-matching-015 | Partner đăng ký sân | Partner đăng ký thông tin sân: tên, địa chỉ, tọa độ, môn hỗ trợ, slot giờ, giá. Manual KYC qua Zalo để xác thực. Staff hỗ trợ onboard. | P1 | CAP-10 |
| FR-sport-matching-016 | Ví điện tử nội bộ | In-app Wallet: Player xem số dư, nạp tiền, rút tiền. Hoàn tiền hủy trận dạng điểm thưởng/tiền điện tử (giảm refund fee qua ngân hàng). | P1 | CAP-11 |
| FR-sport-matching-017 | Premium subscription | Player mua gói Premium 49.000 VND/tháng. Unlock unlimited invite/ngày (bỏ giới hạn 10/ngày/môn). Gợi ý upgrade khi đạt limit free (E-sport-matching-005). | P1 | CAP-12 |
| FR-sport-matching-018 | Hủy trận + Hoàn tiền | Player hủy trận đã confirm. Max 3 lần/tháng. Cooldown 15 phút nếu hủy 2 liên tiếp/1 giờ. Ma trận hoàn tiền: >24h hoàn 100%, 6-24h hoàn 50% + đền bù sân 40%, <6h không hoàn + đền bù sân 90%. Hoàn qua Ví nội bộ. | P2 | CAP-13 |
| FR-sport-matching-019 | Phát hiện đánh giá ác ý | Thuật toán phát hiện mẫu bất thường (vd: 1 player luôn rate 1 sao). Admin xem xét + loại bỏ đánh giá ác ý. Dùng rating trung bình nhiều trận giảm tác động đánh giá đơn lẻ. | P2 | CAP-14 |
| FR-sport-matching-020 | Báo cáo quản trị | Admin dashboard: số user, số trận, revenue, slot occupancy, analytics. Aggregated data tối ưu truy vấn báo cáo. | P2 | CAP-15 |
| FR-sport-matching-021 | Report kết quả trận | Sau trận hoàn thành, cả 2 Player tự report kết quả (Thắng/Thua/Hòa). Nếu 2 bên report khớp → ghi nhận. Nếu conflict (cả 2 claim thắng) → flag cho Admin review. Kết quả dùng cho thống kê win/loss (FR-012). | P0 | CAP-16 |
| FR-sport-matching-022 | Tìm sân độc lập | Player tìm sân theo bộ lọc: môn thể thao, khu vực, ngày, khoảng giá, hoặc combo. Kết quả hiển thị danh sách sân (hình ảnh, giá, đánh giá, khoảng cách). Lịch trống cập nhật real-time. | P0 | CAP-17 |
| FR-sport-matching-023 | Xem chi tiết sân | Player xem: hình ảnh (≥3), giá/giờ, lịch trống real-time, đánh giá trung bình, tiện ích, vị trí bản đồ. Chọn sân con cụ thể (Sân A, Sân B...) + xem khung giờ trống. | P0 | CAP-17 |
| FR-sport-matching-024 | Đặt sân — thanh toán ngay | Player chọn sân con + khung giờ. System tạm giữ 10 phút (tránh concurrent). v1.0: xác nhận booking + thanh toán tại sân (cash, theo BR-011). v1.1+: thanh toán online qua MoMo/VNPay (khi FR-013 P1 ready). Booking tạo trạng thái confirmed (v1.0) hoặc paid (v1.1+). Gửi noti chủ sân. | P0 | CAP-18 |
| FR-sport-matching-025 | Đặt sân — giữ chỗ | Player chọn "Giữ chỗ trước". Booking trạng thái pending, 30 phút để thanh toán. Hết 30p → expired auto. | P0 | CAP-18 |
| FR-sport-matching-026 | Chủ sân duyệt booking | Chủ sân nhận noti, duyệt/từ chối trong 30 phút. Duyệt → confirmed + noti user. Từ chối → hoàn tiền auto + noti user. Hết 30p không duyệt → auto hủy + hoàn tiền. | P0 | CAP-18 |
| FR-sport-matching-027 | Hủy booking sân | Player hủy booking confirmed. Chính sách: >24h hoàn 100%, 12-24h hoàn 75%, 2-12h hoàn 50%, <2h hoàn 0%. Gửi noti chủ sân. | P0 | CAP-19 |
| FR-sport-matching-028 | Đổi giờ/sân booking | Player đổi 1 lần nếu trước 24h. Trong 24h hoặc đã đổi → phải hủy + đặt mới. Gửi noti chủ sân. | P1 | CAP-19 |
| FR-sport-matching-029 | Đánh giá sân | Sau buổi chơi, Player đánh giá 1-5 sao + review text (optional). Cập nhật đánh giá trung bình sân. Cộng điểm thưởng. Deadline 7 ngày có thưởng, sau đó vẫn đánh giá được. 1 đánh giá per booking. | P1 | CAP-20 |
| FR-sport-matching-030 | Chủ sân đăng sân | Chủ sân nhập: tên, địa chỉ, tọa độ, môn, giá/giờ, tiện ích, ≥3 ảnh (max 10, 5MB/tấm), sân con, khung giờ hoạt động. Submit → pending_review. Admin duyệt → active. Từ chối → gửi lý do. | P0 | CAP-21 |
| FR-sport-matching-031 | Chủ sân block khung giờ | Chủ sân chặn khung giờ (bảo trì, khách offline). Blocked slot không hiển thị cho Player. | P0 | CAP-21 |
| FR-sport-matching-032 | Cảnh báo/khóa chủ sân | 3 lần không duyệt booking trong 30p → cảnh báo. 5 lần → tạm khóa sân. Admin mở lại. | P1 | CAP-21 |
| FR-sport-matching-033 | Chat 1-1 | Player chat real-time với Player khác (sau match hoặc từ profile) và với chủ sân (từ venue-detail). Gửi text + ảnh. Lưu lịch sử. Hiện trạng thái online/offline. Player có thể block user khác (chặn gửi tin). Player có thể report tin nhắn vi phạm. Admin có thể xóa/ẩn tin nhắn vi phạm (mở rộng FR-046). | P1 | CAP-22 |
| FR-sport-matching-034 | Danh sách hội thoại | Hiện danh sách chat threads sắp theo tin nhắn mới nhất. Badge số tin chưa đọc. Tap vào thread → mở chat. | P1 | CAP-22 |
| FR-sport-matching-035 | Notification Center | Icon chuông trên header với badge đếm noti chưa đọc. Tap → danh sách noti (mới nhất trước). Đánh dấu đã đọc (tap từng cái hoặc "Đọc tất cả"). Tap noti → deep link đến màn hình liên quan. | P1 | CAP-23 |
| FR-sport-matching-036 | Cài đặt notification | Player bật/tắt từng loại noti: booking, match, chat, đánh giá, khuyến mãi. Mặc định tất cả ON. | P1 | CAP-23 |
| FR-sport-matching-037 | Xem/sửa profile | Player xem và sửa: tên hiển thị, avatar (upload ảnh), email (verify lại nếu đổi). Xem thống kê: rating, matches, win/loss. | P1 | CAP-24 |
| FR-sport-matching-038 | Đổi mật khẩu | Player đổi mật khẩu: nhập mật khẩu cũ + mật khẩu mới (min 8, ≥1 chữ hoa + ≥1 số). Confirm thành công. | P1 | CAP-24 |
| FR-sport-matching-039 | Cài đặt riêng tư | Player toggle: ẩn profile khỏi tìm kiếm đối thủ, ẩn vị trí GPS. Ẩn profile → không xuất hiện trên bản đồ matching. | P1 | CAP-24 |
| FR-sport-matching-040 | Xóa tài khoản | Player yêu cầu xóa tài khoản. Confirm 2 bước (nhập mật khẩu + xác nhận). Xóa sau 30 ngày grace period. Hủy booking pending + hoàn tiền. Match confirmed chưa diễn ra → auto hủy + notify đối thủ + hoàn tiền theo BR-009. Số dư wallet > 0 → chuyển về MoMo/VNPay trong 7 ngày. Đăng nhập lại trong 30 ngày → hủy xóa. | P1 | CAP-24 |
| FR-sport-matching-041 | Wallet — điểm thưởng giảm giá | Điểm thưởng (từ đánh giá sân/đối thủ) dùng giảm giá khi đặt sân. Quy đổi: 100 điểm = 10.000đ giảm. Hiện số dư điểm + lịch sử tích lũy/sử dụng. | P1 | CAP-11 |
| FR-sport-matching-042 | Admin — Quản lý user | Admin xem danh sách user (Player/Partner). Tìm kiếm, filter theo role/status. Xem chi tiết profile. Tạm khóa / mở khóa tài khoản. | P1 | CAP-25 |
| FR-sport-matching-043 | Admin — Quản lý sân | Admin xem danh sách sân, filter theo status. Duyệt/từ chối sân pending. Khóa/mở sân. Xem đánh giá + report. | P1 | CAP-25 |
| FR-sport-matching-044 | Admin — Quản lý booking | Admin xem danh sách booking, filter theo status/ngày/sân. Xem chi tiết. Xử lý tranh chấp (dispute). | P1 | CAP-25 |
| FR-sport-matching-045 | Admin — Dashboard doanh thu | Tổng quan: số user active, số trận, số booking, revenue (commission + premium), slot occupancy rate. Filter theo khoảng thời gian. | P1 | CAP-25 |
| FR-sport-matching-046 | Admin — Moderate đánh giá | Admin xem đánh giá bị report/flag. Ẩn/xóa đánh giá vi phạm. Cảnh báo user vi phạm. | P1 | CAP-25 |
| FR-sport-matching-047 | Onboarding chủ sân tự động | Partner đăng ký trên app: nhập thông tin cá nhân/doanh nghiệp + CMND/CCCD + giấy phép kinh doanh (upload ảnh). Xác nhận điều khoản sử dụng. System auto verify (OCR hoặc manual review). Approved → Partner role activated. | P1 | CAP-26 |
| FR-sport-matching-048 | Tạo đội | Captain tạo đội: đặt tên đội, chọn môn, mời thành viên (từ contacts/search). Đội có ≥2 người. Captain quản lý: thêm/xóa thành viên, giải tán đội. | P2 | CAP-27 |
| FR-sport-matching-049 | Ghép đội vs đội | System ghép random 2 đội theo Team Matching Score (trung bình Matching Score các thành viên). Cùng flow slot lock + invite như 1v1 nhưng Captain đại diện confirm. | P2 | CAP-27 |
| FR-sport-matching-050 | Tạo giải đấu | Player tạo giải tự phát (miễn phí, tối thiểu 4 đội tham gia — mỗi đội ≥1 người hoặc ≥1 cá nhân tuỳ format). Admin/Partner/cộng đồng tạo giải chính thức (có phí đặt cọc). Chọn format: bracket hoặc round-robin. Đặt lịch, chọn sân, mô tả giải. | P2 | CAP-28 |
| FR-sport-matching-051 | Quản lý giải đấu | Người tạo giải quản lý: duyệt đăng ký, sắp bảng đấu, cập nhật kết quả, xử lý bỏ cuộc. Bảng xếp hạng tự động. Thông báo lịch thi đấu cho người tham gia. | P2 | CAP-28 |
| FR-sport-matching-052 | Phí đặt cọc giải | Giải cộng đồng lớn: người tham gia nộp phí đặt cọc qua Wallet/payment. Hoàn cọc nếu tham gia đầy đủ (hoàn thành tất cả trận được xếp). Không hoàn nếu người tham gia bỏ giữa chừng. Nếu người tổ chức hủy giải trước khi bắt đầu → hoàn 100% cọc cho tất cả người đăng ký. Nếu người tổ chức hủy giải sau khi đã bắt đầu → hoàn theo tỷ lệ trận chưa thi đấu. Admin/người tạo quyết định mức phí. | P2 | CAP-28 |
| FR-sport-matching-053 | Đăng bài Social Feed | Player đăng bài: text + ảnh (max 5) + video (max 1, ≤30s). Hiển thị trên timeline followers. Chia sẻ kết quả trận (auto-generate card). | P2 | CAP-29 |
| FR-sport-matching-054 | Like + Comment | Player like/unlike bài viết. Comment text (max 500 ký tự). Reply comment. Notification khi bài được like/comment. | P2 | CAP-29 |
| FR-sport-matching-055 | Follow Player | Player follow/unfollow player khác. Feed timeline hiện bài từ người đang follow (mới nhất trước). Gợi ý follow dựa trên match history (đã chơi ≥1 trận cùng nhau và chưa follow). Algorithm TBD P2 sprint — BA note: cần define threshold và số lượng gợi ý tối đa. | P2 | CAP-29 |
| FR-sport-matching-056 | Moderate Social Feed | Admin ẩn/xóa bài vi phạm. Player report bài. Auto-flag nội dung nghi ngờ. Cảnh báo/khóa user vi phạm nhiều lần. | P2 | CAP-29 |
| FR-sport-matching-057 | Voucher giảm giá | Admin tạo voucher: code, % giảm hoặc số tiền, điều kiện (min booking, môn, khu vực), số lượng, thời hạn. Player nhập code khi đặt sân → áp dụng giảm giá. | P2 | CAP-30 |
| FR-sport-matching-058 | Mã referral | Player có mã referral cá nhân. Mời bạn đăng ký: người mời + người được mời nhận thưởng (điểm hoặc voucher). Tracking referral chain. Chống gian lận (1 device = 1 referral). | P2 | CAP-30 |
| FR-sport-matching-059 | Chiến dịch khuyến mãi tự động | System tự động trigger voucher: chào mừng user mới (first booking), birthday, inactive 30 ngày (win-back), milestone (10 trận). Admin cấu hình rules + budget. Dashboard tracking hiệu quả. | P2 | CAP-30 |

## 3. Non-Functional Requirements (NFR)

| ID | Category | Requirement | Acceptance |
|----|----------|-------------|------------|
| NFR-sport-matching-001 | Performance | Thời gian quét đối thủ + hiện kết quả trên bản đồ | < 3 giây (P95) |
| NFR-sport-matching-002 | Performance | Thời gian gửi/nhận push notification (invite) | < 2 giây (P95) |
| NFR-sport-matching-003 | Availability | Uptime hệ thống | ≥ 99.5% monthly |
| NFR-sport-matching-004 | Security | Mật khẩu mã hóa, OTP có thời hạn | OTP expire sau 5 phút |
| NFR-sport-matching-005 | Security | Dữ liệu vị trí GPS chỉ dùng cho matching/booking | Không chia sẻ cho mục đích ngoài matching/booking. Google Maps API nhận location data theo ToS. Tuân thủ privacy policy VN |
| NFR-sport-matching-006 | Scalability | Hỗ trợ đồng thời | 1.000 MAU, 100 concurrent users |
| NFR-sport-matching-007 | Usability | Số bước từ mở app đến confirm trận | ≤ 5 tap |
| NFR-sport-matching-008 | Security (Payment) | Tất cả payment call dùng idempotency key. Không lưu raw card/account number. Booking + commission + wallet update phải atomic (saga pattern). HTTPS TLS 1.2+ bắt buộc toàn bộ payment API | Saga compensation: payment confirm nhưng booking fail → auto refund qua gateway trong 60s |
| NFR-sport-matching-009 | Performance (Chat) | Chat message delivery latency | < 500ms (P95) trên 4G. WebSocket + pub/sub broker. Presigned URL cho image upload (không qua app server) |
| NFR-sport-matching-010 | Privacy (GPS) | Location chỉ collect khi app foreground + user trên map-search. Không background tracking. Lưu tọa độ approximate (±500m) cho matching. Không log raw GPS history. Consent dialog lần đầu | Tuân thủ Nghị định 13/2023/NĐ-CP |
| NFR-sport-matching-011 | Scalability | Hỗ trợ 3x spike (300 concurrent) peak hours. Stateless API design cho horizontal scale. WebSocket load-balanced qua Redis pub/sub | Design headroom 10x growth |
| NFR-sport-matching-012 | Security (Auth) | Auth token JWT expiry 24h, refresh token 30 ngày. Rate limit: 5 failed login/15 phút per IP. Partner chỉ manage sân/slot/booking thuộc sân mình | Role-based access control matrix bắt buộc |

## 4. Business Rules

| ID | Rule | Trigger | Source |
|----|------|---------|--------|
| BR-sport-matching-001 | Matching Score = Môn 100% hard filter + Vị trí 40% + Trình độ 40% + Rating 20% | Khi Player tìm đối thủ | Brainstorm OQ-1 |
| BR-sport-matching-002 | Invite timeout 5 phút. Hết hạn: auto hủy invite + release slot + rotate đối thủ tiếp theo Matching Score | Khi gửi invite | Brainstorm §6 |
| BR-sport-matching-003 | Pessimistic Slot Locking 5 phút. Hết hạn: auto release slot về Trống | Khi Player chọn slot sân | Brainstorm §6 |
| BR-sport-matching-004 | Free player: 10 invite/ngày/môn, reset 00:00. Premium: unlimited | Khi gửi invite | Brainstorm §7.2 |
| BR-sport-matching-005 | 1 match pending tối đa per Player. Không cho tạo match mới khi có match đang chờ confirm | Khi Player muốn tạo match | Brainstorm §6.4 |
| BR-sport-matching-006 | Concurrent invite: First-come-first-served. 2 Player gửi invite cùng 1 đối thủ → ai đến trước được phục vụ | Khi 2 invite concurrent | Brainstorm §7 |
| BR-sport-matching-007 | Trình độ 3 bậc: Mới chơi (Beginner) / Trung bình (Intermediate) / Nâng cao (Advanced). Mỗi môn trình độ riêng | Khi setup profile, khi matching | Brainstorm OQ-2 |
| BR-sport-matching-008 | Commission cố định 12% trên tổng giá trị đặt chỗ | Khi booking thành công (P1) | BRD OQ-1, PRD OQ-1 |
| BR-sport-matching-009 | Ma trận Hoàn tiền: >24h hoàn 100%, 6-24h hoàn 50% Player + đền bù 40% chủ sân, <6h không hoàn + đền bù 90% chủ sân. Hoàn qua Ví nội bộ | Khi Player hủy trận (P2) | BRD OQ-3 |
| BR-sport-matching-010 | Hủy match: max 3/tháng. Cooldown 15 phút nếu hủy 2 liên tiếp trong 1 giờ | Khi Player hủy trận (P2) | Brainstorm OQ-3 |
| BR-sport-matching-011 | v1.0 thanh toán tại sân (cash). App chỉ giữ chỗ, không thu tiền online | Khi đặt sân v1.0 | PRD OQ-3 |
| BR-sport-matching-012 | Chỉ hỗ trợ 1v1. 2v2+ là future scope | Khi tạo match | PRD OQ-2 |
| BR-sport-matching-013 | Player mới (< 5 trận): rating weight = 0, redistribute sang vị trí 50% + trình độ 50%. Sau ≥5 trận áp dụng full formula (vị trí 40% + trình độ 40% + rating 20%) | Khi matching Player mới | Review #8 |
| BR-sport-matching-014 | Tạm giữ khung giờ sân 10 phút khi Player chọn (tránh concurrent booking). Hết 10p chưa thanh toán → giải phóng slot | Khi Player chọn slot sân | Brainstorm venue |
| BR-sport-matching-015 | Giữ chỗ sân 30 phút chưa thanh toán → auto expired | Khi Player chọn "Giữ chỗ" | Brainstorm venue |
| BR-sport-matching-016 | Chủ sân duyệt booking trong 30 phút. Hết hạn → auto hủy + hoàn tiền 100% | Khi booking paid | Brainstorm venue |
| BR-sport-matching-017 | Hoàn tiền hủy booking sân: >24h hoàn 100%, 12-24h hoàn 75%, 2-12h hoàn 50%, <2h hoàn 0% | Khi Player hủy booking | Brainstorm venue |
| BR-sport-matching-018 | Đổi giờ/sân: max 1 lần per booking, chỉ trước 24h | Khi Player đổi booking | Brainstorm venue |
| BR-sport-matching-019 | Max 3 booking đồng thời per Player (pending + confirmed) | Khi Player đặt sân mới | Brainstorm venue |
| BR-sport-matching-020 | Đặt sân trước tối đa 14 ngày, sớm nhất 2 giờ trước giờ chơi | Khi Player chọn ngày/giờ | Brainstorm venue |
| BR-sport-matching-021 | Hình ảnh sân: tối thiểu 3, tối đa 10, max 5MB/tấm | Khi chủ sân đăng sân | Brainstorm venue |
| BR-sport-matching-022 | Admin duyệt sân mới trước khi hiển thị cho Player | Khi chủ sân submit sân | Brainstorm venue |
| BR-sport-matching-023 | Chủ sân không duyệt 3 lần → cảnh báo, 5 lần → tạm khóa sân | Khi hết 30p duyệt | Brainstorm venue |
| BR-sport-matching-024 | Đánh giá sân: 1 đánh giá per booking, deadline 7 ngày có điểm thưởng | Khi Player đánh giá | Brainstorm venue |
| BR-sport-matching-025 | Authorization matrix: Player chỉ manage booking/profile mình. Partner chỉ manage sân/slot/booking thuộc sân mình. Admin full access. Guest chỉ đọc (xem sân, không đặt). Staff manage slot/booking sân được gán | Mọi API call | Review tech |
| BR-sport-matching-026 | Slot lock shared key space: match flow (5p) và venue booking flow (10p) dùng chung lock — 1 slot chỉ 1 owner tại 1 thời điểm. Lock tự expire theo TTL | Khi lock slot | Review tech |

## 5. Error Matrix

| Error ID | Title | Trigger | Message | Screen | Recovery |
|----------|-------|---------|---------|--------|----------|
| E-sport-matching-001 | GPS tắt | Player mở matching khi GPS off/mất quyền | "Không thể tìm kiếm đối thủ. Vui lòng bật Quyền truy cập vị trí để thuật toán Matchmaking hoạt động." | map-search | Player bật GPS, system resume |
| E-sport-matching-002 | Invite hết hạn | Đối thủ không phản hồi trong 5 phút | "Yêu cầu ghép đôi đã hết hạn (5 phút). Slot sân đã được giải phóng. Vui lòng thử tìm đối thủ khác." | map-search (invite-waiting state) | Auto release slot, Player tìm đối thủ khác |
| E-sport-matching-003 | Đối thủ từ chối | Đối thủ nhấn Reject | "Đối thủ đã từ chối trận đấu. Rất tiếc, bạn có muốn thử tìm Match mới ngay bây giờ không?" | map-search (invite-waiting state) | Release slot, Player chọn đối thủ khác |
| E-sport-matching-004 | Match pending | Player tạo match mới khi đã có match chờ confirm | "Bạn đang có một trận đấu đang chờ xác nhận. Vui lòng hủy trận đấu hiện tại hoặc đợi kết quả trước khi tạo Match mới." | map-search | Hủy match cũ hoặc đợi timeout |
| E-sport-matching-005 | Hết limit invite | Free player đã gửi 10 invite/ngày cho 1 môn | "Bạn đã hết lượt gửi lời mời hôm nay. Nâng cấp Premium để không giới hạn." | map-search | Đợi reset 00:00 hoặc mua Premium |
| E-sport-matching-006 | Không tìm thấy đối thủ | Không có đối thủ phù hợp trong bán kính + trình độ | "Không tìm thấy đối thủ nào trong khu vực của bạn. Thử mở rộng bán kính hoặc điều chỉnh trình độ?" | map-search | Mở rộng filter (bán kính, trình độ) |
| E-sport-matching-007 | Sân hết slot | Sân không còn slot trống trong khung giờ chọn | "Sân này hết slot trong khung giờ bạn chọn. Xem sân/giờ khác?" | court-select | Gợi ý sân/giờ khác |
| E-sport-matching-008 | Hủy vượt limit | Player đã hủy 3 match/tháng | "Đã đạt giới hạn hủy tháng này." | match-confirmed | Đợi tháng sau |
| E-sport-matching-009 | Cooldown hủy | Player hủy 2 match liên tiếp trong 1 giờ | "Vui lòng đợi {mm:ss} trước khi tạo trận mới." | map-search | Đợi hết cooldown 15 phút |
| E-sport-matching-010 | Khung giờ đã đặt | Player chọn slot đã bị người khác tạm giữ/đặt | "Khung giờ này đã có người đặt, vui lòng chọn giờ khác" | venue-detail | Chọn giờ khác |
| E-sport-matching-011 | Hết giữ chỗ sân | Hết 30 phút giữ chỗ chưa thanh toán | "Đã hết 30 phút giữ chỗ, booking đã được hủy" | booking-detail | Đặt lại |
| E-sport-matching-012 | Chủ sân từ chối booking | Chủ sân nhấn Từ chối | "Chủ sân đã từ chối booking, tiền sẽ được hoàn trong 24h" | booking-detail | Đặt sân khác |
| E-sport-matching-013 | Quá 3 booking | Player đã có 3 booking pending/confirmed | "Bạn đang có 3 booking, vui lòng hoàn tất hoặc hủy trước khi đặt thêm" | venue-detail | Quản lý booking hiện có |
| E-sport-matching-014 | Đặt sân sát giờ | Player đặt sân < 2 giờ trước giờ chơi | "Chỉ có thể đặt sân trước tối thiểu 2 giờ" | venue-detail | Chọn giờ khác |
| E-sport-matching-015 | Gửi ảnh chat thất bại | Ảnh > 10MB hoặc format không hỗ trợ | "Không thể gửi ảnh. Vui lòng chọn ảnh dưới 10MB (JPG/PNG)" | chat-detail | Chọn ảnh khác |
| E-sport-matching-016 | Mật khẩu cũ sai | Player nhập sai mật khẩu hiện tại khi đổi | "Mật khẩu hiện tại không đúng" | settings | Nhập lại |
| E-sport-matching-017 | Mật khẩu mới không đủ mạnh | Mật khẩu mới < 8 ký tự hoặc thiếu chữ hoa/số | "Mật khẩu phải có ít nhất 8 ký tự, bao gồm chữ hoa và số" | settings | Nhập lại |
| E-sport-matching-018 | Xóa tài khoản có booking pending | Player xóa tài khoản khi còn booking chưa hoàn thành | "Bạn còn booking chưa hoàn thành. Vui lòng hủy trước khi xóa tài khoản" | settings | Hủy booking trước |
| E-sport-matching-019 | Onboarding thiếu giấy tờ | Partner submit mà chưa upload CMND hoặc giấy phép | "Vui lòng upload đầy đủ CMND/CCCD và giấy phép kinh doanh" | partner-onboard | Upload thêm |
| E-sport-matching-020 | Chat mất kết nối | WebSocket disconnect giữa chat | "Mất kết nối. Đang thử kết nối lại..." | chat-detail | Auto retry 3 lần, fallback offline queue |
| E-sport-matching-021 | Bản đồ không khả dụng | Google Maps API down/timeout | "Không thể tải bản đồ. Hiển thị danh sách sân thay thế" | map-search, venue-search | Fallback list-view với khoảng cách text |
| E-sport-matching-022 | Thanh toán timeout | Payment gateway không phản hồi trong 60s | "Đang xử lý thanh toán, vui lòng đợi... Nếu bị trừ tiền mà chưa nhận xác nhận, liên hệ hỗ trợ" | booking-confirm | Polling 30s, sau 60s treat as failed |
| E-sport-matching-023 | Push noti fail | FCM delivery thất bại | (Silent — không hiện user) | — | Fallback in-app noti khi opponent mở app, invite timer vẫn chạy |
| E-sport-matching-024 | Đã đổi giờ/sân 1 lần | Player đổi booking lần thứ 2 | "Bạn đã đổi 1 lần. Vui lòng hủy và đặt mới nếu cần thay đổi" | booking-detail | Nút Đổi disabled |
| E-sport-matching-025 | Đổi trong 24h | Player đổi booking khi giờ chơi < 24h | "Chỉ đổi được trước 24h. Bạn có thể hủy theo chính sách hoàn tiền" | booking-detail | Hướng dẫn hủy |
| E-sport-matching-026 | Đội chưa đủ người | Captain tìm match khi đội < 2 người | "Đội cần ít nhất 2 thành viên để tìm trận" | team-manage | Mời thêm thành viên |
| E-sport-matching-027 | Giải đầy slot | Player đăng ký giải đã đủ số lượng | "Giải đấu đã đủ số lượng đăng ký" | tournament-detail | Tìm giải khác |
| E-sport-matching-028 | Bài viết vi phạm | Bài bị report hoặc auto-flag | "Bài viết đã bị ẩn do vi phạm quy định cộng đồng" | social-feed | Liên hệ hỗ trợ |
| E-sport-matching-029 | Voucher không hợp lệ | Code sai, hết hạn, hết lượt, không đủ điều kiện | "Mã giảm giá không hợp lệ hoặc đã hết hạn" | booking-confirm | Nhập mã khác |
| E-sport-matching-030 | Referral gian lận | Cùng device referral nhiều lần | "Mã giới thiệu không thể sử dụng trên thiết bị này" | register | — |
| E-sport-matching-031 | Đội đối phương không phản hồi | Captain gửi team invite nhưng đội đối phương không phản hồi trong 5 phút (timeout team matching) | "Đội đối phương không phản hồi. Slot sân đã được giải phóng. Vui lòng thử tìm đội khác." | team-manage | Auto release slot, Captain tìm đội khác |

## 6. Data Entities (tóm tắt — chi tiết ở erd.md)

| Entity | Mô tả | Key attributes |
|--------|-------|----------------|
| Player | Người chơi | name, email, password, avatar |
| Sport | Danh mục môn thể thao | name, icon |
| PlayerSport | Trình độ Player per môn (N:N) | skill_level, rating_avg, matches_played, wins, losses |
| Partner | Chủ sân | name, contact, address, kyc_status |
| Court | Sân thể thao | name, address, lat, lng |
| CourtSport | Môn sân hỗ trợ (N:N) | — (junction) |
| Slot | Suất giờ sân | date, start_time, end_time, price, status |
| Match | Trận đấu | sport_id, status, result, result_reported_by, created_at |
| Invite | Lời mời ghép đôi | status, expires_at |
| Rating | Đánh giá sau trận | score, comment |
| Wallet | Ví điện tử (P1) | balance |
| WalletTransaction | Giao dịch ví (P1) | amount, type |
| Venue | Sân thể thao (đặt sân độc lập) | name, address, lat, lng, status, rating_avg, review_count |
| SubCourt | Sân con (thuộc Venue) | name |
| VenueSlot | Slot giờ sân con | date, start/end_time, price, status, locked_by, lock_expires_at |
| Booking | Đặt sân | player_id, vslot_id, status, amount, refund_amount, change_count |
| VenueReview | Đánh giá sân | booking_id, player_id, score, comment, reward_points |
| VenueImage | Ảnh sân | venue_id, url, sort_order |
| ChatThread | Hội thoại chat | participant_ids, last_message_at |
| Message | Tin nhắn chat | thread_id, sender_id, content, image_url, read_at |
| Notification | Thông báo | player_id, type, title, body, deep_link, read_at |
| PointTransaction | Giao dịch điểm thưởng | player_id, amount, type (earn/spend), reference |

Chi tiết ERD: [[docs/sport-matching/srs/erd.md|ERD Sport Matching]]

## 7. Flows (tóm tắt — chi tiết ở flows.md)

| Flow | Type | Related UC | Related FR |
|------|------|-----------|------------|
| Matching + Booking | Sequence | uc-find-opponent, uc-book-match | FR-003 đến FR-010 |
| Registration + OTP | Sequence | uc-register | FR-001, FR-002 |
| Rating + Auto-adjust | Sequence | uc-rate-opponent | FR-011, FR-014 |
| Venue Booking | Sequence | uc-search-venue, uc-book-venue | FR-022 đến FR-027, FR-030-031 |
| Venue Booking Cancel/Change | Sequence | uc-cancel-venue-booking | FR-027, FR-028 |

Chi tiết flows: [[docs/sport-matching/srs/flows.md|Flows Sport Matching]]

## 8. Screens (tóm tắt — chi tiết ở ascii-screen/)

| Screen | Purpose | Related UC |
|--------|---------|-----------|
| register | Đăng ký tài khoản | uc-register |
| otp-verify | Xác thực OTP email | uc-register |
| profile-setup | Chọn môn + trình độ | uc-register |
| map-search | Bản đồ tìm đối thủ (MAIN) | uc-find-opponent |
| opponent-profile | Xem profile đối thủ | uc-find-opponent |
| court-select | Chọn sân + slot giờ | uc-book-match |
| invite-confirm | Xác nhận gửi invite | uc-book-match |
| invite-waiting | Chờ đối thủ phản hồi (countdown 5p, cancel option) | uc-book-match |
| invite-receive | Đối thủ nhận invite | uc-book-match |
| match-confirmed | Trận xác nhận thành công | uc-book-match |
| match-history | Lịch sử trận + thống kê | uc-view-history |
| rate-opponent | Đánh giá đối thủ | uc-rate-opponent |
| player-profile | Xem/sửa profile cá nhân | cross-UC |
| venue-search | Tìm sân theo bộ lọc | uc-search-venue |
| venue-detail | Chi tiết sân + chọn slot | uc-search-venue, uc-book-venue |
| booking-confirm | Xác nhận đặt sân | uc-book-venue |
| booking-detail | Chi tiết booking | uc-book-venue, uc-cancel-venue-booking |
| venue-rate | Đánh giá sân | uc-rate-venue |
| venue-manage | Quản lý sân (chủ sân) | uc-manage-venue |
| chat-list | Danh sách hội thoại | uc-chat |
| chat-detail | Chat 1-1 | uc-chat |
| notification-center | Trung tâm thông báo | cross-UC |
| settings | Cài đặt & Profile | uc-profile-settings |
| admin-dashboard | Dashboard quản trị | uc-admin |
| partner-onboard | Onboarding chủ sân | uc-partner-onboard |

Chi tiết screens: [[docs/sport-matching/ascii-screen/_index.md|Screens Sport Matching]]

## 9. Constraints & Assumptions

**Constraints:**
- Mobile only: Android + iOS (TestFlight giai đoạn đầu). Tất cả roles chung 1 app.
- Internet liên tục bắt buộc (GPS, push notification, giao dịch).
- Tiếng Việt only.
- GPS bắt buộc cho matching.
- Map provider: Google Maps API / Mapbox.
- Push notification: Firebase Cloud Messaging (FCM).
- Payment gateway (P1): MoMo + VNPay.
- OTP: email (chính), SMS (giai đoạn sau).
- v1.0 thanh toán tại sân (cash), app chỉ giữ chỗ.

**Assumptions:**
- Player sở hữu smartphone đời ≥2020, có GPS, Internet 4G+.
- Partner cung cấp data slot chính xác và cập nhật.
- Thị trường VN, thành phố lớn giai đoạn đầu.
- Peak hours: 17h-22h ngày thường + cả ngày cuối tuần.

## 10. Open Questions

- [x] OQ-1: Matching Score algorithm — Resolved: tuyến tính theo khoảng cách (km). Player mới (<5 trận) rating weight=0, redistribute: vị trí 50% + trình độ 50% (đã ghi BR-013). Sau ≥5 trận: full formula 40/40/20.
- [x] OQ-2: ELO auto-adjust ngưỡng — Resolved: thắng ≥3 trận liên tiếp VÀ rating trung bình nhận ≥4.0 từ ≥5 trận gần nhất → tăng 1 bậc. Thua ≥3 liên tiếp VÀ rating ≤2.0 → giảm 1 bậc. Có giảm bậc ngược. Max 1 lần tăng/giảm per tháng.
