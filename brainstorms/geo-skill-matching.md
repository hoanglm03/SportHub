---
type: brainstorm
feature: sport-matching
idea_slug: geo-skill-matching
status: draft
mode: deep
lang: vi
owner: "@hoangle"
created: 2026-06-03
updated: 2026-06-04
complexity_flags: [has_state_machine, has_async_flow, has_multi_role, has_throttle_rules]
links:
  - docs/sport-matching/urd.md
  - docs/sport-matching/brd.md
  - docs/sport-matching/prd.md
  - docs/sport-matching/srs/spec.md
tags: [brainstorm, sport-matching]
stale_reason: ""
changelog:
  - 2026-06-04 | /brainstorm | resolved OQ-1,OQ-2,OQ-3: Matching Score formula, thang 3 bậc ELO, limits hủy/cooldown
  - 2026-06-04 | /brainstorm | initial brainstorm, deep mode, 3 OQs flagged
---

# Sport Matching — Ghép đối thủ thể thao theo vị trí và trình độ

> Feature: sport-matching | Idea: geo-skill-matching
> 1 feature có thể có nhiều brainstorm — đây là 1 idea/draft độc lập.

## 1. Idea Seed

Ứng dụng cho phép matching những người ở gần theo tọa độ và có trình độ chơi thể thao ngang nhau, tạo thành 1 trận đấu. Multi-sport, ưu tiên cầu lông và pickleball.

## 2. Context

- **Vấn đề:** Người chơi thể thao hiện tại khó tìm đối thủ ngang trình độ gần mình. Phải qua các group, hội nhóm trên Facebook rất mất thời gian, không có cơ chế lọc trình độ hay vị trí.
- **Why now:** Gap trên thị trường VN — chưa có app nào chuyên matching thể thao theo vị trí + trình độ.
- **Định hướng:** Nền tảng kết hợp matching thể thao + đặt sân (E-commerce Platform có chức năng đặt chỗ). UI concept Search-centric tích hợp bản đồ trực quan (Map Integration), tối giản số bước trong hành trình đặt chỗ.
- **Môn ưu tiên:** Cầu lông, Pickleball (đang hot), mở rộng multi-sport.
- **Target ban đầu:** 100+ user.

## 3. User Types (preliminary)

| User Type | Pain Point | Primary Need |
|-----------|-----------|--------------|
| Player (Người chơi) | Khó tìm đối thủ ngang trình gần mình, phải qua group FB mất thời gian | Tìm đối thủ phù hợp nhanh, đặt sân tiện, chơi ngay |
| Partner (Chủ sân) | Sân trống nhiều slot, khó tiếp cận người chơi mới | Lấp đầy slot sân, tiếp cận player qua nền tảng |
| Staff (Nhân viên đối tác) | Quản lý đặt sân thủ công, dễ trùng lịch | Quản lý slot, xác nhận đặt chỗ, hỗ trợ player |
| Admin (Quản trị viên) | Cần giám sát toàn hệ thống, xử lý gian lận | Dashboard quản trị, moderate đánh giá, quản lý user/partner |

**Mô hình:** Freemium — free giai đoạn đầu để tạo critical mass, sau đó premium tier (unlimited invite, stats nâng cao, đặt sân nhanh) khi đạt 1.000+ user active.

**Gating:** Đăng ký cần verify email (OTP chính) + số điện thoại (SMS giai đoạn sau). Ai cũng đăng ký được.

## 4. Capabilities Breakdown

### P0 — must have
- Đăng ký + setup profile (chọn môn thể thao, tự đánh giá trình độ, tên hiển thị, email verify OTP)
- Matching đối thủ theo vị trí GPS + trình độ (Skill-level Filtering Matrix + Geolocation)
- Bản đồ trực quan hiện đối thủ/sân gần (Search-centric + Map Integration)
- Đặt sân (chọn sân + slot giờ + giữ chỗ tạm Pessimistic Locking 5 phút)
- Gửi/nhận invite ghép đôi (timeout 5 phút, auto chuyển đối thủ tiếp)
- Đánh giá đối thủ sau trận đấu

