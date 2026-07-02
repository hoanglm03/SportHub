---
type: srs-states
feature: sport-matching
updated: 2026-06-23
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

## State: Booking (Đặt sân)

```mermaid
stateDiagram-v2
    [*] --> pending: Player giữ chỗ
    [*] --> paid: Player thanh toán ngay
    pending --> paid: Thanh toán trong 30p
    pending --> expired: Hết 30p không thanh toán
    paid --> confirmed: Chủ sân duyệt
    paid --> rejected: Chủ sân từ chối
    paid --> auto_cancelled: Hết 30p không duyệt
    confirmed --> completed: Qua giờ chơi
    confirmed --> cancelled: Player hủy
    expired --> [*]
    rejected --> [*]
    auto_cancelled --> [*]
    completed --> [*]
    cancelled --> [*]
```

| Từ | Sang | Trigger | Reversible |
|----|------|---------|------------|
| (mới) | pending | Player chọn Giữ chỗ | Không |
| (mới) | paid | Player thanh toán ngay | Không |
| pending | paid | Thanh toán trong 30p | Không |
| pending | expired | Hết 30p không thanh toán | Không |
| paid | confirmed | Chủ sân duyệt trong 30p | Không |
| paid | rejected | Chủ sân từ chối → hoàn tiền auto | Không |
| paid | auto_cancelled | Hết 30p chủ sân không duyệt → hoàn tiền | Không |
| confirmed | completed | Qua giờ chơi | Không |
| confirmed | cancelled | Player hủy (hoàn tiền theo chính sách) | Không |

## State: Venue (Sân)

```mermaid
stateDiagram-v2
    [*] --> pending_review: Chủ sân submit
    pending_review --> active: Admin duyệt
    pending_review --> rejected: Admin từ chối
    rejected --> pending_review: Chủ sân sửa + submit lại
    active --> suspended: Admin khóa hoặc 5 lần không duyệt
    active --> inactive: Chủ sân tạm đóng
    suspended --> active: Admin mở lại
    inactive --> active: Chủ sân mở lại
```

| Từ | Sang | Trigger | Reversible |
|----|------|---------|------------|
| (mới) | pending_review | Chủ sân submit sân mới | Không |
| pending_review | active | Admin duyệt | Có (admin khóa) |
| pending_review | rejected | Admin từ chối + gửi lý do | Có (sửa + submit lại) |
| active | suspended | Admin khóa hoặc 5 lần không duyệt booking | Có (admin mở lại) |
| active | inactive | Chủ sân tạm đóng sân | Có (mở lại) |
