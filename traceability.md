---
type: traceability
status: draft
created: 2026-06-07
updated: 2026-06-24
changelog:
  - '2026-06-25 | /gap | [sport-matching] rescan post P2 batch + /review fixes: ~105 files, 9 gaps (0 blocking), 1 conflict, coverage 98%. Matrix rebuilt ở docs/_shared/traceability.md'
  - '2026-06-24 | /gap | [sport-matching] full rescan post P1 expansion: 89 files, coverage 97%, 4 suggestions, 0 blocking, 0 conflicts'
  - '2026-06-23 | /gap | [sport-matching] rescan: 4 gaps fixed (status drift, links, UC FR-021), coverage 98%, 1 OQ mới'
  - 2026-06-07 | /gap | [sport-matching] initial scan, 5 gaps 0 conflicts, coverage 93%
---

# Traceability Matrix

## Feature: sport-matching

**Last scan:** 2026-06-24 | **Files:** 89 | **Coverage:** 97% | **Gaps:** 4 (suggestions only) | **Blocking:** 0 | **Conflicts:** 0

### Inventory

| Artifact | Count |
|----------|-------|
| Brainstorms | 2 (geo-skill-matching, venue-search-booking) |
| URD | 1 |
| BRD | 1 (5 BO) |
| PRD | 1 (26 CAP: 8 P0 + 11 P1 + 3 P2 + 4 venue P0) |
| SRS spec | 1 (47 FR, 12 NFR, 26 BR, 25 Errors) |
| SRS flows | 1 (5 sequence diagrams) |
| SRS states | 1 (5 state machines: Match, Slot, Invite, Booking, Venue) |
| SRS ERD | 1 (23 entities) |
| Use Cases | 16 |
| User Stories | 33 (152 ACs total) |
| Screens | 27 |

### Full Chain: BO → CAP → FR → US → AC → UC → Screen

#### P0 — Matching Core

| BRD Obj | PRD Cap | SRS FR | User Story | ACs | Use Case | Screens |
|---------|---------|--------|------------|-----|----------|---------|
| BO-01 | CAP-01 | FR-001, FR-002 | US-001, US-002 | 9 | uc-register | login, register, otp-verify, profile-setup |
| BO-01 | CAP-02 | FR-003, FR-004 | US-003 | 6 | uc-find-opponent | map-search, opponent-profile |
| BO-01 | CAP-03 | FR-005 | US-003 | (merged) | uc-find-opponent | map-search |
| BO-03 | CAP-04 | FR-006, FR-007 | US-004 | 8 | uc-book-match | court-select, invite-confirm, invite-waiting |
| BO-03 | CAP-05 | FR-008, FR-009, FR-010 | US-004, US-005 | 13 | uc-book-match | invite-confirm, invite-waiting, invite-receive, match-confirmed |
| BO-01 | CAP-06 | FR-011 | US-006 | 5 | uc-rate-opponent | rate-opponent#rating-section |
| BO-01 | CAP-07 | FR-012 | US-007 | 4 | uc-view-history | match-history |
| BO-01 | CAP-16 | FR-021 | US-016 | 6 | uc-report-result | rate-opponent#report-result-section |

#### P0 — Venue Booking

| BRD Obj | PRD Cap | SRS FR | User Story | ACs | Use Case | Screens |
|---------|---------|--------|------------|-----|----------|---------|
| BO-05 | CAP-17 | FR-022, FR-023 | US-017 | 7 | uc-search-venue | venue-search, venue-detail |
| BO-05 | CAP-18 | FR-024, FR-025, FR-026 | US-018, US-019 | 13 | uc-book-venue | venue-detail, booking-confirm, booking-detail, venue-manage |
| BO-05 | CAP-19 | FR-027, FR-028 | US-020, US-021 | 8 | uc-cancel-venue-booking | booking-detail, venue-detail |
| BO-05 | CAP-21 | FR-030, FR-031, FR-032 | US-023, US-024 | 10 | uc-manage-venue | venue-manage, venue-register |

#### P1 — Enhancements

| BRD Obj | PRD Cap | SRS FR | User Story | ACs | Use Case | Screens |
|---------|---------|--------|------------|-----|----------|---------|
| BO-04 | CAP-08 | FR-013 | US-008 | 3 | (UC khi dev P1) | (P1 screens) |
| — | CAP-09 | FR-014 | US-009 | 3 | uc-rate-opponent (ELO) | — |
| BO-02 | CAP-10 | FR-015 | US-010 | 3 | uc-manage-court | (P1 screens) |
| BO-04 | CAP-11 | FR-016, FR-041 | US-011, US-029 | 7 | uc-profile-settings | settings |
| BO-04 | CAP-12 | FR-017 | US-012 | 3 | (UC khi dev P1) | (P1 screens) |
| BO-05 | CAP-20 | FR-029 | US-022 | 5 | uc-rate-venue | venue-rate, booking-detail |
| — | CAP-22 | FR-033, FR-034 | US-025 | 5 | uc-chat | chat-list, chat-detail |
| — | CAP-23 | FR-035, FR-036 | US-026 | 5 | uc-profile-settings | notification-center, settings |
| — | CAP-24 | FR-037, FR-038, FR-039, FR-040 | US-027, US-028 | 9 | uc-profile-settings | settings |
| — | CAP-25 | FR-042→046 | US-030, US-032, US-033 | 10 | uc-admin | admin-dashboard |
| — | CAP-26 | FR-047 | US-031 | 5 | uc-partner-onboard | partner-onboard |