### P1 — should have
- Thanh toán qua MoMo / VNPay
- Cập nhật trình độ tự động dựa trên rating đối thủ
- Partner đăng ký sân lên hệ thống (tên, địa chỉ, tọa độ, slot giờ, giá, môn hỗ trợ)
- Ví điện tử nội bộ (In-app Wallet): số dư, nạp/rút, hoàn tiền dạng điểm thưởng

### P2 — nice to have
- Hủy trận / hủy đặt sân
- Premium tier (unlimited invite/ngày)
- Báo cáo quản trị (admin dashboard, analytics)
- Thuật toán phát hiện đánh giá ác ý

> P0/P1/P2 là tentative; final scope chốt ở `/prd sport-matching`.

## 5. Core Flows (Happy Path)

### 5.1 Luồng Matching + Đặt sân (flow chính)

1. Player mở app
2. System tự động dùng GPS xác định vị trí Player, dùng làm tâm điểm quét
3. Player chọn môn thể thao
4. System hiện bản đồ khu vực gần với danh sách đối thủ phù hợp (lọc theo Matching Score = vị trí + trình độ)
5. Player điều chỉnh filter nếu cần (bán kính 3-50km, trình độ)
6. Player chọn đối thủ từ danh sách
7. Player chọn sân + slot giờ
8. System giữ chỗ tạm (Pessimistic Slot Locking — 5 phút)
9. System gửi invite cho đối thủ (push notification qua FCM, timeout 5 phút)
10. Đối thủ nhận invite, xem thông tin trận, nhấn Accept
11. System xác nhận trận đấu — cả 2 nhận notification: thông tin đối thủ + sân + giờ

```
┌──────────────────┐
│  Player mở app   │
└────────┬─────────┘
         ▼
┌──────────────────┐
│ GPS tự động xác  │
│ định vị trí      │
└────────┬─────────┘
         ▼
     ┌────────┐
     │ GPS OK?│───NO───► "Bật Quyền truy cập vị trí"
     └───┬────┘          (dừng matching)
         │YES
         ▼
┌──────────────────┐
│ Chọn môn thể    │
│ thao + filter    │
│ (trình độ,       │
│  bán kính 3-50km)│
└────────┬─────────┘
         ▼
┌──────────────────┐
│ System quét đối  │
│ thủ theo Matching│
│ Score (vị trí +  │
│ trình độ)        │
└────────┬─────────┘
         ▼
     ┌─────────┐
     │Có đối   │───NO───► "Không tìm thấy đối thủ"
     │thủ?     │          ► Option: mở rộng filter
     └───┬─────┘
         │YES
         ▼
┌──────────────────┐
│ Hiện danh sách   │
│ trên bản đồ      │
└────────┬─────────┘
         ▼
     ┌──────────┐
     │Có match  │───YES──► "Hủy match cũ trước"
     │pending?  │
     └───┬──────┘
         │NO
         ▼
┌──────────────────┐
│ Player chọn đối  │
│ thủ + sân + slot │
└────────┬─────────┘
         ▼
     ┌─────────┐
     │Sân      │───NO───► Gợi ý sân/giờ khác
     │trống?   │          (tăng bán kính/đổi giờ)
     └───┬─────┘
         │YES
         ▼
┌──────────────────┐
│ System LOCK slot │
│ (5 phút)         │
└────────┬─────────┘
         ▼
┌──────────────────┐
│ Gửi invite đối  │
│ thủ (timeout 5p) │
└────────┬─────────┘
         ▼
     ┌──────────┐
     │Đối thủ  │───REJECT──► Thông báo Player
     │phản hồi?│              ► Chọn đối thủ khác
     └───┬─────┘              ► Release slot
         │
     TIMEOUT(5p)──► Auto hủy invite
         │          ► Release slot
         │          ► Tìm đối thủ tiếp
         │            (theo Matching Score)
         │ACCEPT
         ▼
┌──────────────────┐
│ MATCH CONFIRMED  │
│ Cả 2 nhận thông │
│ báo: đối thủ +   │
│ sân + giờ        │
└──────────────────┘
```

### 5.2 Luồng Đăng ký + Setup Profile

