---
type: brd
feature: sport-matching
status: draft
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-04
links:
  - docs/sport-matching/urd.md
  - docs/sport-matching/brainstorms/geo-skill-matching.md
tags: [brd, sport-matching]
stale_reason: ""
changelog:
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

### 4.2 Success metrics (quantitative)

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

## 5. Scope

### 5.1 In scope

- Matching đối thủ theo vị trí GPS + trình độ (Matching Score: môn 100% hard filter, vị trí 40%, trình độ 40%, rating 20%)
- Đặt sân + giữ chỗ tạm (Pessimistic Slot Locking 5 phút)
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

- Mạng xã hội (chat, feed, đăng bài, theo dõi bạn bè)
- Tổ chức giải đấu / tournament
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