#### P2 — Future

| BRD Obj | PRD Cap | SRS FR | User Story | ACs | Use Case | Screens |
|---------|---------|--------|------------|-----|----------|---------|
| — | CAP-13 | FR-018 | US-013 | 5 | (UC khi dev P2) | match-confirmed |
| — | CAP-14 | FR-019 | US-014 | 3 | uc-admin (future) | (P2 screens) |
| — | CAP-15 | FR-020 | US-015 | 3 | uc-admin (future) | admin-dashboard |

### Totals

| Metric | Count |
|--------|-------|
| BO | 5 |
| CAP | 26 (8 P0 + 13 P1 + 3 P2 + 2 venue P0) |
| FR | 47 |
| NFR | 12 |
| BR | 26 |
| Error | 25 |
| UC | 16 |
| US | 33 |
| AC | 152 |
| Screens | 27 |

### Error Matrix Coverage

| Error ID | Screen | In AC? | Notes |
|----------|--------|--------|-------|
| E-001 | map-search | ✓ US-003 | GPS off |
| E-002 | map-search | ✓ US-005 | Invite hết hạn |
| E-003 | map-search | ✓ US-005 | Đối thủ từ chối |
| E-004 | map-search | ✓ US-003, US-004 | Match pending |
| E-005 | map-search | ✓ US-004, US-012 | Hết limit invite |
| E-006 | map-search | ✓ US-003 | Không tìm thấy đối thủ |
| E-007 | court-select | ✓ US-004 | Sân hết slot |
| E-008 | match-confirmed | ✓ US-013 | Hủy vượt limit — screen fixed ✓ |
| E-009 | map-search | ✓ US-013 | Cooldown hủy — screen fixed ✓ |
| E-010 | venue-detail | ✓ US-017, US-018 | Khung giờ đã đặt |
| E-011 | booking-detail | ✓ US-019 | Hết giữ chỗ 30p |
| E-012 | booking-detail | ✓ US-018, US-024 | Chủ sân từ chối |
| E-013 | venue-detail | ✓ US-018, US-019 | Quá 3 booking |
| E-014 | venue-detail | ✓ US-018 | Đặt sát giờ |
| E-015 | chat-detail | ✓ US-025 | Ảnh chat quá lớn |
| E-016 | settings | ⚠️ US-027 (inline) | Mật khẩu cũ sai — no full E-code in AC body |
| E-017 | settings | ⚠️ US-027 (inline) | Mật khẩu mới yếu — no full E-code in AC body |
| E-018 | settings | ⚠️ US-028 (inline) | Xóa TK có booking — no full E-code in AC body |
| E-019 | partner-onboard | ⚠️ US-031 (inline) | Thiếu giấy tờ — no full E-code in AC body |
| E-020 | chat-detail | ⚠️ | Chat mất kết nối — không có AC riêng (system auto-retry) |
| E-021 | map-search, venue-search | ⚠️ US-017 | Maps unavailable — referenced nhưng no dedicated AC |
| E-022 | booking-confirm | ⚠️ US-018 | Payment timeout — referenced in error refs nhưng no dedicated AC |
| E-023 | — | ⚠️ | FCM fail — silent, no user-facing AC needed |
| E-024 | booking-detail | ✓ US-021 | Đã đổi 1 lần |
| E-025 | booking-detail | ✓ US-021 | Đổi trong 24h |

### Link Integrity

| Doc | Status | Links to | Links from | Integrity |
|-----|--------|----------|------------|-----------|
| brainstorm/geo-skill-matching | draft | URD, BRD, PRD, SRS | — (root) | ✓ |
| brainstorm/venue-search-booking | draft | URD, BRD, PRD, SRS | — (root) | ✓ |
| urd.md | in-review | brainstorm×2, BRD, PRD, SRS | brainstorm×2 | ✓ |
| brd.md | in-review | URD, brainstorm, PRD, SRS | URD | ✓ |
| prd.md | in-review | URD, BRD, brainstorm, SRS | BRD | ✓ |
| srs/spec.md | in-review | PRD, URD, BRD, brainstorm | PRD | ✓ |
| usecases/_index | draft | SRS | SRS | ✓ |
| userstories/_index | draft | SRS, UC index | SRS | ✓ |
| ascii-screen/_index | draft | SRS, UC index | SRS | ✓ |

