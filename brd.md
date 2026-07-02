---
type: brd
feature: sport-matching
status: in-review
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-23
links:
  - docs/sport-matching/urd.md
  - docs/sport-matching/brainstorms/geo-skill-matching.md
  - docs/sport-matching/prd.md
  - docs/sport-matching/srs/spec.md
tags: [brd, sport-matching]
stale_reason: ""
changelog:
  - 2026-06-26 | /gap | fix G1: thêm Mục 4.3 mapping CAP-22→30 vào BO-01→05; fix G7: brainstorm links đã có (false alarm)
  - 2026-06-25 | /review | fix W2: Mục 5.2 Out of Scope align P1/P2 roadmap (chat/social/giải đấu)
  - 2026-06-23 | /brd | thêm BO-05 (booking conversion), scope đặt sân độc lập + đánh giá sân + đăng sân, metrics mới
  - 2026-06-23 | /gap | status draft→in-review, added forward links PRD/SRS
  - 2026-06-04 | /prd | cascade từ PRD OQ-1: commission chốt 12% cố định (trước đó 10-15%)
  - 2026-06-04 | /brd | resolved OQ-1,OQ-2,OQ-3,OQ-4: commission 12%, premium 49k, ma trận hoàn tiền, cost categories
  - 2026-06-04 | /brd | initial BRD draft từ URD + brainstorm geo-skill-matching
---

# Sport Matching — Business Requirements Document

> Vì sao business *làm* feature này? Ràng buộc business gì?
> KHÔNG phải: user needs (URD), spec sản phẩm (PRD/SRS).

## 1. Executive Summary

Sport Matching là ứng dụng mobile ghép đối thủ thể thao theo vị trí GPS và trình độ, kết hợp đặt sân trực tiếp. Sản phẩm hoạt động như nền tảng Giao dịch Thương mại điện tử (E-commerce Platform) với chức năng đặt chỗ, doanh thu chính từ hoa hồng (commission) trên mỗi booking sân thành công. Target thị trường Việt Nam — hiện chưa có app nào chuyên ghép đối thủ theo trình độ + vị trí. Ưu tiên cầu lông và pickleball (đang hot). Standalone product, không nằm trong hệ sinh thái lớn hơn. Timeline: MVP Go-Live + Beta tháng 6/2026, target break-even trong 12 tháng.

## 2. Business Context

### 2.1 Problem statement

Người chơi thể thao tại Việt Nam hiện phải tìm đối thủ qua các group, hội nhóm trên Facebook — không có cơ chế lọc trình độ hay vị trí, rất mất thời gian và kết quả không chính xác. Chủ sân (Partner) cũng khó tiếp cận lượng người chơi mới ngoài tệp khách quen, dẫn tới nhiều slot sân trống vào giờ thấp điểm.

### 2.2 Opportunity

- **Gap thị trường:** Chưa có ứng dụng nào tại Việt Nam chuyên matching thể thao theo vị trí + trình độ kết hợp đặt sân.
- **Xu hướng:** Cầu lông và pickleball đang bùng nổ tại VN, nhu cầu tìm đối thủ tăng mạnh.
- **Timing:** Người dùng mobile Việt Nam quen với mô hình đặt chỗ trực tuyến (Grab, ShopeeFood, Traveloka), sẵn sàng chấp nhận app booking sân.
- **E-commerce model:** Chuyển đổi từ matching thuần sang nền tảng giao dịch đặt chỗ, mở ra nguồn thu commission bền vững.

### 2.3 Strategic alignment

Standalone product — không nằm trong chiến lược hay hệ sinh thái lớn hơn. Mục tiêu: xây dựng nền tảng matching thể thao số 1 tại Việt Nam.

## 3. Stakeholders

