---
type: traceability
status: draft
created: 2026-06-07
updated: 2026-06-07
changelog:
  - 2026-06-07 | /gap | [sport-matching] initial scan, 5 gaps 0 conflicts, coverage 93%
---

# Traceability Matrix

## Feature: sport-matching

**Last scan:** 2026-06-07 | **Files:** 46 | **Coverage:** 93% | **Gaps:** 5 | **Conflicts:** 0

### Full Chain: BO → CAP → FR → US → AC → UC → Screen

| BRD Objective | PRD Capability | SRS FR | User Story | ACs | Use Case | Screens |
|---------------|----------------|--------|------------|-----|----------|---------|
| BO-sport-matching-01 | CAP-01 | FR-001, FR-002 | US-001, US-002 | 9 | uc-register | register, otp-verify, profile-setup |
| BO-sport-matching-01 | CAP-02 | FR-003, FR-004 | US-003 | 6 | uc-find-opponent | map-search, opponent-profile |
| BO-sport-matching-01 | CAP-03 | FR-005 | US-003 | (merged) | uc-find-opponent | map-search |
| BO-sport-matching-03 | CAP-04 | FR-006, FR-007 | US-004 | 7 | uc-book-match | court-select, invite-confirm, invite-waiting |
| BO-sport-matching-03 | CAP-05 | FR-008, FR-009, FR-010 | US-004, US-005 | 12 | uc-book-match | invite-confirm, invite-waiting, invite-receive, match-confirmed |
| BO-sport-matching-01 | CAP-06 | FR-011 | US-006 | 4 | uc-rate-opponent | rate-opponent |
| BO-sport-matching-01 | CAP-07 | FR-012 | US-007 | 4 | uc-view-history | match-history |
| BO-sport-matching-04 | CAP-08 | FR-013 | US-008 | 3 | — | (P1) |
| — | CAP-09 | FR-014 | US-009 | 3 | — | — |
| BO-sport-matching-02 | CAP-10 | FR-015 | US-010 | 3 | uc-manage-court | (P1) |
| BO-sport-matching-04 | CAP-11 | FR-016 | US-011 | 3 | — | (P1) |
| BO-sport-matching-04 | CAP-12 | FR-017 | US-012 | 3 | — | (P1) |
| — | CAP-13 | FR-018 | US-013 | 5 | — | (P2) |
| — | CAP-14 | FR-019 | US-014 | 3 | — | (P2) |
| — | CAP-15 | FR-020 | US-015 | 3 | — | (P2) |
| — | **⚠️ Missing CAP** | FR-021 | US-016 | 5 | — | rate-opponent |

**Totals:** 4 BO → 15 CAP → 21 FR → 16 US → 66 AC → 6 UC → 13 screens

### Error Matrix Coverage

| Error ID | Screen referenced | Screen exists | Error in AC |
|----------|-------------------|---------------|-------------|
| E-001 | map-search | ✓ | US-003 AC-002 ✓ |
| E-002 | map-search (invite-waiting) | ✓ | US-005 AC-003 ✓ |
| E-003 | map-search (invite-waiting) | ✓ | US-005 AC-002 ✓ |
| E-004 | map-search | ✓ | US-003 AC-005, US-004 AC-006 ✓ |
| E-005 | map-search | ✓ | US-004 AC-005, US-012 AC-002 ✓ |
| E-006 | map-search | ✓ | US-003 AC-003 ✓ |
| E-007 | court-select | ✓ | US-004 AC-002 ✓ |
| E-008 | match-confirmed | ⚠️ P2 (no cancel button yet) | US-013 AC-004 ✓ |
| E-009 | map-search | ⚠️ P2 (cooldown UI not in screen) | US-013 AC-005 ✓ |

### Gaps

| # | Severity | Rule | Description | Fix |
|---|----------|------|-------------|-----|
| 1 | WARNING | PRD CAP missing for FR | FR-021 "Report kết quả trận" has no PRD Capability | Add CAP-sport-matching-16 to PRD |
| 2 | WARNING | UC screen ref missing | uc-book-match missing invite-waiting screen | Add to Mục f |
| 3 | WARNING | Error screen P2 dep | E-008/E-009 reference screens without P2 UI elements | Fix when dev P2 |
| 4 | WARNING | Link asymmetry | Brainstorm links: [] empty, no forward links | Add forward links |
| 5 | SUGGESTION | P1/P2 screens placeholder | US-008→015 reference placeholder screens | Fix when dev v1.1/v2.0 |

### Conflicts

None detected.
