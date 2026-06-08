# SportHub

Ứng dụng mobile giúp người chơi thể thao tìm đối thủ ngang trình độ gần mình và đặt sân ngay trong 3 phút.

## Về dự án

SportHub là nền tảng matching thể thao kết hợp đặt sân, nhắm thị trường Việt Nam. Giải quyết pain point: người chơi phải tìm đối thủ qua group Facebook, không lọc được trình độ hay vị trí, rất mất thời gian.

**Target:** Mobile app (Android/iOS) | **Thị trường:** Việt Nam | **Môn ưu tiên:** Cầu lông, Pickleball

## Tài liệu

| Folder | Nội dung | Bắt đầu đọc |
|--------|----------|-------------|
| `brainstorms/` | Ý tưởng gốc, deep interview 13 sections | Đọc đầu tiên để hiểu context |
| `urd.md` | User Requirements — personas, user needs, journeys | Hiểu user cần gì |
| `brd.md` | Business Requirements — objectives, revenue, timeline | Hiểu business case |
| `prd.md` | Product Requirements — capabilities P0/P1/P2, release plan | Hiểu scope sản phẩm |
| `srs/` | Software Requirements — FR, NFR, BR, errors, ERD, flows, states | Đặc tả kỹ thuật chi tiết |
| `usecases/` | 6 use cases — prose 8 sections per UC | Luồng nghiệp vụ end-to-end |
| `ascii-screen/` | 13 màn hình — ASCII wireframe + description table | Giao diện người dùng |
| `userstories/` | 16 user stories + 66 acceptance criteria (Given/When/Then) | Backlog cho dev team |
| `traceability.md` | Ma trận truy xuất BO → CAP → FR → US → AC → UC → Screen | Kiểm tra coverage |

## Đọc theo thứ tự

```
brainstorms/geo-skill-matching.md   ← Ý tưởng + deep dive
         ↓
      urd.md                        ← Góc user
         ↓
      brd.md                        ← Góc business
         ↓
      prd.md                        ← Scope sản phẩm
         ↓
   srs/spec.md                      ← Đặc tả kỹ thuật (21 FR, 13 BR, 9 errors)
   srs/erd.md                       ← Data model (12 entities)
   srs/flows.md                     ← 3 sequence diagrams
   srs/states.md                    ← State machines (Match, Slot, Invite)
         ↓
   usecases/_index.md               ← 6 use cases overview
         ↓
   ascii-screen/_index.md           ← 13 screens overview
         ↓
   userstories/_index.md            ← 16 stories + 66 ACs (sprint backlog)
         ↓
   traceability.md                  ← Coverage check (97%)
```

## Key Numbers

| Metric | Value |
|--------|-------|
| Tổng files | 47 |
| Functional Requirements | 21 (13 P0, 5 P1, 3 P2) |
| Non-Functional Requirements | 7 |
| Business Rules | 13 |
| Error Codes | 9 (exact wording tiếng Việt) |
| Data Entities | 12 (ERD Mermaid) |
| Sequence Diagrams | 3 |
| State Machines | 3 (Match, Slot, Invite) |
| Use Cases | 6 |
| Screens (ASCII wireframe) | 13 |
| User Stories | 16 (8 P0, 5 P1, 3 P2) |
| Acceptance Criteria | 66 (Given/When/Then) |
| Traceability Coverage | 97% |
| Review Rounds | 2 (6 agents round 1, senior-ba round 2) |

## Feature Highlights

- **Matching Algorithm:** Matching Score = Môn (100% hard filter) + Vị trí (40%) + Trình độ (40%) + Rating (20%)
- **Đặt sân:** Pessimistic Slot Locking 5 phút, auto release
- **Invite:** Timeout 5 phút, auto-rotate đối thủ, first-come-first-served
- **Trình độ:** 3 bậc (Mới chơi / Trung bình / Nâng cao), ELO auto-adjust
- **Revenue:** Commission 12% + Premium 49k/tháng + In-app Wallet
- **Hoàn tiền:** Ma trận 3 bậc (>24h: 100%, 6-24h: 50%, <6h: 0%)

## Release Plan

| Release | Nội dung | Target |
|---------|----------|--------|
| v1.0 (MVP) | Đăng ký, Matching, Đặt sân, Invite, Đánh giá, Lịch sử, Report kết quả | Tháng 6/2026 |
| v1.1 | Thanh toán MoMo/VNPay, Auto-adjust ELO, Partner đăng ký, Wallet, Premium | Tháng 8-9/2026 |
| v2.0 | Hủy trận + Hoàn tiền, Phát hiện gian lận, Báo cáo quản trị | TBD |

## Stakeholders

| Role | Ảnh hưởng |
|------|-----------|
| Product Owner | Cao nhất — quyết định scope, priority, roadmap |
| Player (Người chơi) | Cao — primary user, adoption quyết định sống còn |
| Partner (Chủ sân) | Cao — supply side, thiếu Partner thì không có sân |
| Dev Team | Cao — feasibility + timeline |
| Admin | Trung bình — operational |

## Tools & Dependencies

- **Map:** Google Maps API / Mapbox
- **Payment (P1):** MoMo + VNPay
- **Push Notification:** Firebase Cloud Messaging (FCM)
- **OTP:** Email (chính), SMS (giai đoạn sau)
- **KYC Partner:** Manual qua Zalo
- **Analytics:** Google Analytics / Firebase
- **Design:** Figma (BA/PO approval)
- **Project Management:** Jira / Trello

---

> Tài liệu BA được tạo bằng [BA-Kit](https://github.com/anthropics/claude-code) pipeline: `/brainstorm` → `/urd` → `/brd` → `/prd` → `/srs` → `/userstory` → `/ac` → `/review` → `/gap`