1. Player mở app lần đầu
2. Nhập email + mật khẩu + tên hiển thị
3. System gửi OTP qua email
4. Player nhập OTP xác thực
5. Player chọn ít nhất 1 môn thể thao
6. Player tự đánh giá trình độ cho từng môn (Mới chơi / Trung bình / Nâng cao)
7. System tạo profile, hiện màn hình chính (bản đồ)

### 5.3 Luồng Đánh giá sau trận

1. Sau trận đấu hoàn thành, system gửi nhắc nhở đánh giá
2. Player mở đánh giá đối thủ
3. Player chấm rating + nhận xét (optional)
4. System cập nhật rating trung bình đối thủ
5. Nếu rating liên tục cao hơn trình độ khai báo, system auto-adjust Matching Score

## 6. System Behavior Deep Dive

### 6.1 Decision Points

| ID | Flow | Khi nào | YES | NO |
|---|---|---|---|---|
| D1 | Matching | GPS có hoạt động không? | Tiếp tục quét đối thủ | Dừng matching, hiện thông báo bật GPS |
| D2 | Matching | Có đối thủ phù hợp trong bán kính + trình độ? | Hiện danh sách trên bản đồ | Thông báo "Không tìm thấy", gợi ý mở rộng filter |
| D3 | Matching | Player đang có match pending? | Chặn tạo match mới, yêu cầu hủy cái cũ | Cho phép tiếp tục |
| D4 | Đặt sân | Sân còn slot trống trong khung giờ? | Lock slot 5 phút, gửi invite | Gợi ý sân/vị trí khác + khung giờ khác |
| D5 | Invite | Đối thủ phản hồi trong 5 phút? | Accept dẫn tới confirm match; Reject dẫn tới thông báo Player chọn lại | Timeout dẫn tới auto hủy + tìm đối thủ tiếp theo (Matching Score) |
| D6 | Concurrent | 2 Player gửi invite cùng 1 đối thủ? | First-come-first-served: ai đến trước được phục vụ | Player sau nhận thông báo đối thủ đã có trận |
| D7 | Invite limit | Player free đã gửi 10 invite/ngày (per môn)? | Chặn môn đó, gợi ý nâng cấp Premium unlimited | Cho phép gửi tiếp |
| D8 | Hủy match | Player đã hủy 3 match/tháng? | Chặn hủy thêm (trừ lý do chính đáng) | Cho phép hủy |
| D9 | Cooldown | Player hủy 2 match liên tiếp trong 1 giờ? | Cooldown 15 phút, không cho tạo match mới | Cho phép tạo match |

### 6.2 Scenario Matrix

| Trạng thái Player | Điều kiện | Hành động | Kết quả |
|---|---|---|---|
| Free, chưa gửi invite hôm nay | GPS ON + có đối thủ | Gửi invite bình thường | Invite sent, đợi confirm |
| Free, đã gửi 10 invite hôm nay | Muốn gửi thêm | Chặn gửi invite | Gợi ý Premium |
| Đang có match pending | Muốn tạo match mới | Chặn tạo match | "Hủy match cũ trước" |
| GPS OFF | Mở matching | Dừng matching | "Bật quyền vị trí" |
| Đối thủ nhận invite | Đóng app, không phản hồi | Timeout 5 phút | Auto hủy, push notification vẫn hiện |
| Đối thủ nhận 2 invite cùng lúc | 2 Player gửi song song | First-come-first-served | Player 1 được, Player 2 bị từ chối |
| Player hủy match lần thứ 3/tháng | Đã dùng hết quota hủy | Chặn hủy | Thông báo "Đã đạt giới hạn hủy tháng này" |
| Player hủy 2 match liên tiếp trong 1 giờ | Trigger cooldown | Chặn tạo match 15 phút | Thông báo cooldown, đếm ngược |
| Free, đã gửi 10 invite/ngày cho cầu lông | Muốn gửi thêm invite cầu lông | Chặn invite cầu lông | Gợi ý Premium; invite môn khác vẫn OK |

### 6.3 State Transitions

**Match (Trận đấu):**

