---
type: userstory-index
feature: sport-matching
status: draft
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-04
links:
  - docs/sport-matching/srs/spec.md
  - docs/sport-matching/usecases/_index.md
tags: [userstory-index]
stale_reason: ""
changelog:
  - 2026-06-26 | /gap | fix US-010 screen ref → venue-register, venue-manage; resolve OQ-1
  - '2026-06-25 | /review | fix W3: US-035 note 3-persona; fix W4: US-037 note scope rộng; fix S1: US-009 persona note; fix S2: US-014/015 screens TBD'
  - 2026-06-25 | /userstory | [us-034→037] 4 P2 stories (ghép đội, giải đấu, social feed, voucher+referral) + AC inline
  - '2026-06-23 | /review | fix UC/US round 2: US-020 AC renumber, US-018/024 exact error msg, US-021 +E-024/025+BR-018, US-016 AC split, US-022/029 boundary ACs, US-018/030 auth AC (BR-025)'
  - '2026-06-23 | /review | fix review findings: split US-030→030+032+033, added AC-008 concurrent lock US-004, AC-007 US-017, AC-005 US-019/US-006, fix error refs US-018, US-016 deadline 24h'
  - 2026-06-23 | /userstory | [us-025→031] 7 P1 stories (chat, noti, profile, privacy, wallet, admin, onboarding) + AC inline
  - 2026-06-23 | /userstory | [us-017→024] 8 venue-booking stories + AC inline
  - 2026-06-07 | /ac | [us-016] generated 5 ACs (3 happy, 1 error, 1 ui-state)
  - 2026-06-07 | /userstory | [us-016] created from FR-sport-matching-021 (post-review)
  - 2026-06-04 | /ac | [us-001] generated 5 ACs (2 happy, 2 error, 1 validation)
  - 2026-06-04 | /ac | [us-002] generated 4 ACs (1 happy, 3 validation)
  - 2026-06-04 | /ac | [us-003] generated 6 ACs (3 happy, 3 error)
  - 2026-06-04 | /ac | [us-004] generated 7 ACs (3 happy, 3 error, 1 validation)
  - 2026-06-04 | /ac | [us-005] generated 5 ACs (3 happy, 2 error)
  - 2026-06-04 | /ac | [us-006] generated 4 ACs (4 happy)
  - 2026-06-04 | /ac | [us-007] generated 4 ACs (3 happy, 1 ui-state)
  - 2026-06-04 | /ac | [us-008] generated 3 ACs (2 happy, 1 error)
  - 2026-06-04 | /ac | [us-009] generated 3 ACs (2 happy, 1 ui-state)
  - 2026-06-04 | /ac | [us-010] generated 3 ACs (1 happy, 1 error, 1 validation)
  - 2026-06-04 | /ac | [us-011] generated 3 ACs (3 happy)
  - 2026-06-04 | /ac | [us-012] generated 3 ACs (2 happy, 1 error)
  - 2026-06-04 | /ac | [us-013] generated 5 ACs (3 happy, 2 error)
  - 2026-06-04 | /ac | [us-014] generated 3 ACs (3 happy)
  - 2026-06-04 | /ac | [us-015] generated 3 ACs (3 happy)
  - 2026-06-04 | /userstory | [us-015] created from FR-sport-matching-020
  - 2026-06-04 | /userstory | [us-014] created from FR-sport-matching-019
  - 2026-06-04 | /userstory | [us-013] created from FR-sport-matching-018
  - 2026-06-04 | /userstory | [us-012] created from FR-sport-matching-017
  - 2026-06-04 | /userstory | [us-011] created from FR-sport-matching-016
  - 2026-06-04 | /userstory | [us-010] created from FR-sport-matching-015
  - 2026-06-04 | /userstory | [us-009] created from FR-sport-matching-014
  - 2026-06-04 | /userstory | [us-008] created from FR-sport-matching-013
  - 2026-06-04 | /userstory | [us-007] created from FR-sport-matching-012
  - 2026-06-04 | /userstory | [us-006] created from FR-sport-matching-011
  - 2026-06-04 | /userstory | [us-005] created from FR-sport-matching-009,010
  - 2026-06-04 | /userstory | [us-004] created from FR-sport-matching-006,007,008
  - 2026-06-04 | /userstory | [us-003] created from FR-sport-matching-003,004,005
  - 2026-06-04 | /userstory | [us-002] created from FR-sport-matching-002
  - 2026-06-04 | /userstory | [us-001] created from FR-sport-matching-001
  - 2026-06-04 | /userstory | initial user stories index scaffolded (15 stories)
