---
type: srs-states
feature: sport-matching
updated: 2026-06-04
---

# Sport Matching — State Diagrams

## State: Match

```mermaid
stateDiagram-v2
    [*] --> Created: Player gửi invite
    Created --> WaitingConfirm: Invite sent to opponent
    WaitingConfirm --> Confirmed: Opponent accept
    WaitingConfirm --> Expired: Timeout 5 phút
    WaitingConfirm --> Rejected: Opponent reject
    Confirmed --> InProgress: Đến giờ trận đấu
    InProgress --> Completed: Trận kết thúc
    Confirmed --> Cancelled: Player hủy (P2)
    Expired --> [*]
    Rejected --> [*]
    Completed --> [*]
    Cancelled --> [*]
```

| Từ | Sang | Trigger | Reversible |
|----|------|---------|------------|
| Created | WaitingConfirm | System gửi invite cho đối thủ | Không |
| WaitingConfirm | Confirmed | Đối thủ nhấn Accept | Không |
| WaitingConfirm | Expired | Timeout 5 phút không phản hồi | Không (tạo match mới) |
| WaitingConfirm | Rejected | Đối thủ nhấn Reject | Không (chọn đối thủ khác) |
| Confirmed | InProgress | Đến giờ trận đấu | Không |
| Confirmed | Cancelled | Player hủy trận (P2, max 3/tháng) | Không |
| InProgress | Completed | Trận kết thúc | Không |

## State: Slot

```mermaid
stateDiagram-v2
    [*] --> Available: Slot được tạo bởi Partner
    Available --> Locked: Player chọn slot (Pessimistic Lock)
    Locked --> Booked: Opponent confirm match
    Locked --> Available: Timeout 5 phút / Invite reject / expired
    Booked --> Completed: Trận đấu kết thúc
    Booked --> Available: Player hủy đặt sân (P2)
    Completed --> [*]
```

| Từ | Sang | Trigger | Reversible |
|----|------|---------|------------|
| Available | Locked | Player chọn sân + slot | Có (hết 5 phút) |
| Locked | Booked | Opponent accept match | Không (trừ hủy P2) |
| Locked | Available | Timeout 5 phút / reject / expired | Tự động |
| Booked | Completed | Trận đấu kết thúc | Không |
| Booked | Available | Player hủy (P2) | Slot quay về trống |

## State: Invite

```mermaid
stateDiagram-v2
    [*] --> Pending: Player gửi invite
    Pending --> Accepted: Opponent accept trong 5 phút
    Pending --> Rejected: Opponent reject
    Pending --> Expired: Timeout 5 phút
    Accepted --> [*]
    Rejected --> [*]
    Expired --> [*]
```

| Từ | Sang | Trigger | Reversible |
|----|------|---------|------------|
| Pending | Accepted | Opponent nhấn Accept | Không |
| Pending | Rejected | Opponent nhấn Reject | Không |
| Pending | Expired | 5 phút không phản hồi | Không |