```
Tạo mới ──► Chờ đối thủ confirm ──► Đã confirm ──► Đang diễn ra ──► Hoàn thành
                    │                                     
                    ├──► Hết hạn (timeout 5p) ──► Tìm đối thủ mới / Hủy
                    │
                    └──► Đối thủ từ chối ──► Player chọn đối thủ khác
```

| Entity | Từ | Sang | Trigger | Quay lại được? |
|--------|------|------|---------|-------------|
| Match | Tạo mới | Chờ confirm | Player gửi invite | Không |
| Match | Chờ confirm | Đã confirm | Đối thủ accept | Không |
| Match | Chờ confirm | Hết hạn | Timeout 5 phút không phản hồi | Không (tạo match mới) |
| Match | Chờ confirm | Từ chối | Đối thủ reject | Không (chọn đối thủ khác) |
| Match | Đã confirm | Đang diễn ra | Đến giờ trận đấu | Không |
| Match | Đang diễn ra | Hoàn thành | Trận kết thúc | Không |

**Slot sân:**

```
Trống ──► Đang giữ tạm (locked 5p) ──► Đã đặt ──► Hoàn thành
                    │                       │
                    └──► Hết hạn 5p ──► Trống   └──► Hủy ──► Trống
```

| Entity | Từ | Sang | Trigger | Quay lại được? |
|--------|------|------|---------|-------------|
| Slot sân | Trống | Đang giữ tạm | Player chọn sân + slot | Có (hết hạn 5p) |
| Slot sân | Đang giữ tạm | Đã đặt | Đối thủ confirm match | Không (trừ hủy P2) |
| Slot sân | Đang giữ tạm | Trống | Hết hạn 5 phút / invite bị reject/timeout | Có (tự động) |
| Slot sân | Đã đặt | Hoàn thành | Trận đấu kết thúc | Không |
| Slot sân | Đã đặt | Hủy | Player hủy đặt sân (P2) | Có, slot quay về Trống |

### 6.4 Interrupted Transactions

| Tình huống | Hệ thống còn lại gì | Resume | Cleanup |
|---|---|---|---|
| Player đóng app giữa lúc chờ đối thủ confirm | Match ở trạng thái "Chờ confirm", slot vẫn locked | Mở lại app thấy trận đang chờ, tiếp tục đợi | Timeout 5 phút vẫn chạy, tự release nếu hết hạn |
| Đối thủ đóng app khi nhận invite | Invite vẫn pending, push notification đã gửi | Đối thủ mở app thấy invite, có thể accept/reject | Timeout 5 phút bình thường, auto hủy nếu hết |
| GPS mất tín hiệu / Player tắt quyền vị trí | Không thể quét đối thủ/sân | Player bật lại GPS, system resume matching | Không có slot nào bị lock (chưa đến bước đặt sân) |
| Mạng mất giữa bước giữ sân tạm | Slot đã locked trên server | Mạng lại, player thấy slot vẫn đang giữ | Slot vẫn lock 5 phút rồi tự release nếu không confirm |
| Player tạo match mới khi match cũ đang pending | Match cũ vẫn pending | Không cho phép — bắt hủy match cũ hoặc đợi hết hạn | Match cũ timeout 5 phút tự hủy, slot release |

### 6.5 Other Edge Cases

- **Player fake trình độ** (khai "Mới chơi" nhưng giỏi): Hệ thống auto-adjust — nếu liên tục nhận rating cao từ đối thủ, Matching Score tự động tăng, ghép với đối thủ mạnh hơn.
- **Đánh giá ác ý** (rate 1 sao không lý do): Thuật toán phát hiện mẫu đánh giá bất thường (vd 1 người luôn rate 1 sao). Admin xem xét + loại bỏ nếu cần. Dùng rating trung bình sau nhiều trận để giảm tác động đánh giá đơn lẻ.
- **Empty state** (app mới, chưa có đối thủ trong vùng): Hiện bản đồ trống + thông báo mời bạn bè, gợi ý mở rộng bán kính.
- **Concurrent lock slot**: 2 Player chọn cùng 1 slot sân cùng lúc — Pessimistic Locking đảm bảo chỉ 1 người lock được, người còn lại nhận thông báo slot đã hết.