---

# Sport Matching — User Stories Index

> Master index cho mọi user stories trong feature. Mỗi US có file riêng (zero frontmatter, prose sections). Metadata + status + priority + jira key + changelog tập trung ở file này.

## User Stories

| # | ID | Title | Persona | Covers FR | Screens | Priority | Status | Jira | Updated |
|---|----|-------|---------|-----------|---------|----------|--------|------|---------|
| 1 | [US-001](us-001.md) | Đăng ký tài khoản | Player | FR-sport-matching-001 | register, otp-verify | P0 | draft | — | 2026-06-04 |
| 2 | [US-002](us-002.md) | Setup profile thể thao | Player | FR-sport-matching-002 | profile-setup | P0 | draft | — | 2026-06-04 |
| 3 | [US-003](us-003.md) | Tìm đối thủ trên bản đồ | Player | FR-sport-matching-003,004,005 | map-search, opponent-profile | P0 | draft | — | 2026-06-04 |
| 4 | [US-004](us-004.md) | Đặt sân + gửi invite | Player | FR-sport-matching-006,007,008 | court-select, invite-confirm | P0 | draft | — | 2026-06-04 |
| 5 | [US-005](us-005.md) | Nhận invite + xác nhận trận | Player (Opponent) | FR-sport-matching-009,010 | invite-receive, match-confirmed | P0 | draft | — | 2026-06-04 |
| 6 | [US-006](us-006.md) | Đánh giá đối thủ | Player | FR-sport-matching-011 | rate-opponent | P0 | draft | — | 2026-06-04 |
| 7 | [US-007](us-007.md) | Xem lịch sử trận + thống kê | Player | FR-sport-matching-012 | match-history | P0 | draft | — | 2026-06-04 |
| 8 | [US-008](us-008.md) | Thanh toán online | Player | FR-sport-matching-013 | (P1 screens) | P1 | draft | — | 2026-06-04 |
| 9 | [US-009](us-009.md) | Auto-adjust trình độ | System (auto-trigger sau trận) | FR-sport-matching-014 | — | P1 | draft | — | 2026-06-04 |
| 10 | [US-010](us-010.md) | Partner đăng ký sân | Partner | FR-sport-matching-015 | venue-register, venue-manage | P1 | draft | — | 2026-06-26 |
| 11 | [US-011](us-011.md) | Ví điện tử nội bộ | Player | FR-sport-matching-016 | (P1 screens) | P1 | draft | — | 2026-06-04 |
| 12 | [US-012](us-012.md) | Premium subscription | Player | FR-sport-matching-017 | (P1 screens) | P1 | draft | — | 2026-06-04 |
| 13 | [US-013](us-013.md) | Hủy trận + hoàn tiền | Player | FR-sport-matching-018 | match-confirmed | P2 | draft | — | 2026-06-04 |
| 14 | [US-014](us-014.md) | Phát hiện đánh giá ác ý | Admin | FR-sport-matching-019 | admin-dashboard (TBD P2 sprint) | P2 | draft | — | 2026-06-04 |
| 15 | [US-015](us-015.md) | Báo cáo quản trị | Admin | FR-sport-matching-020 | admin-dashboard (TBD P2 sprint) | P2 | draft | — | 2026-06-04 |
| 16 | [US-016](us-016.md) | Report kết quả trận | Player | FR-sport-matching-021,012 | rate-opponent | P0 | draft | — | 2026-06-07 |
| 17 | [US-017](us-017.md) | Tìm sân thể thao | Player | FR-sport-matching-022,023 | venue-search, venue-detail | P0 | draft | — | 2026-06-23 |
| 18 | [US-018](us-018.md) | Đặt sân thanh toán ngay | Player | FR-sport-matching-024,026 | venue-detail, booking-confirm, booking-detail, venue-manage | P0 | draft | — | 2026-06-23 |
| 19 | [US-019](us-019.md) | Đặt sân giữ chỗ trước | Player | FR-sport-matching-025 | booking-confirm, booking-detail | P0 | draft | — | 2026-06-23 |
| 20 | [US-020](us-020.md) | Hủy booking sân | Player | FR-sport-matching-027 | booking-detail | P0 | draft | — | 2026-06-23 |
| 21 | [US-021](us-021.md) | Đổi giờ/sân booking | Player | FR-sport-matching-028 | booking-detail, venue-detail | P1 | draft | — | 2026-06-23 |
| 22 | [US-022](us-022.md) | Đánh giá sân | Player | FR-sport-matching-029 | venue-rate, booking-detail | P1 | draft | — | 2026-06-23 |
| 23 | [US-023](us-023.md) | Chủ sân đăng sân mới | Partner | FR-sport-matching-030,031 | venue-manage | P0 | draft | — | 2026-06-23 |
| 24 | [US-024](us-024.md) | Chủ sân duyệt booking | Partner | FR-sport-matching-026,032 | venue-manage | P0 | draft | — | 2026-06-23 |
| 25 | [US-025](us-025.md) | Chat với Player / Chủ sân | Player | FR-sport-matching-033,034 | chat-list, chat-detail | P1 | draft | — | 2026-06-23 |
| 26 | [US-026](us-026.md) | Notification Center | Player | FR-sport-matching-035,036 | notification-center, settings | P1 | draft | — | 2026-06-23 |
| 27 | [US-027](us-027.md) | Sửa profile + đổi mật khẩu | Player | FR-sport-matching-037,038 | settings | P1 | draft | — | 2026-06-23 |
| 28 | [US-028](us-028.md) | Cài đặt riêng tư + Xóa tài khoản | Player | FR-sport-matching-039,040 | settings | P1 | draft | — | 2026-06-23 |
| 29 | [US-029](us-029.md) | Điểm thưởng giảm giá | Player | FR-sport-matching-041 | settings, booking-confirm | P1 | draft | — | 2026-06-23 |
| 30 | [US-030](us-030.md) | Admin quản lý user | Admin | FR-sport-matching-042 | admin-dashboard | P1 | draft | — | 2026-06-23 |
| 31 | [US-031](us-031.md) | Onboarding chủ sân tự động | Partner | FR-sport-matching-047 | partner-onboard | P1 | draft | — | 2026-06-23 |
| 32 | [US-032](us-032.md) | Admin quản lý sân & booking | Admin | FR-sport-matching-043,044 | admin-dashboard | P1 | draft | — | 2026-06-23 |
| 33 | [US-033](us-033.md) | Admin dashboard & moderate | Admin | FR-sport-matching-045,046 | admin-dashboard | P1 | draft | — | 2026-06-23 |
| 34 | [US-034](us-034.md) | Tạo và quản lý đội | Player (Captain) | FR-sport-matching-048,049 | team-manage, court-select | P2 | draft | — | 2026-06-25 |
| 35 | [US-035](us-035.md) | Tạo và tham gia giải đấu | Player, Admin, Partner ⚠️ | FR-sport-matching-050,051,052 | tournament-list, tournament-detail | P2 | draft | — | 2026-06-25 |
| 36 | [US-036](us-036.md) | Social Feed | Player | FR-sport-matching-053,054,055,056 | social-feed, opponent-profile | P2 | draft | — | 2026-06-25 |
| 37 | [US-037](us-037.md) | Voucher + Referral | Player, Admin | FR-sport-matching-057,058,059 | voucher-list, booking-confirm, register | P2 | draft | — | 2026-06-25 |

**⚠️ Cần refactor (review 2026-06-25):**
- **US-035**: 3 personas (Player/Admin/Partner) trong 1 US vi phạm 1-persona rule. Cần split thành US-035a (Player tham gia giải) / US-035b (Admin+Partner quản lý giải) khi P2 sprint.
- **US-037**: Cover 3 FRs khác nhau (Voucher / Referral / Auto campaign). Cần split thành US-037a/b/c khi P2 sprint.

**Status values:** `draft` / `in-review` / `revisions` / `approved` / `shipped` / `archived` / `stale`.

**Jira column:** issue key sau khi `/jira --push` (vd `SM-12`). `—` nếu chưa push.

## Links upstream

- [[docs/sport-matching/srs/spec.md|SRS spec]]
- [[docs/sport-matching/usecases/_index.md|Use cases index]]
