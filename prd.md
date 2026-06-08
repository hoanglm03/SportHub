---
type: prd
feature: sport-matching
status: draft
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-04
links:
  - docs/sport-matching/urd.md
  - docs/sport-matching/brd.md
  - docs/sport-matching/brainstorms/geo-skill-matching.md
tags: [prd, sport-matching]
stale_reason: ""
changelog:
  - 2026-06-07 | /gap | added CAP-sport-matching-16 Report kết quả trận (gap fix: FR-021 orphan)
  - 2026-06-04 | /prd | resolved OQ-1,OQ-2,OQ-3: commission 12% cố định, chỉ 1v1, thanh toán tại sân v1.0
  - 2026-06-04 | /prd | initial PRD draft từ URD + BRD + brainstorm geo-skill-matching
---

# Sport Matching — Product Requirements Document

> Sản phẩm sẽ *làm gì* cho feature này? Scope cụ thể.
> KHÔNG phải: kỹ thuật (SRS), business case (BRD).

## 1. Product Overview

**Sport Matching** là app mobile giúp người chơi thể thao tìm đối thủ ngang trình độ gần mình và đặt sân ngay trong 3 phút.

Sản phẩm hoạt động như nền tảng giao dịch đặt chỗ (E-commerce Platform) kết hợp matching thể thao. Player mở app, hệ thống dùng GPS xác định vị trí, hiện bản đồ đối thủ gần kèm trình độ (Matching Score = vị trí 40% + trình độ 40% + rating 20%, môn hard filter). Player chọn đối thủ, chọn sân + slot giờ, gửi invite. Đối thủ confirm trong 5 phút, trận đấu được tạo.

**Key differentiation:** App duy nhất tại Việt Nam chuyên matching thể thao theo trình độ + vị trí + đặt sân tích hợp. UI search-centric với bản đồ trực quan, tối giản thao tác (minimize clicks). Mô hình freemium với commission 12% trên booking.

**Target market:** Người chơi thể thao Việt Nam, 25-40 tuổi, thành phố lớn (TP.HCM, Hà Nội, Đà Nẵng). Ưu tiên cầu lông và pickleball (đang hot), mở rộng multi-sport.

## 2. Goals

### 2.1 Goals

1. **Matching hiệu quả:** ≥ 70% yêu cầu tìm đối thủ có kết quả trong bán kính 10km, thời gian từ mở app đến confirm trận < 3 phút.
2. **Tăng trưởng user base:** 1.000 Player active (MAU) trong 6 tháng, 50 sân đối tác trong 3 tháng post-launch.
3. **Lấp đầy sân:** Slot occupancy rate ≥ 70% tại peak hours (17h-22h + cuối tuần).
4. **Bền vững tài chính:** Revenue break-even trong 12 tháng từ commission 12% + Premium 49k/tháng.

### 2.2 Non-goals

- **Không tự vận hành sân:** App chỉ là platform kết nối Player-Partner, không sở hữu hay quản lý sân thể thao.
- **Không tự xây hệ thống thanh toán riêng:** Tích hợp MoMo/VNPay làm cổng thanh toán, không phát triển payment gateway nội bộ.
- **Không hỗ trợ team sport:** v1.0 chỉ 1v1. 2v2+ và quản lý đội bóng/giải đấu để future.
- **Không phải mạng xã hội:** Không chat, feed, đăng bài, theo dõi bạn bè.
- **Không hỗ trợ offline / web / đa ngôn ngữ** giai đoạn hiện tại.

## 3. Personas (kế thừa URD)