## 7. Validation, Limits & Wording

### 7.1 Validation rules

| Field | Rule |
|---|---|
| Email | Bắt buộc, format email hợp lệ, verify qua OTP |
| Mật khẩu | Bắt buộc |
| Tên hiển thị | Bắt buộc |
| Môn thể thao | Bắt buộc ít nhất 1 môn, tối đa 5 môn ưu tiên hiển thị trên profile |
| Trình độ | Bắt buộc cho mỗi môn đã chọn (Mới chơi / Trung bình / Nâng cao) |

### 7.2 Limits & Quotas (exact values)

| Tham số | Giá trị | Window | Behavior khi vượt |
|---|---|---|---|
| Invite gửi/ngày (free) | 10 lần/môn | 24 giờ (reset 00:00) | Chặn gửi môn đó, gợi ý nâng cấp Premium (unlimited) |
| Hủy match/tháng | 3 lần | 30 ngày | Chặn hủy thêm (trừ lý do chính đáng hoặc trong khung hoàn tiền) |
| Cooldown sau hủy liên tiếp | 15 phút | Nếu hủy 2 match trong 1 giờ | Không cho tạo match mới trong 15 phút |
| Timeout invite | 5 phút | Per invite | Auto hủy invite + release slot + tìm đối thủ tiếp |
| Giữ slot sân tạm | 5 phút | Per booking | Auto release slot về trạng thái Trống |
| Bán kính tìm kiếm mặc định | 3 km | — | Player có thể tăng lên |
| Bán kính tìm kiếm tối đa | 50 km | — | Không cho vượt |
| Môn thể thao ưu tiên | 5 môn | Per profile | Chỉ 5 môn đầu hiển thị nổi bật |
| Match pending đồng thời | 1 trận | Per player | Chặn tạo match mới, yêu cầu hủy/đợi cái cũ |

### 7.3 Wording samples (exact strings)

#### Error messages

| Tình huống | Wording | Code |
|---|---|---|
| GPS bị tắt / mất quyền vị trí | "Không thể tìm kiếm đối thủ. Vui lòng bật Quyền truy cập vị trí để thuật toán Matchmaking hoạt động." | E-? |
| Invite hết hạn 5 phút | "Yêu cầu ghép đôi đã hết hạn (5 phút). Slot sân đã được giải phóng. Vui lòng thử tìm đối thủ khác." | E-? |
| Đối thủ từ chối | "Đối thủ đã từ chối trận đấu. Rất tiếc, bạn có muốn thử tìm Match mới ngay bây giờ không?" | E-? |
| Đã có match đang chờ | "Bạn đang có một trận đấu đang chờ xác nhận. Vui lòng hủy trận đấu hiện tại hoặc đợi kết quả trước khi tạo Match mới." | E-? |

#### Success messages

| Tình huống | Wording |
|---|---|
| Match confirmed | "Trận đấu đã được xác nhận! Hẹn gặp đối thủ tại {tên sân}, {giờ}." |
| Đăng ký thành công | "Chào mừng bạn đến với Sport Matching! Hãy chọn môn thể thao yêu thích." |
| Đánh giá gửi thành công | "Cảm ơn bạn đã đánh giá! Rating của đối thủ đã được cập nhật." |

#### Info / neutral messages

| Tình huống | Wording |
|---|---|
| Không tìm thấy đối thủ | "Không tìm thấy đối thủ nào trong khu vực của bạn. Thử mở rộng bán kính hoặc điều chỉnh trình độ?" |
| Đang chờ đối thủ confirm | "Đã gửi lời mời ghép đôi. Đang chờ đối thủ xác nhận (tối đa 5 phút)..." |
| Nhắc trước trận 1 giờ | "Nhắc nhở: Bạn có trận đấu tại {tên sân} lúc {giờ}. Sẵn sàng chưa?" |
| Nhắc đánh giá sau trận | "Trận đấu đã kết thúc! Hãy đánh giá đối thủ để cải thiện hệ thống ghép đôi." |