| Stakeholder | Interest | Influence | Notes |
|-------------|----------|-----------|-------|
| Product Owner (PO) | Quyết định scope, priority, roadmap | Cao nhất | Ra quyết định cuối cùng về business direction |
| Player (Người chơi) | Tìm đối thủ nhanh, đặt sân tiện | Cao | Primary user, adoption quyết định sống còn app |
| Partner (Chủ sân) | Lấp đầy slot sân, tăng doanh thu | Cao | Supply side — thiếu Partner thì Player không có sân đặt |
| Dev Team | Xây dựng sản phẩm đúng timeline + chất lượng | Cao | Ảnh hưởng trực tiếp tới feasibility + timeline |
| Admin (Quản trị viên) | Vận hành hệ thống, xử lý gian lận | Trung bình | Operational role, không quyết định business direction |

## 4. Business Objectives

### 4.1 Primary objectives (SMART)

- **BO-sport-matching-01:** Đạt **1.000 Player active** trong 6 tháng đầu kể từ launch (tăng từ 200 player beta). Đo bằng MAU (Monthly Active Users) trên analytics dashboard.
- **BO-sport-matching-02:** Onboard **50 sân đối tác** trong 3 tháng đầu kể từ launch (tăng từ 5 sân beta, gấp 10 lần). Đo bằng số Partner có ít nhất 1 slot active trên hệ thống.
- **BO-sport-matching-03:** Đạt **tỷ lệ lấp đầy sân (slot occupancy rate) 70%** tại các khung giờ cao điểm (17h-22h ngày thường + cuối tuần) trong 6 tháng đầu. Đo bằng tỷ lệ slot booked / slot available trong peak hours.
- **BO-sport-matching-04:** Đạt **revenue break-even** (hòa vốn) trong 12 tháng kể từ launch. Đo bằng tổng revenue (commission + premium) >= tổng chi phí vận hành.
- **BO-sport-matching-05:** Đạt **booking conversion rate ≥ 20%** (từ xem sân đến đặt thành công) và **tỷ lệ chủ sân duyệt trong 30 phút ≥ 80%** trong 6 tháng đầu. Đo bằng analytics dashboard.

### 4.3 Capability → Objective mapping (P1/P2)

Các capabilities P1/P2 không tạo ra BO riêng nhưng đều phục vụ BO-01→05 hiện có:

| Capabilities | Phục vụ BO | Lý do |
|---|---|---|
| CAP-22 (Chat), CAP-23 (Notification) | BO-01 (MAU) | Tăng engagement và retention — Player có lý do quay lại app |
| CAP-24 (Profile/Settings), CAP-26 (Onboarding chủ sân) | BO-01, BO-02 | Profile hoàn chỉnh tăng trust; onboarding nhanh tăng Partner adoption |
| CAP-25 (Admin Dashboard) | BO-01, BO-03, BO-05 | Giám sát KPI, xử lý vi phạm bảo vệ chất lượng nền tảng |
| CAP-27 (Ghép đội), CAP-28 (Giải đấu) | BO-01 | Mở rộng use case → giữ chân Player lâu dài, viral growth |
| CAP-29 (Social Feed), CAP-30 (Khuyến mãi) | BO-01, BO-03, BO-05 | Community tăng organic retention; voucher/referral tăng booking conversion |

### 4.4 Success metrics (quantitative)

| Metric | Target | Window | Đo bằng |
|--------|--------|--------|---------|
| MAU (Monthly Active Users) | 1.000 | 6 tháng post-launch | Analytics dashboard |
| Partner active | 50 sân | 3 tháng post-launch | Số Partner có slot active |
| Slot occupancy rate (peak hours) | ≥ 70% | 6 tháng post-launch | Booked / Available trong 17h-22h + weekend |
| Matching rate | ≥ 70% | Ongoing | Yêu cầu tìm đối thủ có kết quả / tổng yêu cầu |
| Invite accept rate | ≥ 50% | Ongoing | Invite accepted / invite sent |
| Player retention (tuần đầu) | ≥ 40% | Ongoing | Player chơi trận thứ 2 / tổng Player |
| App rating | ≥ 4.0/5 | Ongoing | Store rating |
| Revenue break-even | Tổng revenue ≥ tổng cost | 12 tháng post-launch | P&L report |
| Booking conversion (đặt sân) | ≥ 20% | Ongoing | Bookings / venue page views |
| Chủ sân duyệt trong 30p | ≥ 80% | Ongoing | Approved within 30m / total bookings |
| Tỷ lệ hủy booking | < 15% | Ongoing | Cancelled / total confirmed |
| Đánh giá sân trung bình | ≥ 3.5/5 | Ongoing | Average venue rating |