### Status Consistency

| Doc | Status | Aligned? |
|-----|--------|----------|
| URD | in-review | ✓ |
| BRD | in-review | ✓ |
| PRD | in-review | ✓ |
| SRS | in-review | ✓ |
| UC index | draft | ⚠️ Downstream still draft (OK — reviewed but not promoted yet) |
| US index | draft | ⚠️ Same |
| Screen index | draft | ⚠️ Same |

### Gaps (remaining)

| # | Severity | Rule | Description | Action |
|---|----------|------|-------------|--------|
| 1 | SUGGESTION | Error in AC format | E-016→019 referenced inline in US but not as full `E-sport-matching-NNN` in AC body text. US-027/028/031 use natural language error messages instead of error codes | Low priority — messages match Error Matrix, `/gap` parser may miss |
| 2 | SUGGESTION | Error no AC | E-020 (chat disconnect), E-021 (maps fallback), E-022 (payment timeout), E-023 (FCM fail) are system-level errors with auto-recovery. No user-facing AC needed but no system-test AC exists | Create system-level test cases when dev sprint |
| 3 | SUGGESTION | P1/P2 screens placeholder | US-008→015 reference "(P1 screens)" or "(P2 screens)" — screens will be created when dev reaches those sprints | Expected for incremental development |
| 4 | SUGGESTION | UC/US index status draft | UC/US/Screen indexes still `draft` while URD→SRS are `in-review`. Consider promoting to `in-review` after this gap analysis confirms coverage | Promote when ready for stakeholder sign-off |

### Resolved since last scan (2026-06-23)

| # | Was | Resolution |
|---|-----|------------|
| 1 | BLOCKING (status drift) | URD/BRD/PRD promoted to in-review |
| 2 | BLOCKING (FR-021 missing CAP) | CAP-16 added to PRD |
| 3 | BLOCKING (FR-021 missing UC) | uc-report-result created |
| 4 | BLOCKING (gap hoàn tiền 12-24h) | Tier 12-24h 75% added to FR-027, BR-017, UC, US-020 |
| 5 | BLOCKING (payment security) | NFR-008→012 added |
| 6 | BLOCKING (chat underspec) | NFR-009, E-020 added |
| 7 | BLOCKING (OQ-1/OQ-2 stale) | Both resolved with concrete thresholds |
| 8 | BLOCKING (US-030 compound) | Split into US-030 + US-032 + US-033 |
| 9 | BLOCKING (US-020 duplicate AC ID) | Renumbered AC-002b→003, cascade |
| 10 | BLOCKING (uc-cancel tier mismatch) | Synced 4-tier policy |
| 11 | BLOCKING (booking-confirm countdown) | Clarified 10p slot hold vs 30p giữ chỗ |
| 12 | BLOCKING (login screen missing) | login.md created |
| 13 | BLOCKING (E-008/E-009 orphan screens) | match-confirmed cancel action + map-search E-009 added |
| 14 | WARNING (link asymmetry) | Forward links added across all docs |
| 15 | WARNING (FR-024 vs BR-011) | Aligned v1.0 cash / v1.1 online |
| 16 | WARNING (FR-040 edge cases) | Active match + wallet balance handled |
| 17 | WARNING (chat moderation) | Block/report/admin moderate added to FR-033 |
| 18 | WARNING (auth matrix) | BR-025/026 + NFR-012 + AC in US-018/030 |
| 19 | WARNING (concurrent lock AC) | US-004 AC-008 added |
| 20 | WARNING (US-016 compound AC) | Split nhắc 12h + auto-accept 24h |

### Conflicts

None detected.

### Cross-feature Dependencies

| From (sport-matching) | To (feature) | Link | Type |
|----------------------|--------------|------|------|
| FR-001 (đăng ký) | authentication | Shared auth flow | Overlap — sport-matching has own register, authentication feature has separate spec |
| FR-013 (thanh toán) | premium-payment | Payment gateway integration | Dependency — reuse MoMo/VNPay from premium-payment |
| FR-024 (đặt sân thanh toán) | premium-payment | Booking payment | Dependency — v1.1+ uses shared payment |

### Summary

Sport-matching đã đạt **97% coverage** sau 3 vòng review + fix:
- **0 BLOCKING** — tất cả đã resolved
- **0 WARNING** — tất cả đã resolved  
- **4 SUGGESTION** — low priority, expected cho incremental dev
- **0 CONFLICT** — status/owner/priority đồng nhất
- **20 issues resolved** kể từ scan đầu tiên (2026-06-07)

**Recommendation:** SRS + UC + US ready cho stakeholder review. Promote UC/US/Screen indexes lên `in-review` khi stakeholder sign-off.