| Persona | Description | Key needs |
|---------|-------------|-----------|
| **Player** (primary) | Người chơi thể thao 25-40 tuổi, đi làm, thu nhập ổn định, thành thạo mobile, chơi thường xuyên vào peak hours (17h-22h + cuối tuần) | Tìm đối thủ ngang trình gần mình nhanh, đặt sân không gọi điện, xem rating/trình độ trước khi chơi, theo dõi thống kê win/loss |
| **Partner** (secondary) | Chủ sở hữu/quản lý cơ sở thể thao | Lấp đầy slot sân, tiếp cận player mới, quản lý booking dễ dàng |
| **Staff** (secondary) | Nhân viên vận hành của Partner | Xem/xác nhận đặt chỗ nhanh, tránh trùng lịch |
| **Admin** (secondary) | Quản trị viên hệ thống | Giám sát hệ thống, xử lý gian lận, moderate đánh giá |

## 4. Capabilities (P0 / P1 / P2)

### 4.1 P0 — must have (v1.0 Launch)

| ID | Capability | Mô tả |
|---|---|---|
| CAP-sport-matching-01 | Đăng ký + Setup profile | Email + mật khẩu + tên hiển thị + OTP email. Chọn ≥1 môn (tối đa 5 ưu tiên), tự đánh giá trình độ 3 bậc (Mới chơi / Trung bình / Nâng cao) per môn |
| CAP-sport-matching-02 | Matching đối thủ | GPS tự động, quét đối thủ theo Matching Score (môn 100% hard filter + vị trí 40% + trình độ 40% + rating 20%). Bán kính mặc định 3km, tối đa 50km |
| CAP-sport-matching-03 | Bản đồ trực quan | Search-centric + Map Integration. Hiện đối thủ/sân gần trên bản đồ, filter theo môn/trình độ/khoảng cách |
| CAP-sport-matching-04 | Đặt sân | Chọn sân + slot giờ. Pessimistic Slot Locking 5 phút. Gợi ý sân/giờ khác nếu hết slot. v1.0 thanh toán tại sân (cash), app chỉ giữ chỗ |
| CAP-sport-matching-05 | Invite ghép đôi | Gửi invite, đối thủ nhận push notification (FCM). Timeout 5 phút, auto rotate đối thủ tiếp. First-come-first-served cho concurrent. Limit: 10 invite/ngày/môn (free), 1 match pending tối đa |
| CAP-sport-matching-06 | Đánh giá đối thủ | Rating + nhận xét sau trận. Nhắc nhở đánh giá qua notification. Rating trung bình hiển thị trên profile |
| CAP-sport-matching-07 | Lịch sử trận + Thống kê | Danh sách trận (sân, giờ, đối thủ) + thống kê win/loss + rating nhận từ đối thủ. Theo dõi tiến bộ |
| CAP-sport-matching-16 | Report kết quả trận | Cả 2 Player tự report Thắng/Thua/Hòa sau trận. Report khớp → ghi nhận. Conflict → Admin review. Dùng cho thống kê win/loss |

### 4.2 P1 — soon after (v1.1)

| ID | Capability | Mô tả |
|---|---|---|
| CAP-sport-matching-08 | Thanh toán online | Tích hợp MoMo + VNPay. Commission cố định 12% trên tổng giá trị đặt chỗ. Thay thế thanh toán tại sân (v1.0) |
| CAP-sport-matching-09 | Auto-adjust trình độ | ELO-based: liên tục thắng/rating cao từ cùng bậc dẫn tới tự tăng bậc. Phát hiện fake trình độ |
| CAP-sport-matching-10 | Partner đăng ký sân | Tên, địa chỉ, tọa độ, slot giờ, giá, môn hỗ trợ. Manual KYC qua Zalo |
| CAP-sport-matching-11 | Ví điện tử nội bộ | In-app Wallet: số dư, nạp/rút, hoàn tiền dạng điểm thưởng. Giảm refund fee qua ngân hàng |
| CAP-sport-matching-12 | Premium subscription | 49.000 VND/tháng, unlock unlimited invite/ngày. Gợi ý upgrade khi đạt limit free |

### 4.3 P2 — future

