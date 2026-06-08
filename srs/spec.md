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
  - 2026-06-07 | /review | round 2 by @senior-ba: approve, 2 warnings applied (FR-021 source→CAP-16, Match entity +result fields). Status revisions→in-review
  - 2026-06-07 | /review | round 1 by 6 agents: 1 blocking applied (FR-021), 7 warnings applied. Status draft→revisions
  - 2026-06-04 | /srs | [states] initial 3 entity state machines: Match, Slot, Invite
  - 2026-06-04 | /srs | [flows] initial 3 sequence flows: Registration, Matching+Booking, Rating
  - 2026-06-04 | /srs | [erd] initial 12 entities, 14 relationships
  - 2026-06-04 | /srs | initial spec: 20 FR, 7 NFR, 12 BR, 9 errors, 6 UCs, 12 screens
---

# Sport Matching — Software Requirements Specification

> Kỹ thuật hoá scope đã chốt trong PRD. FR/NFR/business rules/error cụ thể.

## 1. Scope

SRS này cover toàn bộ tính năng Sport Matching: hệ thống matching thể thao 1v1 theo GPS + trình độ, tích hợp đặt sân, mô hình freemium, mobile-only cho thị trường Việt Nam.

Bao gồm: đăng ký/profile, matching algorithm (Matching Score), bản đồ trực quan, đặt sân (Pessimistic Slot Locking), invite ghép đôi, đánh giá đối thủ, lịch sử trận, thanh toán (P1), ví nội bộ (P1), premium subscription (P1), hủy trận + hoàn tiền (P2), phát hiện gian lận (P2), báo cáo quản trị (P2).

Boundary: không cover mạng xã hội, giải đấu, marketplace dụng cụ, web version, offline mode.

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

Chi tiết ERD: [[docs/sport-matching/srs/erd.md|ERD Sport Matching]]

## 7. Flows (tóm tắt — chi tiết ở flows.md)

| Flow | Type | Related UC | Related FR |
|------|------|-----------|------------|
| Matching + Booking | Sequence | uc-find-opponent, uc-book-match | FR-003 đến FR-010 |
| Registration + OTP | Sequence | uc-register | FR-001, FR-002 |
| Rating + Auto-adjust | Sequence | uc-rate-opponent | FR-011, FR-014 |

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

- [ ] OQ-1: Matching Score algorithm chi tiết — tỷ trọng vị trí tính theo khoảng cách tuyến tính hay theo vùng (cluster)? Rating weight 20% khi Player mới (chưa có rating) tính thế nào?
- [ ] OQ-2: ELO auto-adjust ngưỡng cụ thể — bao nhiêu trận thắng liên tiếp / rating trung bình bao nhiêu để tăng bậc? Có giảm bậc ngược không?