## 5. Scope

### 5.1 In scope

- Matching đối thủ theo vị trí GPS + trình độ (Matching Score: môn 100% hard filter, vị trí 40%, trình độ 40%, rating 20%)
- Đặt sân qua matching flow + giữ chỗ tạm (Pessimistic Slot Locking 5 phút)
- **Tìm & đặt sân độc lập** (không cần ghép đối thủ): tìm theo môn/khu vực/ngày/giá, thanh toán hoặc giữ chỗ 30 phút, chủ sân duyệt 30 phút, chính sách hoàn tiền 3 mức, đổi giờ/sân 1 lần
- **Đánh giá sân** 5 sao + review + điểm thưởng tích lũy
- **Chủ sân đăng sân** (admin duyệt), block khung giờ, quản lý booking real-time
- Đánh giá đối thủ sau trận + auto-adjust trình độ (ELO-based)
- Mô hình freemium: free 10 invite/ngày/môn, Premium unlimited
- Commission 12% trên booking sân (nguồn thu chính)
- Premium subscription 49.000 VND/tháng (unlimited invite)
- Ví điện tử nội bộ (In-app Wallet): số dư, nạp/rút, hoàn tiền dạng điểm thưởng (giảm refund fee qua ngân hàng)
- Ma trận Nghiệp vụ Hủy lịch & Hoàn tiền:
  - Hủy trước 24h: hoàn 100% Player, chủ sân 0%
  - Hủy 6-24h trước: hoàn 50% Player, đền bù 40% chủ sân
  - Hủy dưới 6h / no-show: không hoàn Player, đền bù 90% chủ sân
  - Hoàn tiền qua Ví nội bộ (không qua ngân hàng)
- Thanh toán qua MoMo / VNPay
- Push notification qua FCM
- 4 roles: Player, Partner, Staff, Admin (chung 1 app)
- Multi-sport, ưu tiên cầu lông + pickleball

### 5.2 Out of scope

- Mạng xã hội (chat, feed, đăng bài, theo dõi bạn bè) — *v1.0 scope; Chat P1 roadmap (CAP-22), Social Feed P2 roadmap (CAP-29)*
- Tổ chức giải đấu / tournament — *v1.0 scope; Giải đấu + ghép đội P2 roadmap (CAP-27, CAP-28)*
- Bán dụng cụ thể thao (marketplace)
- Phiên bản web
- Hỗ trợ offline
- Đa ngôn ngữ (chỉ tiếng Việt giai đoạn hiện tại)

### 5.3 Constraints (budget, timeline, regulatory)

- **Timeline:** MVP + Launch trong 6 tháng (T1-T6/2026).
- **Budget:** TBD — cần ước tính chi phí dev, server, API (Google Maps, FCM), marketing.
- **Platform:** Mobile only (Android + iOS TestFlight).
- **Regulatory:** Tuân thủ quy định thanh toán điện tử VN khi tích hợp MoMo/VNPay. Xử lý dữ liệu vị trí GPS theo privacy policy.

## 6. Cost-Benefit

### 6.1 Estimated cost

| Hạng mục | Ước tính | Notes |
|----------|----------|-------|
| Dev team (6 tháng) | TBD | Số người, mức lương/rate |
| Server + infrastructure | TBD | Cloud hosting, DB, vận hành |
| Google Maps API / Mapbox | TBD | Matching + định vị, phụ thuộc số request/tháng |
| MoMo/VNPay integration | TBD | Phí tích hợp + transaction fee per booking |
| FCM (Push notification) | Free tier | Google FCM miễn phí |
| Marketing (launch) | TBD | Seed user, onboard Partner |