| ID | Capability | Mô tả |
|---|---|---|
| CAP-sport-matching-13 | Hủy trận + Ma trận Hoàn tiền | Hủy tối đa 3/tháng, cooldown 15 phút. Ma trận: >24h hoàn 100%, 6-24h hoàn 50% + đền bù sân 40%, <6h không hoàn + đền bù 90% |
| CAP-sport-matching-14 | Phát hiện đánh giá ác ý | Thuật toán phát hiện mẫu bất thường (luôn rate 1 sao). Admin moderate + loại bỏ |
| CAP-sport-matching-15 | Báo cáo quản trị | Admin dashboard: số user, trận, revenue, analytics. Aggregated data cho báo cáo |

> P0/P1/P2 là **capability/scope decisions** trong feature này, KHÔNG phải feature breakdown.

## 5. Key User Flows

### Flow 1: Player tìm đối thủ + đặt sân (luồng chính)

1. Player mở app, bản đồ hiện vị trí GPS
2. Chọn môn thể thao + điều chỉnh filter (bán kính, trình độ)
3. Xem danh sách đối thủ trên bản đồ (kèm trình độ, rating)
4. Chọn đối thủ + chọn sân + slot giờ
5. System lock slot 5 phút + gửi invite
6. Đối thủ confirm trong 5 phút
7. Match xác nhận, cả 2 nhận notification (đối thủ + sân + giờ)
8. Nhắc nhở trước trận 1 giờ

### Flow 2: Player đăng ký + setup profile

1. Nhập email + mật khẩu + tên hiển thị
2. Verify OTP qua email
3. Chọn ≥1 môn + tự đánh giá trình độ per môn
4. Profile sẵn sàng, hiện bản đồ chính

### Flow 3: Player đánh giá sau trận

1. Nhận nhắc nhở đánh giá sau trận
2. Chấm rating + nhận xét (optional)
3. System cập nhật rating trung bình đối thủ
4. Auto-adjust Matching Score nếu rating khác trình độ khai báo (P1)

## 6. Release Plan

| Release | Capabilities | Target Date | Status |
|---------|--------------|-------------|--------|
| v1.0 (MVP Launch) | CAP-01 đến CAP-07 (Đăng ký, Matching, Bản đồ, Đặt sân, Invite, Đánh giá, Lịch sử) | Tháng 6/2026 | planned |
| v1.1 | CAP-08 đến CAP-12 (Thanh toán, Auto-adjust, Partner đăng ký, Ví nội bộ, Premium) | Tháng 8-9/2026 | planned |
| v2.0 | CAP-13 đến CAP-15 (Hủy trận + Hoàn tiền, Phát hiện ác ý, Báo cáo) | TBD | planned |

**Milestones chi tiết (từ BRD):**

| Milestone | Thời gian | Nội dung |
|-----------|-----------|----------|
| Requirements freeze | Tháng 1-2 | Waterfall: hoàn thiện yêu cầu, đóng băng scope MVP |
| Development | Tháng 3-5 | Agile/Scrum: Auth, Payment, Matching Algorithm, BI Dashboard |
| MVP Go-Live (UAT) | Tháng 6 | Hoàn tất UAT, phát hành Android + iOS TestFlight |
| Beta Test | Tháng 6 (Sprint 12) | 5 chủ sân + 200 người chơi |
| Launch chính thức | Tháng 6 (cuối) | Phát hành công khai sau Beta |

## 7. Success Metrics

| Metric | Target | Window | Source |
|--------|--------|--------|--------|
| MAU (Monthly Active Users) | 1.000 | 6 tháng post-launch | BRD BO-01 |
| Partner active | 50 sân | 3 tháng post-launch | BRD BO-02 |
| Slot occupancy (peak hours) | ≥ 70% | 6 tháng post-launch | BRD BO-03 |
| Revenue break-even | Revenue ≥ Cost | 12 tháng post-launch | BRD BO-04 |
| Matching rate | ≥ 70% | Ongoing | URD SC |
| Time to match | < 3 phút | Ongoing | URD SC |
| Invite accept rate | ≥ 50% | Ongoing | BRD |
| Player retention (tuần đầu) | ≥ 40% | Ongoing | URD SC |
| App rating | ≥ 4.0/5 | Ongoing | URD SC |