## 8. Assumptions

- Email là identifier chính cho account (unique).
- Trình độ ban đầu do Player tự khai báo, hệ thống điều chỉnh dần qua ELO-based rating (liên tục thắng/rating cao từ cùng bậc dẫn tới tự tăng bậc).
- Thang trình độ 3 bậc: Mới chơi (Beginner) / Trung bình (Intermediate) / Nâng cao (Advanced) — đã confirm.
- Matching Score formula: Môn thể thao 100% (hard filter, phải khớp) + Vị trí 40% + Trình độ 40% + Rating/uy tín 20%.
- Mỗi môn thể thao có trình độ riêng biệt.
- App hỗ trợ cả mobile (iOS + Android) — GPS là tính năng core.
- Partner (chủ sân) cung cấp dữ liệu slot giờ chính xác và cập nhật.
- Thanh toán P1 — giai đoạn đầu đặt sân không cần thanh toán online.
- Region: Việt Nam (VN) là thị trường chính.
- First-come-first-served cho concurrent invite.

## 9. Risks

| Rủi ro | Khả năng | Hậu quả nghiệp vụ | Cách phòng |
|--------|----------|-------------------|-----------|
| **Adoption chicken-and-egg:** User ít dẫn tới matching không hiệu quả (bán kính 3km không tìm thấy ai), user bỏ app, vòng xoáy tiêu cực | Thường | Mất user, app chết yểu, không tạo được critical mass | Tập trung launch theo khu vực (vd quận/thành phố cụ thể), seed user ban đầu qua các CLB thể thao, free hoàn toàn giai đoạn đầu |
| **Vendor dependency:** Google Maps API tăng phí hoặc MoMo/VNPay thay đổi policy/phí giao dịch | Thỉnh thoảng | Tăng chi phí vận hành, phải đổi vendor gấp, gián đoạn dịch vụ thanh toán | Thiết kế abstraction layer cho map + payment, có backup Mapbox + cổng thanh toán thay thế |
| **Partner onboard:** Chủ sân không muốn lên nền tảng, hoặc data slot giờ không chính xác dẫn tới đặt sân sai | Thường | Player đặt sân nhưng đến nơi không có slot, mất uy tín app | Hỗ trợ Partner onboard (Staff role), kiểm tra data định kỳ, cho phép Player report sân sai thông tin |

## 10. Success Criteria (preliminary)

- Matching rate: ≥ 70% yêu cầu tìm đối thủ có kết quả trong bán kính 10km.
- Thời gian từ mở app đến confirm trận: < 3 phút (trung bình).
- Tỷ lệ invite được accept: ≥ 50%.
- Tỷ lệ Player quay lại chơi trận thứ 2: ≥ 40% (retention).
- Rating trung bình đánh giá trải nghiệm app: ≥ 4.0/5.

## 11. Open Questions

- [x] OQ-1: Chi tiết công thức Matching Score — Resolved: Môn thể thao 100% (hard filter, phải khớp) + Vị trí 40% + Trình độ 40% + Rating/uy tín 20% (giá trị điều chỉnh). (source: OQ-123.docx)
- [x] OQ-2: Thang đo trình độ + auto-adjust — Resolved: 3 bậc (Mới chơi / Trung bình / Nâng cao). Cơ chế ELO-based: Player cấp Trung bình liên tục thắng/rating cao từ đối thủ Trung bình dẫn tới tự động chuyển sang Nâng cao. (source: OQ-123.docx)
- [x] OQ-3: Business limits bổ sung — Resolved: 10 invite/ngày per môn, hủy tối đa 3 lần/tháng, cooldown 15 phút nếu hủy 2 match liên tiếp trong 1 giờ, chỉ 1 slot pending (Pessimistic Locking 5 phút). (source: OQ-123.docx)

## 12. Next Steps

Sau brainstorm này (sau khi BA approve):
- `/urd sport-matching` — capture user perspective, inherit 3 OQ còn hold
- `/brd sport-matching` — business case (freemium model, ROI, partner onboard strategy)
- `/prd sport-matching` — product scope (chốt P0/P1/P2 final, release plan)