**Tối ưu chi phí:** Xác thực đối tác thủ công (Manual KYC) thay vì tích hợp hệ thống tự động ở giai đoạn đầu, tiết kiệm ước tính 2 tuần phát triển.

### 6.2 Expected benefit

- **Commission revenue:** Hoa hồng **12%** trên mỗi booking sân thành công. Với target 1.000 Player active + 50 sân, ước tính hàng nghìn booking/tháng tạo nguồn thu chính.
- **Premium subscription:** **49.000 VND/tháng** unlock unlimited invite. Với 10% conversion rate (100/1.000 player) = ~4,9 triệu VND recurring revenue/tháng.
- **In-app Wallet:** Hoàn tiền dạng điểm thưởng giảm chi phí refund qua ngân hàng (Refund transactional fee), giữ tiền trong hệ thống lâu hơn.
- **Partner value:** Tăng slot occupancy cho chủ sân, tạo giá trị 2 phía (Player tìm sân, Partner lấp slot).

### 6.3 ROI / payback

- Target break-even trong **12 tháng** kể từ launch.
- ROI chính xác phụ thuộc chi phí ước tính (TBD). Revenue sources đã confirm: commission 12% + Premium 49k/tháng + In-app Wallet retention.

## 7. Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **Adoption chicken-and-egg:** Player ít dẫn tới matching kém, Partner ít sân, vòng xoáy tiêu cực | High | High | Tập trung launch theo khu vực (thành phố cụ thể), seed user qua CLB thể thao, free hoàn toàn giai đoạn beta |
| **Vendor dependency:** Google Maps API tăng phí hoặc MoMo/VNPay thay đổi policy | Medium | High | Abstraction layer cho map + payment, backup Mapbox + cổng thay thế |
| **Partner onboard:** Chủ sân không muốn lên nền tảng hoặc data slot không chính xác | High | High | Staff role hỗ trợ onboard, kiểm tra data định kỳ, Player report sân sai |
| **Refund/dispute:** Hủy trận gây tranh chấp tài chính giữa Player-Partner | Medium | Medium | Ma trận Nghiệp vụ Hủy lịch & Hoàn tiền rõ ràng (đền bù chủ sân 40%/90%), In-app Wallet giảm refund cost |
| **Competition:** Đối thủ copy model hoặc app lớn thêm feature matching | Low | High | First-mover advantage, xây community loyalty, tích lũy data matching (network effect) |

## 8. Timeline (high-level milestones)

| Giai đoạn | Thời gian | Phương pháp | Nội dung chính |
|-----------|-----------|-------------|----------------|
| Giai đoạn 1: Requirements | Tháng 1-2 | Waterfall | Hoàn thiện yêu cầu, đóng băng phạm vi MVP |
| Giai đoạn 2-4: Development | Tháng 3-5 | Agile/Scrum | Phát triển tính năng lõi: Auth, Payment, Matching Algorithm, BI Dashboard |
| MVP Go-Live (UAT) | Tháng 6 | — | Hoàn tất UAT, phát hành lên Android + iOS TestFlight |
| Beta Test | Tháng 6 (Sprint 12) | — | Thử nghiệm thực tế với 5 chủ sân + 200 người chơi |
| Launch chính thức | Tháng 6 (cuối) | — | Sau hoàn tất Beta Test, đóng dự án, phát hành công khai |

## 9. Open Questions

- [x] OQ-1: Commission — Resolved: 12% trên mỗi booking sân thành công.
- [x] OQ-2: Premium pricing — Resolved: 49.000 VND/tháng.
- [x] OQ-3: Ma trận Hủy lịch & Hoàn tiền — Resolved: Hủy trước 24h hoàn 100%; 6-24h hoàn 50% Player + đền bù 40% chủ sân; dưới 6h không hoàn + đền bù 90% chủ sân. Hoàn tiền qua Ví nội bộ (không qua ngân hàng).
- [x] OQ-4: Chi phí ước tính — Resolved: Giá trị TBD, categories xác định: API (Maps/Payment), vận hành (DB/Server/FCM), tối ưu Manual KYC tiết kiệm 2 tuần dev.