## 8. Dependencies

### 8.1 Internal teams

| Team / Role | Phụ thuộc | Impact |
|-------------|-----------|--------|
| Product Owner (PO) | Xác lập mục tiêu chiến lược, phân rã Backlog, ký duyệt cuối cùng | Chặn nếu PO không available cho sign-off |
| Tech Lead | Thiết kế ERD (Conceptual/Logical), xử lý sự cố nghiệp vụ, ước tính chi phí | Chặn nếu chưa có ERD cho dev |
| Dev team (BE/FE) | API Master Data, giao diện cốt lõi. Cần điều phối nguồn lực (FE hỗ trợ mockup) | Timeline risk nếu thiếu resource |
| UI/UX | Thiết kế giao diện từ Wireframe + Style Guide. Output: Figma (cần BA/PO approval) | Chặn FE dev nếu Figma chưa xong |
| Tester | Xây dựng test cases từ User Stories + Exception Handling. Thực hiện UAT | Chặn launch nếu UAT chưa pass |

### 8.2 External tools / vendors

| Tool / Vendor | Mục đích | Giai đoạn |
|---------------|----------|-----------|
| Google Maps API / Mapbox | Matching + định vị, quét bán kính | v1.0 |
| MoMo + VNPay | Cổng thanh toán | v1.1 |
| Firebase (FCM + Analytics) | Push notification + product analytics (Beta) | v1.0 |
| Zalo | Q&A + Manual KYC xác thực đối tác | v1.1 |
| Jira / Trello | Quản lý Product Backlog | Toàn dự án |
| Figma | Thiết kế UI, BA/PO approval | Toàn dự án |
| SMS service / vendor | Tối ưu luồng OTP SMS (giai đoạn sau email OTP) | v1.1+ |

### 8.3 Approval gates

| Sign-off | Thời điểm | Người phê duyệt |
|----------|-----------|------------------|
| BRD Sign-off Draft | Tháng 1 | PO |
| Scope Sign-off (đóng băng MVP) | Tháng 2 | PO + BA |
| User Journey Sign-off | Tháng 2 | PO + BA |
| User Story + Figma Approval | Trước mỗi Sprint | BA (Impact Analysis) + PO (Final approval) — Single Source of Truth |
| UAT Sign-off Report | Tháng 6 | PO + Tester |
| Project Closure Report | Tháng 6 (cuối) | PO |

## 9. Product Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **Adoption chicken-and-egg:** Player ít dẫn tới matching kém, Partner ít sân | High | High | Launch theo khu vực, seed user qua CLB, free giai đoạn beta |
| **Vendor dependency:** Google Maps/MoMo/VNPay thay đổi phí/policy | Medium | High | Abstraction layer, backup Mapbox + cổng thay thế |
| **Partner onboard:** Chủ sân không muốn lên nền tảng, data slot sai | High | High | Staff hỗ trợ, Manual KYC qua Zalo, Player report |
| **Refund/dispute:** Tranh chấp tài chính hủy trận | Medium | Medium | Ma trận Hoàn tiền rõ ràng, In-app Wallet giảm refund cost |
| **Resource/timeline:** 6 tháng tight cho MVP, FE cần hỗ trợ mockup | Medium | High | Agile sprint planning, PO priority ruthless, scope freeze sớm |
| **Competition:** App lớn thêm feature matching | Low | High | First-mover advantage, network effect, community loyalty |

## 10. Open Questions

- [x] OQ-1: Commission — Resolved: cố định 12% trên tổng giá trị đặt chỗ. Không thang bậc.
- [x] OQ-2: Match format — Resolved: v1.0 chỉ hỗ trợ 1v1. 2v2+ để future.
- [x] OQ-3: Thanh toán v1.0 — Resolved: thanh toán tại sân (cash). App chỉ giữ chỗ, không thu tiền online. Thanh toán online là P1 (v1.1).
