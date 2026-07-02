---
type: usecases-index
feature: sport-matching
status: draft
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-04
links:
  - docs/sport-matching/srs/spec.md
tags: [usecases, sport-matching]
stale_reason: ""
changelog:
  - 2026-06-26 | /gap | thêm 5 UCs P1/P2: uc-payment, uc-wallet, uc-premium, uc-notification, uc-cancel-match; fix uc-manage-court screen
  - 2026-06-25 | /review | fix S4: P2 block thêm header row cho format nhất quán
  - 2026-06-25 | /usecase | [uc-team-matching, uc-tournament, uc-social-feed, uc-promotions] 4 P2 UCs created
  - 2026-06-23 | /review | fix UC findings: rate-opponent component split, uc-cancel tier 12-24h, uc-view-history +FR-021, uc-admin +FR-021, uc-manage-court OQ FR-015 vs FR-047, uc-profile-settings +FR-035, FR orphan notes
  - 2026-06-23 | /usecase | [uc-search-venue, uc-book-venue, uc-cancel-venue-booking, uc-rate-venue, uc-manage-venue] 5 venue-booking UCs created
  - 2026-06-23 | /gap | [uc-report-result] created UC for FR-021 (gap fix)
  - 2026-06-04 | /srs | initial 6 UCs scaffolded
---

# Sport Matching — Use Cases Index

## Use cases

| Slug | Status | Actor | Related FR | Screens | Priority | Updated |
|------|--------|-------|-----------|---------|----------|---------|
| uc-register | draft | Player | FR-sport-matching-001, 002 | register, otp-verify, profile-setup | P0 | 2026-06-04 |
| uc-find-opponent | draft | Player | FR-sport-matching-003, 004, 005 | map-search, opponent-profile | P0 | 2026-06-04 |
| uc-book-match | draft | Player, Opponent | FR-sport-matching-006 đến 010 | court-select, invite-confirm, invite-receive, match-confirmed | P0 | 2026-06-04 |
| uc-rate-opponent | draft | Player | FR-sport-matching-011, 014 | rate-opponent | P0 | 2026-06-04 |
| uc-view-history | draft | Player | FR-sport-matching-012 | match-history | P0 | 2026-06-04 |
| uc-manage-court | draft | Partner, Staff | FR-sport-matching-015 | venue-register, venue-manage | P1 | 2026-06-26 |
| uc-report-result | draft | Player, Admin | FR-sport-matching-021, 012 | rate-opponent | P0 | 2026-06-23 |
| uc-payment | draft | Player | FR-sport-matching-013 | payment-checkout, booking-detail | P1 | 2026-06-26 |
| uc-wallet | draft | Player | FR-sport-matching-016, 041 | wallet, settings | P1 | 2026-06-26 |
| uc-premium | draft | Player | FR-sport-matching-017 | premium-upgrade, settings, map-search | P1 | 2026-06-26 |
| uc-notification | draft | Player | FR-sport-matching-035, 036 | notification-center, settings | P1 | 2026-06-26 |
| uc-search-venue | draft | Player | FR-sport-matching-022, 023 | venue-search, venue-detail | P0 | 2026-06-23 |
| uc-book-venue | draft | Player, Partner | FR-sport-matching-024, 025, 026 | venue-detail, booking-confirm, booking-detail, venue-manage | P0 | 2026-06-23 |
| uc-cancel-venue-booking | draft | Player | FR-sport-matching-027, 028 | booking-detail, venue-detail | P0 | 2026-06-23 |
| uc-rate-venue | draft | Player | FR-sport-matching-029 | venue-rate, booking-detail | P1 | 2026-06-23 |
| uc-manage-venue | draft | Partner, Admin, Staff | FR-sport-matching-030, 031, 032, 026 | venue-manage | P0 | 2026-06-23 |
| uc-chat | draft | Player, Partner | FR-sport-matching-033, 034 | chat-list, chat-detail | P1 | 2026-06-23 |
| uc-profile-settings | draft | Player | FR-sport-matching-036→041 | settings | P1 | 2026-06-23 |
| uc-admin | draft | Admin | FR-sport-matching-042→046 | admin-dashboard | P1 | 2026-06-23 |
| uc-partner-onboard | draft | Partner, Admin | FR-sport-matching-047 | partner-onboard | P1 | 2026-06-23 |


| uc-cancel-match | draft | Player | FR-sport-matching-018 | match-confirmed | P2 | 2026-06-26 |

**P2 — future roadmap:**

| Slug | Status | Actor | Related FR | Screens | Priority | Updated |
|------|--------|-------|-----------|---------|----------|---------|
| uc-team-matching | draft | Player (Captain) | FR-sport-matching-048, 049 | team-manage, court-select, match-confirmed | P2 | 2026-06-25 |
| uc-tournament | draft | Player, Admin, Partner | FR-sport-matching-050, 051, 052 | tournament-list, tournament-detail | P2 | 2026-06-25 |
| uc-social-feed | draft | Player, Admin | FR-sport-matching-053, 054, 055, 056 | social-feed, opponent-profile | P2 | 2026-06-25 |
| uc-promotions | draft | Player, Admin | FR-sport-matching-057, 058, 059 | voucher-list, booking-confirm, register | P2 | 2026-06-25 |

**FRs chưa có UC owner (P1/P2, UC tạo khi dev sprint):**
- FR-013 (Thanh toán online P1) → sẽ thuộc uc-book-venue khi P1 ready
- FR-016 (Ví điện tử P1) → sẽ thuộc uc-profile-settings
- FR-017 (Premium P1) → UC riêng khi dev
- FR-018 (Hủy trận P2) → UC riêng khi dev
- FR-019 (Phát hiện đánh giá ác ý P2) → thuộc uc-admin
- FR-020 (Báo cáo quản trị P2) → thuộc uc-admin
